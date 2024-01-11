<template>

  <main>
    <Textarea
        :name="'Название поля'"
        :header="'Текст перед полем ввода'"
        :showCounter="true"
        :maxlength="10"
    />
  </main>

</template>

<script setup>
import Textarea from './components/UI/Textarea.vue'
</script>

<style scoped>

</style>
