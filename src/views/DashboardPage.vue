<template>
  <div class="dashboard-container">
    <!-- Sidebar Navigation -->
    <aside class="sidebar" :class="{ collapsed: isCollapsed }">
      <div class="collapse-btn-container" @click="toggleCollapse">
        <button class="collapse-btn">
          <i class="fas" :class="isCollapsed ? 'fa-arrow-right' : 'fa-arrow-left'"></i>
        </button>
      </div>
      <div class="navbar-content" v-if="!isCollapsed">
        <div class="section">
          <h4>Apps</h4>
          <ul>
            <li><router-link to="/dashboard">Dashboard</router-link></li>
            <li><router-link to="/calendar">Calendar</router-link></li>
            <li><router-link to="/contacts">Contacts</router-link></li>
            <li><router-link to="/gallery">Gallery</router-link></li>
            <li><router-link to="/cards">Cards</router-link></li>
            <li><router-link to="/mail">Mail</router-link></li>
            <li><router-link to="/e-commerce">E-commerce</router-link></li>
          </ul>
        </div>

        <div class="section">
          <h4>User Interface</h4>
          <ul>
            <li><router-link to="/layout">Layout</router-link></li>
            <li><router-link to="/themes">Themes</router-link></li>
            <li><router-link to="/icons">Icons</router-link></li>
            <li><router-link to="/multilanguage">Multilanguage</router-link></li>
            <li><router-link to="/typography">Typography</router-link></li>
            <li><router-link to="/helper-classes">Helper Classes</router-link></li>
            <li><router-link to="/element">Element</router-link></li>
          </ul>
        </div>

        <div class="section">
          <h4>Components</h4>
          <ul>
            <li><router-link to="/tables">Tables</router-link></li>
            <li><router-link to="/maps">Maps</router-link></li>
            <li><router-link to="/editors">Editors</router-link></li>
            <li><router-link to="/charts">Charts</router-link></li>
          </ul>
        </div>

        <div class="section">
          <h4>Pages</h4>
          <ul>
            <li><router-link to="/profile">Profile</router-link></li>
            <li><router-link to="/">Login</router-link></li>
            <li><router-link to="/register">Register</router-link></li>
            <li><router-link to="/invoice">Invoice</router-link></li>
            <li><router-link to="/feedback">Feedback</router-link></li>
          </ul>
        </div>
      </div>
    </aside>

    <main class="main-content">
      <div class="header">
        <div class="search-container">
          <input type="text" placeholder="Search..." />
        </div>
        <div class="user-icons">
          <router-link to="/profile" class="profile-link">Profile</router-link>
        </div>
      </div>

      <!-- Dashboard Cards -->
      <section class="cards">
        <div class="card" v-for="(value, index) in cardValues" :key="index">
          <h3>{{ value.title }}</h3>
          <p>{{ value.data }}</p>
        </div>
      </section>

      <!-- Chart (Revenue Statistics) -->
      <section class="chart">
        <canvas id="revenueChart"></canvas>
      </section>

      <!-- Progress Section -->
      <section class="progress-section">
        <h3>Progress</h3>
        <div v-for="(user, index) in usersProgress" :key="index" class="progress-item">
          <p>User {{ index + 1 }}: {{ user.progress }}%</p>
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: user.progress + '%' }"></div>
          </div>
        </div>
      </section>

      <!-- Reports Section -->
      <section class="reports">
        <h3>Reports</h3>
        <div class="report-item" v-for="(report, index) in reportValues" :key="index">
          <p>{{ report.label }}:</p>
          <span>{{ report.data }}</span>
        </div>
      </section>
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';
import { Chart, registerables } from 'chart.js';

Chart.register(...registerables);

