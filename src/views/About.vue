<script setup lang="ts">
import Section from '../components/layout/Section.vue'
import Lorem from '../components/shared/Lorem.vue'
import TitleSection from '../components/ui/TitleSection.vue'
</script>

<template>
  <Section id="about" aria-labelledby="heading-about">
    <TitleSection id="heading-about">About</TitleSection>
    <Lorem />
  </Section>
</template>

<style scoped>
</style>
