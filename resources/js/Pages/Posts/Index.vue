<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import Post from '@/Components/Post.vue';
import { useForm, Head } from '@inertiajs/vue3';

const form = useForm({
    title: '',
    content: '',
});

defineProps(['posts']);

</script>

<template>
    <Head title="Posts" />

    <AuthenticatedLayout>
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">

            <form @submit.prevent="form.post(route('posts.store'), { onSuccess: () => form.reset() })">

                <h1 class="text-xl font-semibold text-gray-900">Title</h1>

                <input 
                    type="text"
                    v-model="form.title"
                    placeholder="Title"
                    class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
                >

                <br>
                <h1 class="text-xl font-semibold text-gray-900">What's on your mind?</h1>

                <textarea
                    v-model="form.content"
                    placeholder="What's on your mind?"
                    class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
                ></textarea>

                <InputError :message="form.errors.message" class="mt-2" />
                
                <PrimaryButton class="mt-4">Post</PrimaryButton>
            </form>

            <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
                
                <Post
                    v-for="post in posts"
                    :key="post.id"
                    :post="post" 
                />

            </div>

        </div>
    </AuthenticatedLayout>

</template>