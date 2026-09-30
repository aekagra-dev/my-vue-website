<template>
  <main>
    <section class="hero">
      <img
        src="https://images.unsplash.com/photo-1523240795612-9a054b0db644"
        alt="Students studying together"
      />

      <h1>Student Registration System</h1>

      <p>
        Manage your university information in one place.
      </p>
    </section>

    <section class="welcome">
      <h2>Welcome to the student registration system</h2>

      <p>
        This website allows students to manage and view information
        such as their attendance, grades, units and invoices.
      </p>

      <p>
        Students can use the system to access their university
        information in one place.
      </p>
    </section>

    <section class="login-area">
      <div class="student">
        <h2>Student</h2>

        <p>
          Students can login or register to access their university
          information.
        </p>

        <button @click="$emit('navigate', 'dashboard')">
          Login
        </button>

        <button @click="$emit('navigate', 'dashboard')">
          Register
        </button>
      </div>

      <div class="staff">
        <h2>Staff</h2>

        <p>
          Staff can login to manage student information and university
          records.
        </p>

        <button @click="$emit('navigate', 'dashboard')">
          Login
        </button>
      </div>
    </section>

    <section class="announcements">
      <h2>ANNOUNCEMENTS</h2>

      <div class="announcement-container">
        <article class="announcement">
          <h3>ANNOUNCEMENT 1</h3>
          <p>
            Unit enrolment information is now available.
          </p>
        </article>

        <article class="announcement">
          <h3>ANNOUNCEMENT 2</h3>
          <p>
            Please check your student information before the new
            semester begins.
          </p>
        </article>

        <article class="announcement">
          <h3>ANNOUNCEMENT 3</h3>
          <p>
            Students should check their timetable before attending
            their first class.
          </p>
        </article>
      </div>
    </section>
  </main>
</template>

<script setup>
defineEmits(['navigate'])
</script>