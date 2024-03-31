<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';

defineProps({
    student: {
        type: Object,
    },
});
</script>

<template>

    <Head title="Student View" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Student - {{
                student.data.name
            }}</h2>
        </template>
        <template #default>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                    <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg">
                        <div class="p-6 text-gray-900 dark:text-gray-100">
                            <div class="flex flex-col">
                                <div class="flex flex-row">
                                    <div class="w-1/2">
                                        <img :src="student.data.image" :alt="student.data.name"
                                            class="w-32 h-32 rounded-full" />
                                    </div>
                                    <div class="w-1/2">
                                        <div class="flex flex-col">
                                            <div class="flex flex-row">
                                                <div class="w-1/2">
                                                    <p class="font-semibold">Name:</p>
                                                </div>
                                                <div class="w-1/2">
                                                    <p>{{ student.data.name }}</p>
                                                </div>
                                            </div>
                                            <div class="flex flex-row">
                                                <div class="w-1/2">
                                                    <p class="font-semibold">Age:</p>
                                                </div>
                                                <div class="w-1/2">
                                                    <p>{{ student.data.age }}</p>
                                                </div>
                                            </div>
                                            <div class="flex flex-row">
                                                <div class="w-1/2">
                                                    <p class="font-semibold">Status:</p>
                                                </div>
                                                <div class="w-1/2">
                                                    <p>{{ student.data.status }}</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </template>
    </AuthenticatedLayout>

</template>
