<script setup lang="ts">
import { ref, onMounted } from 'vue';
import '../assets/navbar.css';

interface Course {
  id: number;
  title: string;
  instructor: string;
  description: string;
  duration: string;
  level: string;
  category: string;
  enrollmentStatus: 'Open' | 'Closed' | 'In Progress';
  thumbnail: string;
}

const courses = ref<Course[]>([
  {
    id: 1,
    title: 'Introduction to Web Development',
    instructor: 'John Doe',
    description: 'Learn the fundamentals of web development including HTML, CSS, and JavaScript.',
    duration: '8 weeks',
    level: 'Beginner',
    category: 'Web Development',
    enrollmentStatus: 'Open',
    thumbnail: 'https://placehold.co/600x400'
  },
  {
    id: 2,
    title: 'Data Science Fundamentals',
    instructor: 'Jane Smith',
    description: 'Master the basics of data science, statistics, and Python programming.',
    duration: '12 weeks',
    level: 'Intermediate',
    category: 'Data Science',
    enrollmentStatus: 'In Progress',
    thumbnail: 'https://placehold.co/600x400'
  },
  {
    id: 3,
    title: 'Machine Learning Essentials',
    instructor: 'Mike Johnson',
    description: 'Explore machine learning algorithms and their practical applications.',
    duration: '10 weeks',
    level: 'Advanced',
    category: 'Machine Learning',
    enrollmentStatus: 'Open',
    thumbnail: 'https://placehold.co/600x400'
  }
]);

const searchQuery = ref('');
const selectedCategory = ref('All');
const selectedLevel = ref('All');

const categories = ['All', 'Web Development', 'Data Science', 'Machine Learning'];
const levels = ['All', 'Beginner', 'Intermediate', 'Advanced'];

const filteredCourses = computed(() => {
  return courses.value.filter(course => {
    const matchesSearch = course.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                         course.description.toLowerCase().includes(searchQuery.value.toLowerCase());
    const matchesCategory = selectedCategory.value === 'All' || course.category === selectedCategory.value;
    const matchesLevel = selectedLevel.value === 'All' || course.level === selectedLevel.value;
    
    return matchesSearch && matchesCategory && matchesLevel;
  });
});

const enrollInCourse = (courseId: number) => {
  // TODO: Implement enrollment logic
  console.log(`Enrolling in course ${courseId}`);
};
</script>

<template>
  <div class="course-management">
    <div class="filters">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search courses..."
        class="search-input"
      />
      
      <select v-model="selectedCategory" class="filter-select">
        <option v-for="category in categories" :key="category" :value="category">
          {{ category }}
        </option>
      </select>
      
      <select v-model="selectedLevel" class="filter-select">
        <option v-for="level in levels" :key="level" :value="level">
          {{ level }}
        </option>
      </select>
    </div>

    <div class="courses-grid">
      <div v-for="course in filteredCourses" :key="course.id" class="course-card">
        <img :src="course.thumbnail" :alt="course.title" class="course-thumbnail" />
        <div class="course-content">
          <h3>{{ course.title }}</h3>
          <p class="instructor">Instructor: {{ course.instructor }}</p>
          <p class="description">{{ course.description }}</p>
          <div class="course-details">
            <span class="duration">{{ course.duration }}</span>
            <span class="level">{{ course.level }}</span>
            <span :class="['status', course.enrollmentStatus.toLowerCase()]">{{ course.enrollmentStatus }}</span>
          </div>
          <button
            @click="enrollInCourse(course.id)"
            :disabled="course.enrollmentStatus === 'Closed'"
            class="enroll-button"
          >
            {{ course.enrollmentStatus === 'Closed' ? 'Enrollment Closed' : 'Enroll Now' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.course-management {
  padding: 2rem;
}

.filters {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
}

.search-input,
.filter-select {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

.search-input {
  flex: 1;
}

.courses-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.course-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.2s;
}

.course-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.course-thumbnail {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.course-content {
  padding: 1.5rem;
}

.course-content h3 {
  margin: 0 0 0.5rem;
  font-size: 1.25rem;
}

.instructor {
  color: #666;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.description {
  font-size: 0.9rem;
  margin-bottom: 1rem;
  line-height: 1.4;
}

.course-details {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
  font-size: 0.9rem;
}

.duration,
.level,
.status {
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  background-color: #f5f5f5;
}

.status.open {
  background-color: #e6f4ea;
  color: #1e7e34;
}

.status.closed {
  background-color: #fbe9e7;
  color: #d32f2f;
}

.status.in-progress {
  background-color: #fff3e0;
  color: #f57c00;
}

.enroll-button {
  width: 100%;
  padding: 0.75rem;
  border: none;
  border-radius: 4px;
  background-color: #1a73e8;
  color: white;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

.enroll-button:hover:not(:disabled) {
  background-color: #1557b0;
}

.enroll-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

@media (max-width: 768px) {
  .filters {
    flex-direction: column;
  }
  
  .courses-grid {
    grid-template-columns: 1fr;
  }
}
</style>