<script setup>
import router from '@/router';
import axios from 'axios';
import {reactive, onMounted} from 'vue';
import { useToast } from 'vue-toastification';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();

const jobId = route.params.id;

const form = reactive({
    type: 'Full-Time',
    title:'',
    description:'',
    salary:'',
    location:'',
    company:{
        name:'',
        description:'',
        contactEmail:'',
        contactEmail:'',
        contactPhone:'',
    }
});

const state = reactive({
    job:{},
    isLoading: true
});

const toast = useToast();

const handleSubmit = async()=>{
    const newJob = {
        type: form.type,
        title:form.title,
        description:form.description,
        salary:form.salary,
        location:form.location,
        company:{
            name:form.company.name,
            description:form.company.description,
            contactEmail:form.company.contactEmail,
            contactPhone:form.company.contactPhone,
    }};

    await addNewJob(newJob);

    toast.success("Job added succesfully");
};

onMounted(async ()=>{
    try {
        const response = await axios.get(`http://localhost:5000/jobs/${jobId}`);
        state.job = response.data;
        populateFormField(state.job);
    } catch (error) {
        console.log("Error Fetching Job:", error);
    } finally{
        state.isLoading = false;
    }
});

const populateFormField = (formFiels)=>{
    // Populate inputs
    form.type = formFiels.type;
    form.title = formFiels.title;
    form.description = formFiels.description;
    form.salary = formFiels.salary;
    form.location = formFiels.location;
    form.company.name = formFiels.company.name;
    form.company.description = formFiels.company.description;
    form.company.contactEmail = formFiels.company.contactEmail;
    form.company.contactPhone = formFiels.company.contactPhone;
};

const addNewJob = async(newJob)=>{
    try {
        const response = await axios.put(`http://localhost:5000/jobs/${jobId}`, newJob);

        router.push(`/jobs/${response.data.id}`);

    } catch (error) {
        console.log("Error Posting a new job:", error);
        toast.error("Error adding a new job")
    }
};

</script>

<template>
    <section class="job-form-section">
      <div class="container">
        <div class="form-wrapper">
          <form @submit.prevent="handleSubmit">
            <h2 class="form-title">Edit Job</h2>
  
            <div class="form-group">
              <label for="type">Job Type</label>
              <select id="type" name="type" required v-model="form.type">
                <option value="Full-Time">Full-Time</option>
                <option value="Part-Time">Part-Time</option>
                <option value="Remote">Remote</option>
                <option value="Internship">Internship</option>
              </select>
            </div>
  
            <div class="form-group">
              <label for="name">Job Listing Title</label>
              <input v-model="form.title" type="text" id="name" name="name" placeholder="e.g. Software Engineer" required />
            </div>
  
            <div class="form-group">
              <label for="description">Description</label>
              <textarea id="description" v-model="form.description" name="description" rows="4" placeholder="Job duties, expectations, etc"></textarea>
            </div>
  
            <div class="form-group">
              <label for="salary">Salary</label>
              <select id="salary" name="salary" required v-model="form.salary">
                <option value="Under $50K">Under $50K</option>
                <option value="$50K - $60K">$50K - $60K</option>
                <option value="$60K - $70K">$60K - $70K</option>
                <option value="$70K - $80K">$70K - $80K</option>
                <option value="$80K - $90K">$80K - $90K</option>
                <option value="$90K - $100K">$90K - $100K</option>
                <option value="$100K - $125K">$100K - $125K</option>
                <option value="$125K - $150K">$125K - $150K</option>
                <option value="$150K - $175K">$150K - $175K</option>
                <option value="$175K - $200K">$175K - $200K</option>
                <option value="Over $200K">Over $200K</option>
              </select>
            </div>
  
            <div class="form-group">
              <label for="location">Location</label>
              <input v-model="form.location"  type="text" id="location" name="location" placeholder="Company Location" required />
            </div>
  
            <h3 class="form-subtitle">Company Info</h3>
  
            <div class="form-group">
              <label for="company">Company Name</label>
              <input v-model="form.company.name" type="text" id="company" name="company" placeholder="Company Name" />
            </div>
  
            <div class="form-group">
              <label for="company_description">Company Description</label>
              <textarea v-model="form.company.description" id="company_description" name="company_description" rows="4" placeholder="What does your company do?"></textarea>
            </div>
  
            <div class="form-group">
              <label for="contact_email">Contact Email</label>
              <input v-model="form.company.contactEmail" type="email" id="contact_email" name="contact_email" placeholder="Email address for applicants" required />
            </div>
  
            <div class="form-group">
              <label for="contact_phone">Contact Phone</label>
              <input v-model="form.company.contactPhone" type="tel" id="contact_phone" name="contact_phone" placeholder="Optional phone for applicants" />
            </div>
  
            <div>
              <button class="submit-button" type="submit">Edit Job</button>
            </div>
          </form>
        </div>
      </div>
    </section>
  </template>
  
  <style>
  /* General Section Styling */
  .job-form-section {
    background-color: #f0fdf4; /* Light green */
    padding: 40px 0;
  }
  
  /* Centering the Form */
  .container {
    max-width: 640px;
    margin: 0 auto;
    padding: 0 20px;
  }
  
  /* Form Wrapper */
  .form-wrapper {
    background: white;
    padding: 24px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    border: 1px solid #e5e7eb;
  }
  
  /* Form Title */
  .form-title {
    text-align: center;
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 16px;
  }
  
  /* Form Subtitle */
  .form-subtitle {
    font-size: 20px;
    margin-bottom: 16px;
  }
  
  /* Form Group */
  .form-group {
    margin-bottom: 16px;
  }
  
  /* Labels */
  .form-group label {
    display: block;
    font-weight: bold;
    color: #374151;
    margin-bottom: 8px;
  }
  
  /* Inputs & Selects */
  .form-group input,
  .form-group select,
  .form-group textarea {
    width: 100%;
    padding: 8px;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    font-size: 16px;
  }
  
  /* Submit Button */
  .submit-button {
    width: 100%;
    background-color: #16a34a; /* Green */
    color: white;
    font-weight: bold;
    padding: 12px;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: background 0.2s;
  }
  
  .submit-button:hover {
    background-color: #15803d; /* Darker green */
  }
  
  /* Responsive Design */
  @media (max-width: 768px) {
    .container {
      max-width: 90%;
    }
  }
  </style>
  