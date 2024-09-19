<script setup lang="ts">
import { useForm } from 'vee-validate';
import * as yup from 'yup';

/**=============
 ** VARIABLES
================*/
const phoneRegex = /^\(\d{3}\) \d{3}-\d{4}$/;
const MIN_AGE = 18;

/**===============
 ** VALIDATIONS
==================*/
const validationSchema = yup.object({
    fullName: yup.string().required('The fullname is a required field'),
    email: yup.string()
        .email('The email is not valid')
        .required('The email is a required field'),
    password: yup.string()
        .min(8, 'Password must be at least 8 characters')
        .test(
            'password-strength',
            'The password must include at least one uppercase letter, one lowercase letter, one number, and one special character',
            (value) => {
                if (typeof value !== 'string') return false;
                const strongPasswordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
                return strongPasswordRegex.test(value);
            }
        ),
    phoneNumber: yup.string()
        .matches(phoneRegex, 'Invalid phone number. The format should be (###) ###-####')
        .required('The phone number is a required field'),
    birthDate: yup.date()
        .required('The birthday is a required field')
        .max(new Date(), 'The birthday cannot be in the future')
        .test('is-old-enough', `You must be at least ${MIN_AGE} years old`, value => {
            if (!value) return false;
            const today = new Date();
            const birthDate = new Date(value);
            const age = today.getFullYear() - birthDate.getFullYear();
            const month = today.getMonth() - birthDate.getMonth();
            if (month < 0 || (month === 0 && today.getDate() < birthDate.getDate())) {
                return age - 1 >= MIN_AGE;
            }
            return age >= MIN_AGE;
        }),
    address: yup.string()
        .min(10, 'The address must be at least 10 characters.')
        .max(500, 'The address cannot be more than 500 characters')
        .required('The address is a required field'),
});

/**=====================
 ** USE FORM FUNCTION
========================*/
const { defineField, errors, handleSubmit } = useForm({
    validationSchema: validationSchema,
});

/**==========
 ** FIELDS
=============*/
const [fullName, fullNameAttrs] = defineField('fullName');
const [email, emailAttrs] = defineField('email');
const [password, passwordAttrs] = defineField('password');
const [phoneNumber, phoneNumberAttrs] = defineField('phoneNumber');
const [birthDate, birthDateAttrs] = defineField('birthDate');
const [address, addressAttrs] = defineField('address');

/**=============
 ** FUNCTIONS
================*/

/**===========================
 * HANDLE SUBMIT FUNCTION
 * @param {any} values
 * @returns {Promise<void>}
==============================*/
const onSubmit = handleSubmit(async (values): Promise<void> => {
    try {
        console.log('values:', JSON.stringify(values, null, 3));
    } catch (error) {
        console.error('Error:', error);
    }
});
</script>

<template>

    <div class="max-w-2xl mx-auto mt-10 p-6 border border-gray-300 rounded-lg shadow-md bg-white">

        <form @submit.prevent="onSubmit">

            <!--============
                FULL NAME 
            ================-->
            <div class="mb-4">
                <label 
                    for="fullName" 
                    class="block text-sm font-medium text-gray-700"
                >
                    Full Name
                </label>
                <input 
                    v-model="fullName" 
                    v-bind="fullNameAttrs" 
                    id="fullName" 
                    type="text" 
                    :class="['mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm', {'border-red-500': errors.fullName }]"
                />
                <span class="text-red-400" v-if="errors.fullName">
                    {{ errors.fullName }}
                </span>
            </div>

            <!--========
                EMAIL
            ============-->
            <div class="mb-4">
                <label 
                    for="email" 
                    class="block text-sm font-medium text-gray-700"
                >
                    Email
                </label>
                <input 
                    v-model="email" 
                    v-bind="emailAttrs" 
                    id="email" 
                    type="email"
                    :class="['mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm', { 'border-red-500': errors.email }]"
                />
                <span class="text-red-400" v-if="errors.email">
                    {{ errors.email }}
                </span>
            </div>

            <!--===========
                PASSWORD
            ===============-->
            <div class="mb-4">
                <label 
                    for="password" 
                    class="block text-sm font-medium text-gray-700"
                >
                    Password
                </label>
                <input
                    v-model="password"
                    v-bind="passwordAttrs"
                    id="password" 
                    type="password"
                    :class="['mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm', { 'border-red-500': errors.password }]"
                />
                <span class="text-red-400" v-if="errors.password">
                    {{ errors.password }}
                </span>
            </div>

            <!--=============== 
                PHONE NUMBER
            ===================-->
            <!-- TODO: PONER UNA MASCARA PARA NUMEROS DE TELEFONO -->
            <div class="mb-4">
                <label 
                    for="phone" 
                    class="block text-sm font-medium text-gray-700"
                >
                    Phone Number
                </label>
                <input 
                    v-model="phoneNumber" 
                    v-bind="phoneNumberAttrs" 
                    id="phone" 
                    type="tel"
                    :class="['mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm', { 'border-red-500': errors.phoneNumber }]"
                />
                <span class="text-red-400" v-if="errors.phoneNumber">
                    {{ errors.phoneNumber }}
                </span>
            </div>

            <!--================
                DATE OF BIRTH 
            ====================-->
            <div class="mb-4">
                <label 
                    for="birth_date" 
                    class="block text-sm font-medium text-gray-700">
                    Date of Birth
                </label>
                <input 
                    v-model="birthDate" 
                    v-bind="birthDateAttrs" 
                    id="birth_date" 
                    type="date"
                    :class="['mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm', { 'border-red-500': errors.birthDate }]"
                />
                <span class="text-red-400" v-if="errors.birthDate">
                    {{ errors.birthDate }}
                </span>
            </div>

            <!--==========
                ADDRESS 
            ==============-->
            <div class="mb-4">
                <label 
                    for="address" 
                    class="block text-sm font-medium text-gray-700"
                >
                    Address
                </label>
                <textarea 
                    v-model="address" 
                    v-bind="addressAttrs" 
                    id="address"
                    :class="['mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm', { 'border-red-500': errors.address }]"
                ></textarea>
                <span class="text-red-400" v-if="errors.address">
                    {{ errors.address }}
                </span>
            </div>

            <!--================
                SUBMIT BUTTON 
            ====================-->
            <div class="mt-6">
                <button type="submit"
                    class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                    Submit
                </button>
            </div>

        </form>

    </div>

</template>

<style scoped></style>