<script setup>
import { ref, onMounted } from 'vue'

const heroStats = ref([
  { icon: '🏘️', value: '500+', label: 'Properties Listed' },
  { icon: '🔑', value: '250+', label: 'Successful Sales' },
  { icon: '🌟', value: '4.8', label: 'Customer Rating' }
])

const featuredProperties = ref([
  {
    id: 1,
    name: 'Luxury Waterfront Villa',
    price: '$1,200,000',
    location: 'Miami, FL',
    bedrooms: 4,
    bathrooms: 3,
    area: '3,500 sq ft',
    image: 'https://images.unsplash.com/photo-1570129477492-45c003edd2f5'
  },
  {
    id: 2,
    name: 'Modern Downtown Loft',
    price: '$650,000',
    location: 'New York, NY',
    bedrooms: 2,
    bathrooms: 2,
    area: '1,800 sq ft',
    image: 'https://images.unsplash.com/photo-1600047509358-9dc75507daeb'
  },
  {
    id: 3,
    name: 'Suburban Family Home',
    price: '$450,000',
    location: 'Austin, TX',
    bedrooms: 3,
    bathrooms: 2,
    area: '2,200 sq ft',
    image: 'https://images.unsplash.com/photo-1605276374104-dee2a0ed3cd6'
  }
])

const searchQuery = ref('')
const handleSearch = () => {
  // Implement search logic
  console.log('Searching for:', searchQuery.value)
}
</script>

<template>
  <div class="home-container">
    <section class="hero-section">
      <div class="hero-content">
        <h1>Discover Your Perfect Home</h1>
        <p>Find, Buy, and Sell Real Estate with Confidence</p>
        
        <div class="search-container">
          <input 
            v-model="searchQuery" 
            type="text" 
            placeholder="Search by city, neighborhood, or property type"
            class="search-input"
          >
          <button @click="handleSearch" class="search-button">
            Search Properties
          </button>
        </div>

        <div class="hero-stats">
          <div v-for="stat in heroStats" :key="stat.label" class="stat-item">
            <span class="stat-icon">{{ stat.icon }}</span>
            <div class="stat-details">
              <h3>{{ stat.value }}</h3>
              <p>{{ stat.label }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="featured-properties">
      <h2>Featured Properties</h2>
      <div class="properties-grid">
        <div v-for="property in featuredProperties" :key="property.id" class="property-card">
          <div class="property-image" :style="{ backgroundImage: `url(${property.image})` }">
            <span class="property-price">{{ property.price }}</span>
          </div>
          <div class="property-details">
            <h3>{{ property.name }}</h3>
            <p class="property-location">{{ property.location }}</p>
            <div class="property-specs">
              <span>🛏️ {{ property.bedrooms }} Beds</span>
              <span>🚿 {{ property.bathrooms }} Baths</span>
              <span>📏 {{ property.area }}</span>
            </div>
            <button class="view-details-btn">View Details</button>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.home-container {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  color: #333;
}

.hero-section {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 4rem 2rem;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.hero-content {
  max-width: 800px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
}

.hero-section h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
  font-weight: 800;
}

.search-container {
  display: flex;
  max-width: 600px;
  margin: 2rem auto;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
}

.search-input {
  flex-grow: 1;
  padding: 1rem;
  border: none;
  font-size: 1rem;
}

.search-button {
  background-color: #4a90e2;
  color: white;
  border: none;
  padding: 1rem 2rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.search-button:hover {
  background-color: #357abd;
}

.hero-stats {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 2rem;
}

.stat-item {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.stat-icon {
  font-size: 2rem;
}

.stat-details h3 {
  margin: 0;
  font-size: 1.5rem;
}

.stat-details p {
  margin: 0;
  color: rgba(255,255,255,0.8);
}

.featured-properties {
  padding: 4rem 2rem;
  background-color: #f4f6f9;
}

.featured-properties h2 {
  text-align: center;
  margin-bottom: 2rem;
  color: #333;
}

.properties-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.property-card {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
}

.property-card:hover {
  transform: translateY(-10px);
}

.property-image {
  height: 250px;
  background-size: cover;
  background-position: center;
  position: relative;
}

.property-price {
  position: absolute;
  top: 1rem;
  left: 1rem;
  background: rgba(0,0,0,0.7);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 5px;
}

.property-details {
  padding: 1.5rem;
}

.property-details h3 {
  margin: 0 0 0.5rem 0;
}

.property-location {
  color: #666;
  margin-bottom: 1rem;
}

.property-specs {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
  color: #666;
}

.view-details-btn {
  width: 100%;
  padding: 1rem;
  background-color: #4a90e2;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.view-details-btn:hover {
  background-color: #357abd;
}

@media (max-width: 1024px) {
  .properties-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .properties-grid {
    grid-template-columns: 1fr;
  }

  .hero-stats {
    flex-direction: column;
    align-items: center;
  }
}
</style>
