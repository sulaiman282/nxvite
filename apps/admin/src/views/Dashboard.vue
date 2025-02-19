<script setup>
import { ref, computed } from 'vue'
import { Chart } from 'chart.js/auto'

const dashboardStats = ref({
  totalProperties: 524,
  activeListings: 287,
  soldProperties: 237,
  totalRevenue: 12450000
})

const recentActivities = ref([
  {
    id: 1,
    type: 'Sale',
    details: 'Luxury Villa in Miami',
    amount: 1200000,
    date: '2025-02-18',
    status: 'Completed'
  },
  {
    id: 2,
    type: 'Listing',
    details: 'Modern Downtown Apartment',
    amount: 650000,
    date: '2025-02-17',
    status: 'Active'
  },
  {
    id: 3,
    type: 'Purchase',
    details: 'Suburban Family Home',
    amount: 450000,
    date: '2025-02-16',
    status: 'Pending'
  }
])

const propertyTypeDistribution = ref({
  labels: ['Residential', 'Commercial', 'Luxury', 'Investment'],
  data: [45, 25, 20, 10]
})

const formatCurrency = (value) => {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
  }).format(value)
}

const renderPieChart = (ctx, labels, data) => {
  new Chart(ctx, {
    type: 'pie',
    data: {
      labels: labels,
      datasets: [{
        data: data,
        backgroundColor: [
          'rgba(255, 99, 132, 0.8)',
          'rgba(54, 162, 235, 0.8)',
          'rgba(255, 206, 86, 0.8)',
          'rgba(75, 192, 192, 0.8)'
        ]
      }]
    },
    options: {
      responsive: true,
      plugins: {
        legend: {
          position: 'right'
        }
      }
    }
  })
}
</script>

<template>
  <div class="admin-dashboard">
    <div class="dashboard-header">
      <h1>Admin Dashboard</h1>
      <div class="dashboard-actions">
        <button class="btn-primary">Generate Report</button>
        <button class="btn-secondary">Export Data</button>
      </div>
    </div>

    <div class="dashboard-stats">
      <div class="stat-card">
        <div class="stat-icon">🏘️</div>
        <div class="stat-content">
          <h3>{{ dashboardStats.totalProperties }}</h3>
          <p>Total Properties</p>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">🔑</div>
        <div class="stat-content">
          <h3>{{ dashboardStats.activeListings }}</h3>
          <p>Active Listings</p>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">💰</div>
        <div class="stat-content">
          <h3>{{ formatCurrency(dashboardStats.totalRevenue) }}</h3>
          <p>Total Revenue</p>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">📈</div>
        <div class="stat-content">
          <h3>{{ dashboardStats.soldProperties }}</h3>
          <p>Sold Properties</p>
        </div>
      </div>
    </div>

    <div class="dashboard-insights">
      <div class="property-distribution">
        <h2>Property Type Distribution</h2>
        <canvas ref="pieChartRef" width="400" height="400"></canvas>
      </div>

      <div class="recent-activities">
        <h2>Recent Activities</h2>
        <table>
          <thead>
            <tr>
              <th>Type</th>
              <th>Details</th>
              <th>Amount</th>
              <th>Date</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="activity in recentActivities" :key="activity.id">
              <td>{{ activity.type }}</td>
              <td>{{ activity.details }}</td>
              <td>{{ formatCurrency(activity.amount) }}</td>
              <td>{{ activity.date }}</td>
              <td>
                <span :class="`status-${activity.status.toLowerCase()}`">
                  {{ activity.status }}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>
.admin-dashboard {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background-color: #f4f6f9;
  padding: 2rem;
}

.dashboard-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.dashboard-header h1 {
  color: #2c3e50;
  margin: 0;
}

.dashboard-actions {
  display: flex;
  gap: 1rem;
}

.btn-primary, .btn-secondary {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-primary {
  background-color: #3498db;
  color: white;
}

.btn-secondary {
  background-color: #ecf0f1;
  color: #2c3e50;
}

.dashboard-stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.stat-card {
  background-color: white;
  border-radius: 10px;
  padding: 1.5rem;
  display: flex;
  align-items: center;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
}

.stat-card:hover {
  transform: translateY(-5px);
}

.stat-icon {
  font-size: 3rem;
  margin-right: 1.5rem;
  opacity: 0.7;
}

.stat-content h3 {
  margin: 0 0 0.5rem 0;
  color: #2c3e50;
  font-size: 1.5rem;
}

.stat-content p {
  margin: 0;
  color: #7f8c8d;
}

.dashboard-insights {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.property-distribution, .recent-activities {
  background-color: white;
  border-radius: 10px;
  padding: 1.5rem;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
}

.recent-activities table {
  width: 100%;
  border-collapse: collapse;
}

.recent-activities th {
  background-color: #f4f6f9;
  text-align: left;
  padding: 1rem;
  border-bottom: 2px solid #e0e6ed;
}

.recent-activities td {
  padding: 1rem;
  border-bottom: 1px solid #e0e6ed;
}

.status-completed {
  color: #2ecc71;
  background-color: rgba(46, 204, 113, 0.1);
  padding: 0.25rem 0.5rem;
  border-radius: 3px;
}

.status-active {
  color: #3498db;
  background-color: rgba(52, 152, 219, 0.1);
  padding: 0.25rem 0.5rem;
  border-radius: 3px;
}

.status-pending {
  color: #f39c12;
  background-color: rgba(243, 156, 18, 0.1);
  padding: 0.25rem 0.5rem;
  border-radius: 3px;
}

@media (max-width: 1200px) {
  .dashboard-stats {
    grid-template-columns: repeat(2, 1fr);
  }

  .dashboard-insights {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .dashboard-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .dashboard-actions {
    margin-top: 1rem;
    width: 100%;
  }

  .btn-primary, .btn-secondary {
    width: 50%;
  }
}
</style>

<script>
export default {
  mounted() {
    if (this.$refs.pieChartRef) {
      renderPieChart(
        this.$refs.pieChartRef.getContext('2d'), 
        this.propertyTypeDistribution.labels, 
        this.propertyTypeDistribution.data
      )
    }
  }
}
</script>
