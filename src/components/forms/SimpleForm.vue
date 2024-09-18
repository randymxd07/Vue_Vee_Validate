<script setup lang="ts">

</script>

<template>

    <div class="max-w-2xl mx-auto mt-10 p-6 border border-gray-300 rounded-lg shadow-md bg-white">

        <form @submit.prevent="handleSubmit">

            <!-- Full Name -->
            <div class="mb-4">
                <label for="fullName" class="block text-sm font-medium text-gray-700">Full Name</label>
                <input id="fullName" type="text"
                    class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" />
            </div>

            <!-- Email -->
            <div class="mb-4">
                <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
                <input id="email" type="email"
                    class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" />
            </div>

            <!-- Password -->
            <div class="mb-4">
                <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
                <input id="password" type="password"
                    class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" />
            </div>

            <!-- Phone Number -->
            <div class="mb-4">
                <label for="phone" class="block text-sm font-medium text-gray-700">Phone Number</label>
                <input id="phone" type="tel"
                    class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" />
            </div>

            <!-- Gender -->
            <div class="mb-4">
                <label class="block text-sm font-medium text-gray-700">Gender</label>
                <div class="mt-1 flex items-center">
                    <label class="mr-4 flex items-center">
                        <input type="radio" value="male" class="form-radio text-indigo-600" />
                        <span class="ml-2">Male</span>
                    </label>
                    <label class="flex items-center">
                        <input type="radio" value="female" class="form-radio text-indigo-600" />
                        <span class="ml-2">Female</span>
                    </label>
                </div>
            </div>

            <!-- Date of Birth -->
            <div class="mb-4">
                <label for="dob" class="block text-sm font-medium text-gray-700">Date of Birth</label>
                <input id="dob" type="date"
                    class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" />
            </div>

            <!-- Address -->
            <div class="mb-4">
                <label for="address" class="block text-sm font-medium text-gray-700">Address</label>
                <textarea id="address"
                    class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"></textarea>
            </div>

            <!-- Submit Button -->
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