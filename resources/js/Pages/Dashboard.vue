<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Pagination from '@/Components/Pagination.vue';
import { Head, Link, router } from '@inertiajs/vue3';

defineProps({
    students: {
        type: Object,
    },
});

function deleteStudent(student) {
    if (!confirm('Are you sure you want to delete the student?')) {
        return
    }
    router.delete(route('student.destroy', student.id))
}
</script>

<template>

    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <div className="flex justify-between items-center">
                <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Dashboard</h2>
                <Link :href="route('student.create')"
                    className="bg-emerald-500 py-1 px-3 text-white rounded shadow transition-all hover:bg-emerald-600">
                Add New Student
                </Link>
            </div>
        </template>
        <template #default>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                    <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg">
                        <div class="p-6 text-gray-900 dark:text-gray-100">
                            <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
                                <thead
                                    class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400 border-b-2 border-gray-500">
                                    <tr class="text-nowrap">
                                        <th class="px-4 py-2">ID</th>
                                        <th class="px-4 py-2">Image</th>
                                        <th class="px-4 py-2">Name</th>
                                        <th class="px-4 py-2">Age</th>
                                        <th class="px-4 py-2">Status</th>
                                        <th class="px-4 py-2 text-right">Actions</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="student in students.data" :key="student.id"
                                        class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                        <td class="px-4 py-2">{{ student.id }}</td>
                                        <td class="px-4 py-2">
                                            <img :src="student.image" :alt="student.name"
                                                class="w-8 h-8 rounded-full" />
                                        </td>
                                        <td class="px-4 py-2">{{ student.name }}</td>
                                        <td class="px-4 py-2">{{ student.age }}</td>
                                        <td class="px-4 py-2">{{ student.status }}</td>
                                        <td class="px-4 py-2 text-right">
                                            <Link :href="route('student.show', student.id)"
                                                class="text-green-600 dark:text-green-500 hover:underline mx-1">View
                                            </Link>
                                            <Link :href="route('student.edit', student.id)"
                                                class="font-medium text-blue-600 dark:text-blue-500 hover:underline mx-1">
                                            Edit</Link>
                                            <button @click="deleteStudent(student)"
                                                class="font-medium text-red-600 dark:text-red-500 hover:underline mx-1">
                                                Delete
                                            </button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                            <Pagination :links="students.meta.links" />
                        </div>
                    </div>
                </div>
            </div>

        </template>
    </AuthenticatedLayout>
</template>
