<template>
  <header class="site-header">
    <div class="logo">
  Student Registration System
</div>
    <nav>
      <a href="#" @click.prevent="$emit('navigate', 'home')">
        Home
      </a>

      <a href="#" @click.prevent="$emit('navigate', 'dashboard')">
        Dashboard
      </a>

      <a href="#" @click.prevent="$emit('navigate', 'enrolment')">
        Enrolment
      </a>

      <a href="#" @click.prevent="$emit('navigate', 'support')">
        Support
      </a>
    </nav>
  </header>
</template>

<script setup>
defineEmits(['navigate'])
</script>