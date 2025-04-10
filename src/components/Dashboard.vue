<script setup lang="ts">
import { ref, computed } from 'vue';
import '../assets/navbar.css';

interface EnrolledCourse {
  id: number;
  title: string;
  progress: number;
  nextLesson: string;
  lastAccessed: string;
}

interface Recommendation {
  id: number;
  title: string;
  category: string;
  matchScore: number;
}

const enrolledCourses = ref<EnrolledCourse[]>([
  {
    id: 1,
    title: 'Introduction to Web Development',
    progress: 65,
    nextLesson: 'JavaScript Fundamentals',
    lastAccessed: '2024-01-15'
  },
  {
    id: 2,
    title: 'Data Science Fundamentals',
    progress: 30,
    nextLesson: 'Statistical Analysis',
    lastAccessed: '2024-01-14'
  }
]);

const recommendations = ref<Recommendation[]>([
  {
    id: 3,
    title: 'Machine Learning Essentials',
    category: 'Data Science',
    matchScore: 95
  },
  {
    id: 4,
    title: 'Advanced JavaScript Patterns',
    category: 'Web Development',
    matchScore: 88
  }
]);

const upcomingDeadlines = ref([
  {
    courseId: 1,
    title: 'JavaScript Project Submission',
    dueDate: '2024-01-20'
  },
  {
    courseId: 2,
    title: 'Data Analysis Report',
    dueDate: '2024-01-25'
  }
]);

const averageProgress = computed(() => {
  const total = enrolledCourses.value.reduce((sum, course) => sum + course.progress, 0);
  return Math.round(total / enrolledCourses.value.length);
});

const continueLearning = (courseId: number) => {
  // TODO: Implement navigation to course content
  console.log(`Continuing course ${courseId}`);
};

const viewCourseDetails = (courseId: number) => {
  // TODO: Implement navigation to course details
  console.log(`Viewing course ${courseId}`);
};
</script>

<template>
  <div class="dashboard">
    <header class="dashboard-header">
      <h1>Welcome back, Student!</h1>
      <p class="stats">Overall Progress: {{ averageProgress }}%</p>
    </header>

    <div class="dashboard-grid">
      <!-- Current Courses Section -->
      <section class="dashboard-section current-courses">
        <h2>Your Courses</h2>
        <div class="courses-list">
          <div v-for="course in enrolledCourses" :key="course.id" class="course-card">
            <div class="course-info">
              <h3>{{ course.title }}</h3>
              <div class="progress-bar">
                <div class="progress-fill" :style="{ width: `${course.progress}%` }"></div>
              </div>
              <p class="progress-text">{{ course.progress }}% Complete</p>
              <p class="next-lesson">Next: {{ course.nextLesson }}</p>
              <button @click="continueLearning(course.id)" class="continue-btn">
                Continue Learning
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- Recommendations Section -->
      <section class="dashboard-section recommendations">
        <h2>Recommended for You</h2>
        <div class="recommendations-list">
          <div v-for="course in recommendations" :key="course.id" class="recommendation-card">
            <div class="recommendation-info">
              <h3>{{ course.title }}</h3>
              <p class="category">{{ course.category }}</p>
              <div class="match-score">
                <span class="score">{{ course.matchScore }}%</span>
                <span class="match-label">Match</span>
              </div>
              <button @click="viewCourseDetails(course.id)" class="view-details-btn">
                View Details
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- Deadlines Section -->
      <section class="dashboard-section deadlines">
        <h2>Upcoming Deadlines</h2>
        <div class="deadlines-list">
          <div v-for="deadline in upcomingDeadlines" :key="deadline.courseId" class="deadline-card">
            <h3>{{ deadline.title }}</h3>
            <p class="due-date">Due: {{ deadline.dueDate }}</p>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
.dashboard {
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.dashboard-header {
  margin-bottom: 2rem;
  text-align: center;
}

.dashboard-header h1 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 0.5rem;
}

.stats {
  font-size: 1.1rem;
  color: #666;
}

.dashboard-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.dashboard-section {
  background: white;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.dashboard-section h2 {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 1.5rem;
}

.course-card,
.recommendation-card,
.deadline-card {
  background: #f8f9fa;
  border-radius: 8px;
  padding: 1.5rem;
  margin-bottom: 1rem;
}

.course-info h3,
.recommendation-info h3 {
  font-size: 1.2rem;
  color: #333;
  margin-bottom: 1rem;
}

.progress-bar {
  height: 8px;
  background: #e9ecef;
  border-radius: 4px;
  margin-bottom: 0.5rem;
}

.progress-fill {
  height: 100%;
  background: #1a73e8;
  border-radius: 4px;
  transition: width 0.3s ease;
}

.progress-text {
  font-size: 0.9rem;
  color: #666;
  margin-bottom: 0.5rem;
}

.next-lesson {
  font-size: 0.9rem;
  color: #666;
  margin-bottom: 1rem;
}

.continue-btn,
.view-details-btn {
  width: 100%;
  padding: 0.75rem;
  border: none;
  border-radius: 6px;
  background-color: #1a73e8;
  color: white;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

.continue-btn:hover,
.view-details-btn:hover {
  background-color: #1557b0;
}

.category {
  font-size: 0.9rem;
  color: #666;
  margin-bottom: 0.5rem;
}

.match-score {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.score {
  font-size: 1.2rem;
  font-weight: 500;
  color: #1a73e8;
}

.match-label {
  font-size: 0.9rem;
  color: #666;
}

.deadline-card {
  border-left: 4px solid #f57c00;
}

.deadline-card h3 {
  font-size: 1.1rem;
  color: #333;
  margin-bottom: 0.5rem;
}

.due-date {
  font-size: 0.9rem;
  color: #666;
}

@media (max-width: 768px) {
  .dashboard {
    padding: 1rem;
  }

  .dashboard-grid {
    grid-template-columns: 1fr;
  }
}
</style>