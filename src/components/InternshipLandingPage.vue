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
            <!-- Hero Section -->
    <header id="home1" class="herointern">
      <div class="hero1-overlay"></div>
      <video class="hero1-video" autoplay loop muted playsinline>
        <source src="https://cdn.dribbble.com/uploads/48226/original/963b639949e9d26b654825a6c6e9d368.mp4?1689952459" type="video/mp4">
      </video>
      <div class="container">
        <div class="hero1-content" data-aos="fade-up">
          <h1 class="hero1-title">
            <span class="gradient-text">Shape Your Future</span>
            <br>in Technology
          </h1>
          <p class="hero1-description">
            Join our comprehensive internship program and gain hands-on experience with cutting-edge technologies. 
            Work on real projects, learn from industry experts, and kickstart your career.
          </p>
          <div class="button-group">
            <a href="#apply" class="button button-primary">Apply Now</a>
            <a href="#programs" class="button button-secondary">Explore Programs</a>
          </div>
        </div>
      </div>
    </header>

    <!-- Statistics Section -->
    <section class="stats">
      <div class="container">
        <div class="stats-grid" data-aos="fade-up">
          <div class="stat-card">
            <h3 class="stat-number">1000+</h3>
            <p class="stat-label">Graduates Placed</p>
          </div>
          <div class="stat-card">
            <h3 class="stat-number">95%</h3>
            <p class="stat-label">Placement Rate</p>
          </div>
          <div class="stat-card">
            <h3 class="stat-number">100+</h3>
            <p class="stat-label">Partner Companies</p>
          </div>
          <div class="stat-card">
            <h3 class="stat-number">15+</h3>
            <p class="stat-label">Years Experience</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Programs Section -->
    <section id="programs" class="programs">
      <div class="container">
        <h2 class="section-title">Our Programs</h2>
        <div class="accordion-list" data-aos="fade-up">
          <div v-for="(program, index) in ['Full Stack Development', 'Data Science & AI', 'Cloud Computing']" 
               :key="index"
               class="accordion">
            <button 
              class="accordion-header"
              @click="toggleAccordion(index)"
            >
              <h3>{{ program }}</h3>
              <span :style="{ transform: activeAccordion === index ? 'rotate(180deg)' : '' }">▼</span>
            </button>
            <div v-if="activeAccordion === index" class="accordion-content">
              <ul class="accordion-list">
                <li v-for="(item, i) in ['Frontend Development', 'Backend Development', 'Database Management', 'Modern Frameworks', 'DevOps & Deployment']" 
                    :key="i"
                    class="accordion-item">
                  <span>•</span>
                  <span>{{ item }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="projects">
      <div class="container">
        <h2 class="section-title">Student Projects</h2>
        <div class="projects-grid">
          <div v-for="(project, index) in ['AI-Powered Health Assistant', 'E-Commerce Platform', 'Cloud-Based CRM']"
               :key="index"
               class="project-card"
               data-aos="fade-up"
               :data-aos-delay="index * 100">
            <img :src="`https://picsum.photos/800/600?random=${index}`" :alt="project" class="project-image" />
            <div class="project-content">
              <h3 class="project-title">{{ project }}</h3>
              <p class="project-description">A sophisticated application leveraging cutting-edge technologies to deliver innovative solutions.</p>
              <div class="tag-list">
                <span class="tag">React</span>
                <span class="tag">Node.js</span>
                <span class="tag">MongoDB</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Application Form -->
    <section id="apply" class="apply">
      <div class="container">
        <h2 class="section-title">Apply Now</h2>
        <form class="form" data-aos="fade-up">
          <div class="form-group">
            <label class="form-label">First Name</label>
            <input type="text" class="form-input" />
          </div>
          <div class="form-group">
            <label class="form-label">Last Name</label>
            <input type="text" class="form-input" />
          </div>
          <div class="form-group">
            <label class="form-label">Email</label>
            <input type="email" class="form-input" />
          </div>
          <div class="form-group">
            <label class="form-label">Program of Interest</label>
            <select class="form-input">
              <option>Full Stack Development</option>
              <option>Data Science & AI</option>
              <option>Cloud Computing</option>
            </select>
          </div>
          <button type="submit" class="button button-primary">Submit Application</button>
        </form>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container1">
        <p>© 2024 EduSync Internship Program. All rights reserved.</p>
      </div>
    </footer>
    </div>

</template>