<script setup lang="ts">

const handleSmoothScroll = (event: Event): void => {
  event.preventDefault()
  
  const anchor = event.target as HTMLAnchorElement
  const targetId = anchor.getAttribute('href')
  
  if (!targetId?.startsWith('#')) return
  
  const targetElement = document.querySelector(targetId)
  if (!targetElement) return
  
	// Calculate the header height + safety margin
  const headerHeight = document.querySelector('header')?.getBoundingClientRect().height || 0
  const offset = 20 // extra space between header and content 
  
  const targetPosition = targetElement.getBoundingClientRect().top + window.scrollY - headerHeight - offset
  
  window.scrollTo({
    top: targetPosition,
    behavior: 'smooth'
  })
}

</script>

<template>
  <header class="sticky top-0 bg-white z-50">
    <nav>
      <ul class="nav-list" id="main-menu">
        <li><a @click="handleSmoothScroll" href="#what">What</a></li>
        <li><a @click="handleSmoothScroll" href="#about">About</a></li>
        <li><a @click="handleSmoothScroll" href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
nav {
  border: 5px dotted red;
}
</style>
