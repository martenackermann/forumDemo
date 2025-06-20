<template>
  <div class="forum-layout">
    <header class="navbar">
      <div class="container">
        <h1 class="navbar-brand">Forum</h1>
        <nav>
          <ul class="nav-links">
            <li><NuxtLink to="/">Home</NuxtLink></li>
            <li><NuxtLink to="/about">About</NuxtLink></li>
            <li><NuxtLink to="/contact">Contact</NuxtLink></li>
          </ul>
        </nav>
      </div>
    </header>
    
    <main class="container">
      <slot />
    </main>
    
    <footer class="footer">
      <div class="container">
        <p>&copy; 2023 Forum. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.forum-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}

.navbar {
  background-color: #333;
  color: white;
  padding: 1rem 0;
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar-brand {
  font-size: 1.5rem;
  margin: 0;
}

.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links li {
  margin-left: 1.5rem;
}

.nav-links a {
  color: white;
  text-decoration: none;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: #ddd;
}

main {
  flex: 1;
  padding: 2rem 0;
}

.footer {
  background-color: #f5f5f5;
  padding: 1rem 0;
  text-align: center;
}
</style>