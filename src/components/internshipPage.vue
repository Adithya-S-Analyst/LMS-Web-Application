<script setup lang="ts">

import "../assets/internship.css";

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
                <button class="cta-button1">Get Started</button>
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
    <div class="eligible-groups">
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

</template>