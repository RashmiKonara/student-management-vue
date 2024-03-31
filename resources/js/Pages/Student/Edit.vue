<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
import InputError from '@/Components/InputError.vue'
import InputLabel from '@/Components/InputLabel.vue'
import TextInput from '@/Components/TextInput.vue'
import SelectInput from '@/Components/SelectInput.vue'

const props = defineProps({
    student: {
        type: Object,
    },
});

const form = useForm({
    image: '',
    name: props.student.data.name || '',
    status: props.student.data.status || '',
    age: props.student.data.age || '',
    _method: 'PUT',
})

function onSubmit() {
    form.post(route('student.update', props.student.data.id))
}
</script>



<template>

    <Head title="Student View" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Student - {{
                student.data.name
            }} - EDIT</h2>
        </template>
        <template #default>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                    <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg">
                        <form @submit.prevent="onSubmit(student.data)"
                            class="p-4 sm:p-8 bg-white dark:bg-gray-800 shadow sm:rounded-lg">
                            <div v-if="student.data.image" class="mb-4 flex items-center justify-center">
                                <img :src="student.data.image" class="w-40 h-40 rounded-full" />
                            </div>
                            <div>
                                <InputLabel for="student_image_path" value="Student Image" />
                                <TextInput id="student_image_path" type="file" name="image" class="mt-1 block w-full"
                                    @input="form.image = $event.target.files[0]" />
                                <InputError :message="form.errors.image" class="mt-2" />
                            </div>
                            <div class="mt-4">
                                <InputLabel for="student_name" value="Student Name" />
                                <TextInput id="student_name" type="text" name="name" v-model="form.name"
                                    class="mt-1 block w-full" isFocused />
                                <InputError :message="form.errors.name" class="mt-2" />
                            </div>
                            <div class="mt-4">
                                <InputLabel for="student_age" value="Student Age" />
                                <TextInput id="student_age" type="number" name="age" v-model="form.age"
                                    class="mt-1 block w-full" isFocused />
                                <InputError :message="form.errors.age" class="mt-2" />
                            </div>
                            <div class="mt-4">
                                <InputLabel for="student_status" value="Student Status" />
                                <SelectInput name="status" id="student_status"
                                    class="mt-1 block w-full border-gray-300 dark:border-gray-700 dark:bg-gray-900 dark:text-gray-300 focus:border-indigo-500 dark:focus:border-indigo-600 focus:ring-indigo-500 dark:focus:ring-indigo-600 rounded-md shadow-sm"
                                    required v-model="form.status">
                                    <option value="active">Active</option>
                                    <option value="inactive">Inactive</option>
                                </SelectInput>
                                <InputError :message="form.errors.status" class="mt-2" />
                            </div>
                            <div class="mt-4 text-right">
                                <Link :href="route('dashboard') "
                                    class="bg-gray-100 py-1 px-3 text-gray-800 rounded shadow transition-all hover:bg-gray-200 mr-2">
                                Cancel
                                </Link>
                                <button type="submit"
                                    class="bg-emerald-500 py-1 px-3 text-white rounded shadow transition-all hover:bg-emerald-600">
                                    Update
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </template>
    </AuthenticatedLayout>
</template>
