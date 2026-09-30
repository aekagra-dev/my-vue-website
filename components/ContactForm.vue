<template>
  <section class="contact-form-section">
    <h1>Student Support</h1>

<form @submit.prevent="submitForm" novalidate>

      <div class="form-group">
        <label for="name">Full Name</label>

        <input
          id="name"
          type="text"
          v-model="form.name"
          placeholder="Enter your full name"
        />

        <p v-if="errors.name" class="error">
          {{ errors.name }}
        </p>
      </div>

      <div class="form-group">
        <label for="studentId">Student ID</label>

        <input
          id="studentId"
          type="text"
          v-model="form.studentId"
          placeholder="s123456789"
        />

        <p v-if="errors.studentId" class="error">
          {{ errors.studentId }}
        </p>
      </div>

      <div class="form-group">
        <label for="email">University Email</label>

        <input
          id="email"
          type="email"
          v-model="form.email"
          placeholder="student@deakin.edu.au"
        />

        <p v-if="errors.email" class="error">
          {{ errors.email }}
        </p>
      </div>

      <div class="form-group">
        <label for="year">Year of Study</label>

        <input
          id="year"
          type="number"
          v-model.number="form.yearOfStudy"
          min="1"
          max="6"
        />

        <p v-if="errors.yearOfStudy" class="error">
          {{ errors.yearOfStudy }}
        </p>
      </div>

      <div class="form-group">
        <label for="unit">Unit</label>

        <select id="unit" v-model="form.unit">
          <option value="">Select a unit</option>

          <option
            v-for="unit in units"
            :key="unit"
            :value="unit"
          >
            {{ unit }}
          </option>
        </select>

        <p v-if="errors.unit" class="error">
          {{ errors.unit }}
        </p>
      </div>

      <div class="form-group">
        <label for="enquiry">Enquiry Type</label>

        <select id="enquiry" v-model="form.enquiryType">
          <option value="">Select enquiry type</option>
          <option value="Unit enrolment">Unit enrolment</option>
          <option value="Attendance">Attendance</option>
          <option value="Results and grades">Results and grades</option>
          <option value="Tuition and payments">Tuition and payments</option>
          <option value="Account and profile">Account and profile</option>
          <option value="Other">Other</option>
        </select>

        <p v-if="errors.enquiryType" class="error">
          {{ errors.enquiryType }}
        </p>
      </div>

      <div class="form-group">
        <label for="description">Description</label>

        <textarea
          id="description"
          v-model="form.description"
          rows="5"
          placeholder="Describe your enquiry..."
        ></textarea>

        <p v-if="errors.description" class="error">
          {{ errors.description }}
        </p>
      </div>

      <fieldset class="form-group">
        <legend>Preferred Contact Method</legend>

        <label>
          <input
            type="radio"
            value="Email"
            v-model="form.contactMethod"
          />
          Email
        </label>

        <label>
          <input
            type="radio"
            value="Phone"
            v-model="form.contactMethod"
          />
          Phone
        </label>

        <p v-if="errors.contactMethod" class="error">
          {{ errors.contactMethod }}
        </p>
      </fieldset>

      <div class="form-group checkbox-group">
        <label>
          <input
            type="checkbox"
            v-model="form.confirmed"
          />
          I confirm that the information I have provided is correct.
        </label>

        <p v-if="errors.confirmed" class="error">
          {{ errors.confirmed }}
        </p>
      </div>

      <div class="form-buttons">
        <button
          type="button"
          @click="resetForm"
        >
          Reset
        </button>

        <button type="submit">
          Submit
        </button>
      </div>

      <p v-if="submitted" class="success">
        Your enquiry has been submitted successfully.
      </p>

    </form>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  initialData: {
    type: Object,
    default: () => ({})
  }
})

const emit = defineEmits(['submit-form'])

const units = [
  'SIT001',
  'SIT002',
  'SIT003',
  'SIT004'
]

function createForm() {
  return {
    name: props.initialData.name || '',
    studentId: props.initialData.studentId || '',
    email: props.initialData.email || '',
    yearOfStudy: props.initialData.yearOfStudy || null,
    unit: props.initialData.unit || '',
    enquiryType: props.initialData.enquiryType || '',
    description: props.initialData.description || '',
    contactMethod: props.initialData.contactMethod || '',
    confirmed: false
  }
}

const form = ref(createForm())

const errors = ref({})

const submitted = ref(false)

function validateForm() {
  errors.value = {}

  if (!form.value.name) {
    errors.value.name = 'Please enter your full name.'
  }

  if (!/^s\d{9}$/i.test(form.value.studentId)) {
    errors.value.studentId =
      'Student ID must contain s followed by 9 digits.'
  }

if (!form.value.email) {
  errors.value.email = 'Please enter your university email.'
} else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.value.email)) {
  errors.value.email = 'Please enter a valid email address.'
}

  if (
    !form.value.yearOfStudy ||
    form.value.yearOfStudy < 1 ||
    form.value.yearOfStudy > 6
  ) {
    errors.value.yearOfStudy =
      'Please enter a valid year of study.'
  }

  if (!form.value.unit) {
    errors.value.unit = 'Please select a unit.'
  }

  if (!form.value.enquiryType) {
    errors.value.enquiryType =
      'Please select an enquiry type.'
  }

  if (!form.value.description) {
    errors.value.description =
      'Please describe your enquiry.'
  }

  if (!form.value.contactMethod) {
    errors.value.contactMethod =
      'Please select a contact method.'
  }

  if (!form.value.confirmed) {
    errors.value.confirmed =
      'Please confirm that your information is correct.'
  }

  return Object.keys(errors.value).length === 0
}

function submitForm() {
  if (!validateForm()) {
    return
  }

emit('submit-form', { ...form.value })

  submitted.value = true

  setTimeout(() => {
    resetForm()
    submitted.value = false
  }, 2000)
}

function resetForm() {
  form.value = createForm()
  errors.value = {}
}
</script>