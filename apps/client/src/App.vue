<script setup>
import { ref } from 'vue'
import { RouterView } from 'vue-router'

const appTitle = ref('My Broker Cloud - Client Portal')
const navigationLinks = ref([
  { name: 'Home', path: '/' },
  { name: 'Properties', path: '/properties' },
  { name: 'Dashboard', path: '/dashboard' },
  { name: 'Profile', path: '/profile' }
])
</script>

<template>
  <div class="app-container">
    <header class="app-header">
      <div class="logo-container">
        <h1>{{ appTitle }}</h1>
      </div>
      <nav class="main-navigation">
        <RouterLink 
          v-for="link in navigationLinks" 
          :key="link.name"
          :to="link.path" 
          class="nav-link"
          active-class="nav-link-active"
        >
          {{ link.name }}
        </RouterLink>
      </nav>
      <div class="user-actions">
        <button class="login-btn">Login</button>
        <button class="signup-btn">Sign Up</button>
      </div>
    </header>
    
    <main class="app-content">
      <RouterView />
    </main>
    
    <footer class="app-footer">
      <div class="footer-content">
        <div class="footer-section">
          <h4>My Broker Cloud</h4>
          <p>Your trusted partner in real estate</p>
        </div>
        <div class="footer-section">
          <h4>Quick Links</h4>
          <ul>
            <li>About Us</li>
            <li>Contact</li>
            <li>Terms of Service</li>
          </ul>
        </div>
        <div class="footer-section">
          <h4>Contact</h4>
          <p>Email: support@mybrokercloud.com</p>
          <p>Phone: (555) 123-4567</p>
        </div>
      </div>
      <div class="copyright">
        &copy; 2025 My Broker Cloud. All Rights Reserved.
      </div>
    </footer>
  </div>
</template>

<style scoped>
.app-container {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f4f6f9;
}

.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 5%;
  background-color: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.logo-container h1 {
  margin: 0;
  color: #2c3e50;
  font-size: 1.5rem;
}

.main-navigation {
  display: flex;
  gap: 1.5rem;
}

.nav-link {
  text-decoration: none;
  color: #34495e;
  font-weight: 500;
  transition: color 0.3s ease;
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -5px;
  left: 0;
  background-color: #3498db;
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link-active {
  color: #3498db;
}

.user-actions {
  display: flex;
  gap: 1rem;
}

.login-btn, .signup-btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.login-btn {
  background-color: transparent;
  color: #3498db;
  border: 1px solid #3498db;
}

.signup-btn {
  background-color: #3498db;
  color: white;
}

.app-content {
  flex-grow: 1;
  padding: 2rem 5%;
}

.app-footer {
  background-color: #2c3e50;
  color: white;
  padding: 2rem 5%;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.footer-section {
  flex: 1;
  margin-right: 1rem;
}

.footer-section h4 {
  margin-bottom: 1rem;
  color: #ecf0f1;
}

.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section ul li {
  margin-bottom: 0.5rem;
  color: #bdc3c7;
  cursor: pointer;
}

.copyright {
  text-align: center;
  padding-top: 1rem;
  border-top: 1px solid rgba(255,255,255,0.1);
}

@media (max-width: 768px) {
  .app-header {
    flex-direction: column;
  }

  .main-navigation {
    margin-top: 1rem;
  }

  .footer-content {
    flex-direction: column;
  }
}
</style>
