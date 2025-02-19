<script setup lang="ts">
import { ref, onMounted } from 'vue'

defineProps<{
  title: string;
}>();

const features = ref([
  {
    icon: '💼',
    title: 'Client Dashboard',
    description: 'Intuitive interface for managing your financial portfolio'
  },
  {
    icon: '📈',
    title: 'Real-time Analytics',
    description: 'Track your investments with live market data and insights'
  },
  {
    icon: '🔐',
    title: 'Secure Transactions',
    description: 'End-to-end encryption and multi-factor authentication'
  }
])

const animatedTitle = ref('')
const titleToAnimate = `Welcome ${new Date().getFullYear()} My Broker Client Portal 👋`

const copyToClipboard = (text: string) => {
  if (navigator && navigator.clipboard) {
    navigator.clipboard.writeText(text).catch(err => {
      console.error('Failed to copy text: ', err);
    });
  } else {
    console.warn('Clipboard API not available');
  }
}

const clientCommands = [
  {
    name: 'Start Client App',
    command: 'npm run client:start',
    description: 'Launch client development environment'
  },
  {
    name: 'Build Production',
    command: 'npm run client:build',
    description: 'Create optimized production build'
  }
]

const selectedCommand = ref(clientCommands[0])

onMounted(() => {
  let index = 0
  const typeWriter = () => {
    if (index < titleToAnimate.length) {
      animatedTitle.value += titleToAnimate.charAt(index)
      index++
      setTimeout(typeWriter, 50)
    }
  }
  typeWriter()
})
</script>

<template>
  <div class="client-welcome-container">
    <div class="welcome-header">
      <h1>{{ animatedTitle }}</h1>
    </div>

    <div class="feature-grid">
      <div 
        v-for="(feature, index) in features" 
        :key="index" 
        class="feature-card"
      >
        <div class="feature-icon">{{ feature.icon }}</div>
        <h3>{{ feature.title }}</h3>
        <p>{{ feature.description }}</p>
      </div>
    </div>

    <div class="project-actions">
      <div class="action-card">
        <h2>Client Quick Actions</h2>
        <div class="command-selector">
          <div class="command-list">
            <button 
              v-for="cmd in clientCommands" 
              :key="cmd.name"
              @click="selectedCommand = cmd"
              :class="{ active: selectedCommand.name === cmd.name }"
            >
              {{ cmd.name }}
            </button>
          </div>
          <div class="command-section">
            <div class="command-details">
              <p>{{ selectedCommand.description }}</p>
              <pre><code>{{ selectedCommand.command }}</code></pre>
            </div>
            <button 
              @click="() => copyToClipboard(selectedCommand.command)"
              class="copy-btn"
            >
              Copy Command
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.client-welcome-container {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  background-color: #f0f4f8;
  min-height: 100vh;
  color: #2c3e50;
}

.welcome-header {
  text-align: center;
  margin-bottom: 3rem;
  padding: 2rem;
  background: linear-gradient(135deg, #4a90e2 0%, #50c878 100%);
  border-radius: 15px;
  color: white;
  box-shadow: 0 15px 25px rgba(74, 144, 226, 0.2);
}

.welcome-header h1 {
  font-size: 2.5rem;
  font-weight: 600;
  letter-spacing: -0.025em;
  text-shadow: 0 2px 4px rgba(0,0,0,0.2);
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  margin-bottom: 3rem;
}

.feature-card {
  background-color: white;
  border-radius: 15px;
  padding: 2rem;
  text-align: center;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;
  border: 1px solid #e6e9f0;
}

.feature-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 25px rgba(74, 144, 226, 0.1);
  border-color: #4a90e2;
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  opacity: 0.8;
}

.feature-card h3 {
  color: #4a90e2;
  margin-bottom: 1rem;
  font-weight: 600;
}

.feature-card p {
  color: #7f8c8d;
}

.project-actions {
  display: flex;
  justify-content: center;
}

.action-card {
  background-color: white;
  border-radius: 15px;
  padding: 2rem;
  text-align: center;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.05);
  max-width: 800px;
  width: 100%;
  border: 1px solid #e6e9f0;
}

.command-selector {
  display: flex;
  flex-direction: column;
}

.command-list {
  display: flex;
  justify-content: center;
  margin-bottom: 1.5rem;
  gap: 1rem;
}

.command-list button {
  background-color: #f0f0f0;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.command-list button.active,
.command-list button:hover {
  background-color: #4a90e2;
  color: white;
}

.command-section {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-top: 1rem;
}

.command-details {
  flex-grow: 1;
  text-align: left;
}

.command-section pre {
  background-color: #2c3e50;
  color: #50c878;
  padding: 1rem;
  border-radius: 10px;
  font-family: 'Courier New', monospace;
  margin-top: 0.5rem;
}

.copy-btn {
  background-color: #4a90e2;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.copy-btn:hover {
  background-color: #50c878;
  transform: translateY(-3px);
}

@media (max-width: 1024px) {
  .feature-grid {
    grid-template-columns: 1fr;
  }

  .command-list {
    flex-direction: column;
  }
}
</style>
