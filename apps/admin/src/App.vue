<script setup>
import { ref } from 'vue'
import { RouterView, RouterLink } from 'vue-router'

const adminTitle = ref('My Broker Cloud - Admin Portal')
const user = ref({
  name: 'Admin User',
  role: 'Super Administrator'
})

const sidebarLinks = ref([
  { icon: '', name: 'Dashboard', path: '/dashboard' },
  { icon: '', name: 'Properties', path: '/properties' },
  { icon: '', name: 'Users', path: '/users' },
  { icon: '', name: 'Reports', path: '/reports' },
  { icon: '', name: 'Settings', path: '/settings' }
])
</script>

<template>
  <div class="admin-container">
    <header class="admin-header">
      <div class="header-logo">
        <h1>{{ adminTitle }}</h1>
      </div>
      <div class="header-user-info">
        <div class="user-details">
          <span class="user-name">{{ user.name }}</span>
          <span class="user-role">{{ user.role }}</span>
        </div>
        <div class="user-actions">
          <button class="notification-btn"></button>
          <button class="logout-btn">Logout</button>
        </div>
      </div>
    </header>
    
    <div class="admin-layout">
      <aside class="sidebar">
        <nav class="sidebar-nav">
          <RouterLink 
            v-for="link in sidebarLinks" 
            :key="link.name"
            :to="link.path" 
            class="sidebar-link"
            active-class="sidebar-link-active"
          >
            <span class="link-icon">{{ link.icon }}</span>
            <span class="link-name">{{ link.name }}</span>
          </RouterLink>
        </nav>
      </aside>
      
      <main class="main-content">
        <RouterView />
      </main>
    </div>
    
    <footer class="admin-footer">
      <div class="footer-content">
        <p> 2025 My Broker Cloud Admin Portal</p>
        <div class="footer-links">
          <a href="#">Privacy Policy</a>
          <a href="#">Terms of Service</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.admin-container {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f4f6f9;
}

.admin-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.header-logo h1 {
  margin: 0;
  color: #2c3e50;
  font-size: 1.5rem;
}

.header-user-info {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.user-details {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.user-name {
  font-weight: 600;
  color: #2c3e50;
}

.user-role {
  font-size: 0.8rem;
  color: #7f8c8d;
}

.user-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.notification-btn {
  background: none;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  position: relative;
}

.notification-btn::after {
  content: '3';
  position: absolute;
  top: -5px;
  right: -5px;
  background-color: #e74c3c;
  color: white;
  border-radius: 50%;
  padding: 2px 6px;
  font-size: 0.7rem;
}

.logout-btn {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  cursor: pointer;
}

.admin-layout {
  display: flex;
  flex: 1;
}

.sidebar {
  width: 250px;
  background-color: #2c3e50;
  padding: 2rem 0;
}

.sidebar-nav {
  display: flex;
  flex-direction: column;
}

.sidebar-link {
  display: flex;
  align-items: center;
  padding: 1rem 2rem;
  text-decoration: none;
  color: #bdc3c7;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.sidebar-link:hover {
  background-color: rgba(255,255,255,0.1);
  color: white;
}

.sidebar-link-active {
  background-color: #34495e;
  color: white;
}

.link-icon {
  margin-right: 1rem;
  font-size: 1.2rem;
}

.main-content {
  flex: 1;
  padding: 2rem;
  background-color: #f4f6f9;
  overflow-y: auto;
}

.admin-footer {
  background-color: #2c3e50;
  color: white;
  padding: 1rem 2rem;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-links {
  display: flex;
  gap: 1rem;
}

.footer-links a {
  color: #bdc3c7;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-links a:hover {
  color: white;
}

@media (max-width: 1024px) {
  .admin-layout {
    flex-direction: column;
  }

  .sidebar {
    width: 100%;
    flex-direction: row;
  }

  .sidebar-nav {
    flex-direction: row;
    justify-content: space-around;
  }
}
</style>