export default defineComponent({
  name: 'DashboardPage',
  setup() {
    const totalUsers = ref(1500);
    const totalViews = ref(5000);
    const conversionRate = ref(3.2);
    const totalRevenue = ref(25000);
    const newUsers = ref(200);
    const newSales = ref(150);
    const isCollapsed = ref(false);
    const usersProgress = ref([{ progress: 75 }, { progress: 50 }, { progress: 90 }]);

    const cardValues = ref([
      { title: 'Users', data: totalUsers.value },
      { title: 'Views', data: totalViews.value },
      { title: 'Conversion', data: conversionRate.value + '%' },
      { title: 'Revenue', data: totalRevenue.value + '$' }
    ]);

    const reportValues = ref([
      { label: 'New Users', data: newUsers.value },
      { label: 'Total Views', data: totalViews.value },
      { label: 'New Sales', data: newSales.value }
    ]);

    const toggleCollapse = () => {
      isCollapsed.value = !isCollapsed.value;
    };

    // Initialize Chart
    onMounted(() => {
      const ctx = (document.getElementById('revenueChart') as HTMLCanvasElement).getContext('2d');
      if (ctx) {
        new Chart(ctx, {
          type: 'line',
          data: {
            labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
            datasets: [{
              label: 'Revenue',
              data: [5000, 1000, 15000, 7000, 2500, 30000, 3500],
              fill: false,
              borderColor: 'rgb(75, 192, 192)',
              tension: 0.1
            }]
          },
          options: {
            responsive: true,
            plugins: {
              legend: { position: 'top' },
              title: {
                display: true,
                text: 'Revenue Statistics'
              }
            }
          }
        });
      }
    });

    return {
      isCollapsed,
      usersProgress,
      cardValues,
      reportValues,
      toggleCollapse
    };
  }
});
</script>

<style scoped>
.dashboard-container {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  width: 250px;
  background-color: black;
  padding: 20px;
  transition: width 0.3s ease;
  height: 100vh;
  overflow-y: auto;
  position: fixed;
  left: 0;
  top: 0;
}

.sidebar.collapsed {
  width: 80px;
}

.sidebar.collapsed ~ .main-content {
  margin-left: 80px;
}

.main-content {
  margin-left: 250px;
  flex-grow: 1;
  padding: 50px;
  background-color: #ecf0f1;
  overflow-y: auto;
  height: 100vh;
  transition: margin-left 0.3s ease;
}

.collapse-btn-container {
  position: absolute;
  top: 20px;
  right: -15px;
  background-color: red;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.collapse-btn {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  font-size: 16px;
}

.navbar-content {
  color: white;
  padding-bottom: 20px;
}

.section {
  margin-bottom: 20px;
}

.section h4 {
  font-size: 16px;
  margin-bottom: 10px;
  color: #ecf0f1;
}

.section ul {
  list-style: none;
  padding: 0;
}

.section ul li {
  margin-bottom: 10px;
}

.section ul li a {
  color: #bdc3c7;
  text-decoration: none;
  display: block;
}

.section ul li a:hover {
  color: white;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.search-container {
  flex-grow: 1;
  margin-right: 20px;
  max-width: 20%;
}

.search-container input {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #bdc3c7;
}

.user-icons {
  display: flex;
  align-items: center;
}

.profile-link {
  color: black;
  margin-right: 10px;
  text-decoration: none;
  transition: color 0.3s ease, text-decoration 0.3s ease;
}

.profile-link:hover {
  color: green;
  text-decoration: underline;
}

.cards {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.card {
  background-color: white;
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  flex: 1;
  text-align: center;
}

.progress-section,
.reports {
  background-color: white;
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  margin-bottom: 20px;
}

.progress-item {
  margin-bottom: 10px;
}

.progress-bar {
  background-color: #bdc3c7;
  border-radius: 4px;
  overflow: hidden;
}

.progress-fill {
  background-color: #3498db;
  height: 10px;
  border-radius: 4px;
}

.reports {
  display: flex;
  justify-content: space-between;
}

.report-item {
  flex: 1;
  text-align: center;
}

.report-item p {
  margin: 0;
  font-weight: bold;
}

.report-item span {
  display: block;
  margin-top: 10px;
  font-size: 1.5em;
}
</style>
