<template>
  <div>
    <AppHeader @navigate="changePage" />

    <HomeView
      v-if="currentPage === 'home'"
      @navigate="changePage"
    />

    <DashboardView
      v-else-if="currentPage === 'dashboard'"
    />

    <EnrolmentView
      v-else-if="currentPage === 'enrolment'"
    />

 <ContactForm
  v-else-if="currentPage === 'support'"
  :initial-data="{ name: 'Student' }"
  @submit-form="handleSubmission"
/>
   
   <section
  v-if="submittedData"
  class="acknowledgement-card"
>
  <h3>Enquiry Submitted</h3>

  <p>
    Thank you, {{ submittedData.name }}.
    Your enquiry has been received successfully.
  </p>

  <ul>
    <li>
      <strong>Student ID:</strong>
      {{ submittedData.studentId }}
    </li>

    <li>
      <strong>Email:</strong>
      {{ submittedData.email }}
    </li>

    <li>
      <strong>Year of Study:</strong>
      {{ submittedData.yearOfStudy }}
    </li>

    <li>
      <strong>Unit:</strong>
      {{ submittedData.unit }}
    </li>

    <li>
      <strong>Enquiry:</strong>
      {{ submittedData.enquiryType }}
    </li>

    <li>
      <strong>Preferred contact:</strong>
      {{ submittedData.contactMethod }}
    </li>
  </ul>
</section>

    <AppFooter />
  </div>
</template>

<script setup>
import { ref } from 'vue'

import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import HomeView from './components/HomeView.vue'
import DashboardView from './components/DashboardView.vue'
import EnrolmentView from './components/EnrolmentView.vue'
import ContactForm from './components/ContactForm.vue'

const currentPage = ref('home')

const submittedData = ref(null)

function changePage(page) {
  currentPage.value = page
}

function handleSubmission(data) {
  submittedData.value = data
}
</script>