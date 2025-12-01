<script setup lang="ts">
import { ref } from 'vue'

const isMobileMenuOpen = ref(false)

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
  
  // Close mobile menu after clicking a link
  isMobileMenuOpen.value = false
}

const toggleMobileMenu = (): void => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

</script>

<template>
  <header class="sticky top-0 bg-white z-50">
    <nav class="flex justify-between" style="border:1px solid red">
			
      <a href="#inicio" class="flex gap-1" aria-label="Ir al inicio">
        <div class="flex item-center justify-center w-[40px] h-[25px] font-bold bg-gray-700 text-white rounded-md" aria-hidden="true">MS</div>
        <span>Mi Sitio</span>
      </a>

      <button 
        @click="toggleMobileMenu" 
        class="hamburger-btn"
        aria-label="Toggle menu"
        aria-expanded="isMobileMenuOpen"
      >
        <span :class="{ 'open': isMobileMenuOpen }"></span>
        <span :class="{ 'open': isMobileMenuOpen }"></span>
        <span :class="{ 'open': isMobileMenuOpen }"></span>
      </button>

      <!-- Navigation Menu -->
      <ul 
        class="nav-list" 
        :class="{ 'mobile-open': isMobileMenuOpen }"
        id="main-menu"
      >
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
  position: relative;
  padding: 1rem;
}

/* Hamburger Button Styles */
.hamburger-btn {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  z-index: 100;
}

.hamburger-btn span {
  display: block;
  width: 25px;
  height: 3px;
  background-color: #333;
  transition: all 0.3s ease;
  border-radius: 2px;
}

/* Hamburger animation when open */
.hamburger-btn span.open:nth-child(1) {
  transform: rotate(45deg) translate(7px, 7px);
}

.hamburger-btn span.open:nth-child(2) {
  opacity: 0;
}

.hamburger-btn span.open:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -7px);
}

/* Desktop Navigation */
.nav-list {
  display: flex;
  gap: 2rem;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-list li a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  cursor: pointer;
  transition: color 0.3s ease;
}

.nav-list li a:hover {
  color: #007bff;
}

/* Mobile Styles */
@media (max-width: 768px) {
  .hamburger-btn {
    display: flex;
  }

  .nav-list {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    flex-direction: column;
    background-color: white;
    gap: 0;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
    border-top: 1px solid #eee;
  }

  .nav-list.mobile-open {
    max-height: 300px;
  }

  .nav-list li {
    border-bottom: 1px solid #eee;
  }

  .nav-list li a {
    display: block;
    padding: 1rem;
  }
}
</style>
