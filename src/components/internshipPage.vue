<script setup lang="ts">
import { ref, onMounted } from "vue";
import "../assets/internship.css";
import "../assets/navbar.css";
import AOS from 'aos';
import 'aos/dist/aos.css';

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

onMounted(() => {
  AOS.init({
    duration: 800,
    easing: 'ease-in-out',
    once: true
  });
  
  const container = document.querySelector(".scroll-container");
  container?.scrollTo({ left: 0, behavior: "instant" });
});

document.addEventListener("click", closeDropdown);

onMounted(() => {
  const container = document.querySelector(".scroll-container");
  container?.scrollTo({ left: 0, behavior: "instant" });

  const handleEscape = (e: KeyboardEvent) => {
    if (e.key === "Escape") activeDropdown.value = null;
  };

  document.addEventListener("keydown", handleEscape);
  document.addEventListener("click", closeDropdown);
});

const features = [
  'Industry-Relevant Curriculum',
  'Live Project Implementation',
  'Personal Mentorship & Guidance',
  'Soft Skills & Personality Development Sessions',
  'Resume & LinkedIn Profile Building Tips',
  'Interview Preparation & Mock Sessions',
  'Certificates & Recommendation Letters'
]

const certificates = [
  'Internship Completion Certificate',
  'Full Course Completion Certificate',
  'LOR (Letter of Recommendation) — based on performance',
  'IOR (Internship Offer Letter) — for internship participants'
]

const eligibleGroups = [
  'College Students (All Streams)',
  'Final Year Project Seekers',
  'Fresh Graduates',
  'Working Professionals',
  'Anyone Passionate to Upskill'
]
</script>

<template>
  <div class="internpage" :class="{ 'menu-open': isMenuOpen }">
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
          <a href="/internship">About Us</a>
        </li>
        <li class="nav-item" @click.stop="toggleDropdown('analytics')">
          <a href="/internlanding">Project Details and Internship</a>
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
    <section class="heromain">
          <div class="hero-content1">
              <h1 data-aos="fade-up">
                  <span class="highlight1">Unlock</span> Your Potential.<br>
                  <span class="highlight1">Upgrade</span> Your Skills.<br>
                  <span class="highlight1">Shape</span> Your Future.
              </h1>
              <p class="subtitle1" data-aos="fade-up" data-aos-delay="200">
                  Our Internship & Full Course Training Program is a career-oriented platform
                  designed to empower Students, Fresh Graduates, and Working Professionals.
              </p>
              <div class="cta-container1" data-aos="fade-up" data-aos-delay="400">
                <RouterLink to="/internlanding">
                  <button class="cta-button1">Get Started</button>
                </RouterLink>
              </div>
          </div>
    </section>
    <section class="features1">
          <h2 data-aos="fade-down">What We <span class="highlight1">Offer</span></h2>
          <div class="features-grid1">
          <div 
              v-for="(feature, index) in features" 
              :key="feature" 
              class="feature-item1"
              :data-aos="index % 2 === 0 ? 'fade-right' : 'fade-left'"
              :data-aos-delay="index * 100"
          >
              <span class="checkmark1">✓</span>
              {{ feature }}
          </div>
          </div>
    </section>
    <section class="certification">
      <h2 data-aos="fade-down">Certification & <span class="highlight1">Recognition</span></h2>
      <div class="certificates">
        <div 
          v-for="(cert, index) in certificates" 
          :key="cert" 
          class="cert-item"
          :data-aos="index % 2 === 0 ? 'zoom-in-right' : 'zoom-in-left'"
          :data-aos-delay="index * 100"
        >
          {{ cert }}
        </div>
      </div>
      <p class="quote" data-aos="fade-up">
        "Certificates are not just a document, they are proof of your growth and skills."
      </p>
    </section>

    <section class="eligibility">
      <h2 data-aos="fade-down">Who Can <span class="highlight1">Apply?</span></h2>
      <div class="eligible-groups":class="{ 'menu-open': isMenuOpen }">
        <div 
          v-for="(group, index) in eligibleGroups" 
          :key="group" 
          class="group-item"
          :data-aos="'flip-up'"
          :data-aos-delay="index * 100"
        >
          {{ group }}
        </div>
      </div>
    </section>
  </div>
</template>
