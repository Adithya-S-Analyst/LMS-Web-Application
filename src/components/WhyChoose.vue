<script setup lang="ts">
import { ref, onMounted } from "vue";
import "../assets/navbar.css";
import "../assets/whychoose.css";

const isMenuOpen = ref(false);

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}

const features = [
  {
    title: "Accessibility",
    description: "Anytime, anywhere access from desktop or mobile devices."
  },
  {
    title: "Interactivity",
    description: "Foster meaningful learning through forums, feedback, and collaborative tools."
  },
  {
    title: "Efficiency",
    description: "Reduce administrative workload with streamlined workflows."
  },
  {
    title: "Scalability",
    description: "Suitable for small seminars or institution-wide deployments."
  },
  {
    title: "Data Security",
    description: "Compliant with academic data protection and privacy standards."
  }
];


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

</script>

<template>
  <div class="Whypage">
    <!-- Navbar -->
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
    <main class="why-choose">
        <h2 class="why-title">WHY CHOOSE THIS LMS?</h2>
          <p class="why-intro">
            In an era where digital transformation defines educational success, this LMS empowers all users with:
          </p>
          <div class="features-grid">
            <div class="feature-card" v-for="(feature, index) in features" :key="index">
              <h3 class="feature-title">{{ feature.title }}</h3>
              <p class="feature-description">{{ feature.description }}</p>
            </div>
          </div>
    </main>
  </div>
</template>