<script setup>
import router from '@/router';
import { reactive } from 'vue';
import { useToast } from 'vue-toastification';
import axios from 'axios';
const form = reactive({
    type: 'Part-Time',
    title: '',
    description: '',
    salary: '',
    location: '',
    company: {
        name: '',
        description: '',
        contactEmail: '',
        contactPhone: ''
    }
})

const toast = useToast();
const handleSubmit = async () => {
    const newJob = {
        title: form.title,
        type: form.type,
        location: form.location,
        description: form.description,
        salary: form.salary,
        company: {
            name: form.company.name,
            description: form.company.description,
            contactEmail: form.company.contactEmail,
            contactPhone: form.company.contactPhone
        }
    }
    try {
        const response = await axios.post('https://json-server-xguj.onrender.com/jobs', newJob);
        toast.success('Job Added Successfully');
        router.push(`/jobs/${response.data.id}`)
    } catch (error) {
        console.error('Error fetching job', error);
        toast.error('Job Was Not Added')
    }
};

</script>
<template>
    <section class="bg-green-50">
        <div class="container m-auto max-w-2xl py-24">
            <div class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0">
                <form @submit.prevent="handleSubmit">
                    <h2 class="text-3xl text-center font-semibold mb-6">Add Job</h2>

                    <div class="mb-4">
                        <label for="type" class="block text-gray-700 font-bold mb-2">Job Type</label>
                        <select v-model="form.type" id="type" name="type" class="border rounded w-full py-2 px-3"
                            required>
                            <option value="Full-Time">Full-Time</option>
                            <option value="Part-Time">Part-Time</option>
                            <option value="Remote">Remote</option>
                            <option value="Internship">Internship</option>
                        </select>
                    </div>

                    <div class="mb-4">
                        <label class="block text-gray-700 font-bold mb-2">Job Listing Name</label>
                        <input type="text" v-model="form.title" id="name" name="name"
                            class="border rounded w-full py-2 px-3 mb-2" placeholder="eg. Beautiful Apartment In Miami"
                            required />
                    </div>
                    <div class="mb-4">
                        <label for="description" class="block text-gray-700 font-bold mb-2">Description</label>
                        <textarea id="description" v-model="form.description" name="description"
                            class="border rounded w-full py-2 px-3" rows="4"
                            placeholder="Add any job duties, expectations, requirements, etc"></textarea>
                    </div>

                    <div class="mb-4">
                        <label for="type" class="block text-gray-700 font-bold mb-2">Salary</label>
                        <select id="salary" v-model="form.salary" name="salary" class="border rounded w-full py-2 px-3"
                            required>
                            <option value="Under ₹10,000">Under ₹10,000</option>
                            <option value="₹10,000 - ₹15,000">₹10,000 - ₹15,000</option>
                            <option value="₹15,000 - ₹20,000">₹15,000 - ₹20,000</option>
                            <option value="₹20,000 - ₹25,000">₹20,000 - ₹25,000</option>
                            <option value="₹25,000 - ₹30,000">₹25,000 - ₹30,000</option>
                            <option value="₹30,000 - ₹40,000">₹30,000 - ₹40,000</option>
                            <option value="₹40,000 - ₹50,000">₹40,000 - ₹50,000</option>
                            <option value="₹50,000 - ₹60,000">₹50,000 - ₹60,000</option>
                            <option value="₹60,000 - ₹75,000">₹60,000 - ₹75,000</option>
                            <option value="₹75,000 - ₹1,00,000">₹75,000 - ₹1,00,000</option>
                            <option value="Over ₹1,00,000">Over ₹1,00,000</option>
                        </select>
                    </div>

                    <div class="mb-4">
                        <label class="block text-gray-700 font-bold mb-2">
                            Location
                        </label>
                        <input type="text" v-model="form.location" id="location" name="location"
                            class="border rounded w-full py-2 px-3 mb-2" placeholder="Company Location" required />
                    </div>

                    <h3 class="text-2xl mb-5">Company Info</h3>

                    <div class="mb-4">
                        <label for="company" class="block text-gray-700 font-bold mb-2">Company Name</label>
                        <input type="text" v-model="form.company.name" id="company" name="company"
                            class="border rounded w-full py-2 px-3" placeholder="Company Name" />
                    </div>

                    <div class="mb-4">
                        <label for="company_description" class="block text-gray-700 font-bold mb-2">Company
                            Description</label>
                        <textarea id="company_description" v-model="form.company.description" name="company_description"
                            class="border rounded w-full py-2 px-3" rows="4"
                            placeholder="What does your company do?"></textarea>
                    </div>

                    <div class="mb-4">
                        <label for="contact_email" class="block text-gray-700 font-bold mb-2">Contact Email</label>
                        <input type="email" v-model="form.company.contactEmail" id="contact_email" name="contact_email"
                            class="border rounded w-full py-2 px-3" placeholder="Email address for applicants"
                            required />
                    </div>
                    <div class="mb-4">
                        <label for="contact_phone" class="block text-gray-700 font-bold mb-2">Contact Phone</label>
                        <input type="tel" v-model="form.company.contactPhone" id="contact_phone" name="contact_phone"
                            class="border rounded w-full py-2 px-3" placeholder="Optional phone for applicants" />
                    </div>

                    <div>
                        <button
                            class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
                            type="submit">
                            Add Job
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </section>
</template>