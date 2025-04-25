<script setup lang="ts">
import { ref, onMounted } from "vue";
import "../assets/navbar.css";
import "../assets/InternLandingPg.css";

const isMenuOpen = ref(false);

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}

const activeDropdown = ref<string | null>(null);


const toggleDropdown = (menu: string) => {
  activeDropdown.value = activeDropdown.value === menu ? null : menu;
};

const closeDropdown = (event: MouseEvent) => {
  if (!(event.target as HTMLElement).closest(".nav-item")) {
    activeDropdown.value = null;
  }
};

</script>

<template>
    <nav class="navbar">
      <RouterLink to="/dashboard">
        <div class="navbar-logo">
          <img src="/FinalLogo.png" alt="EduSync"></img>
        </div>
      </RouterLink>
      <div class="hamburger" @click="toggleMenu">
        <span></span>
        <span></span>
        <span></span>
      </div>
      <ul class="nav-links" :class="{ 'show-menu': isMenuOpen }">
        <li class="nav-item" @click.stop="toggleDropdown('courses')">
          <a href="#">Courses</a>
          <svg class="caret" :class="{ open: activeDropdown === 'courses' }" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6 9 12 15 18 9" /></svg>
          <ul class="dropdown" :class="{ show: activeDropdown === 'courses' }">
            <li><a href="#">Web Development</a></li>
            <li><a href="#">Data Science</a></li>
            <li><a href="#">Machine Learning</a></li>
          </ul>
        </li>
        <li class="nav-item" @click.stop="toggleDropdown('analytics')">
          <a href="#">Analytics</a>
          <svg class="caret" :class="{ open: activeDropdown === 'analytics' }" width="16" height="16" viewBox="0 0 24 24"><polyline points="6 9 12 15 18 9" /></svg>
          <ul class="dropdown" :class="{ show: activeDropdown === 'analytics' }">
            <li><a href="#">Reports</a></li>
            <li><a href="#">Trends</a></li>
            <li><a href="#">Performance</a></li>
          </ul>
        </li>
        <li class="nav-item" @click.stop="toggleDropdown('enrolled')">
          <a href="#">Enrolled Courses</a>
          <svg class="caret" :class="{ open: activeDropdown === 'enrolled' }" width="16" height="16" viewBox="0 0 24 24"><polyline points="6 9 12 15 18 9" /></svg>
          <ul class="dropdown" :class="{ show: activeDropdown === 'enrolled' }">
            <li><a href="#">My Courses</a></li>
            <li><a href="#">Progress</a></li>
          </ul>
        </li>
        <li class="nav-item" @click.stop="toggleDropdown('lab')">
          <a href="#">Lab</a>
          <svg class="caret" :class="{ open: activeDropdown === 'lab' }" width="16" height="16" viewBox="0 0 24 24"><polyline points="6 9 12 15 18 9" /></svg>
          <ul class="dropdown" :class="{ show: activeDropdown === 'lab' }">
            <li><a href="#">Practice Problems</a></li>
            <li><a href="#">Code Challenges</a></li>
          </ul>
        </li>
        <li class="nav-item" @click.stop="toggleDropdown('certificates')">
          <a href="#">Certificates</a>
          <svg class="caret" :class="{ open: activeDropdown === 'certificates' }" width="16" height="16" viewBox="0 0 24 24"><polyline points="6 9 12 15 18 9" /></svg>
          <ul class="dropdown" :class="{ show: activeDropdown === 'certificates' }">
            <li><a href="#">Earned Certificates</a></li>
            <li><a href="#">Upcoming Certifications</a></li>
          </ul>
        </li>
        <li class="nav-item" @click.stop="toggleDropdown('profile')">
          <a href="#">Profile</a>
          <svg class="caret" :class="{ open: activeDropdown === 'profile' }" width="16" height="16" viewBox="0 0 24 24"><polyline points="6 9 12 15 18 9" /></svg>
          <ul class="dropdown" :class="{ show: activeDropdown === 'profile' }">
            <li><a href="#">Settings</a></li>
            <li><a href="/login">Logout</a></li>
          </ul>
        </li>
      </ul>
    </nav>
    
    <div class="intern-L-content">
    
    </div>

</template>