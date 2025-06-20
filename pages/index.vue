<template>
  <div>
    <h1>Forum Threads</h1>
    
    <div class="thread-list">
      <div v-for="thread in threads" :key="thread.id" class="thread-card">
        <NuxtLink :to="`/thread/${thread.id}`" class="thread-link">
          <h2 class="thread-title">{{ thread.title }}</h2>
          <p class="thread-excerpt">{{ thread.excerpt }}</p>
          <div class="thread-meta">
            <span class="thread-author">Posted by {{ thread.author }}</span>
            <span class="thread-date">{{ thread.date }}</span>
            <span class="thread-replies">{{ thread.replies }} replies</span>
          </div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
// Sample thread data
const threads = [
  {
    id: 1,
    title: "Welcome to our new forum!",
    excerpt: "This is the first thread in our forum. Feel free to introduce yourself and share your thoughts.",
    author: "Admin",
    date: "June 20, 2023",
    replies: 5
  },
  {
    id: 2,
    title: "Tips for new forum members",
    excerpt: "Here are some helpful tips for navigating and participating in our forum community.",
    author: "Moderator",
    date: "June 21, 2023",
    replies: 3
  },
  {
    id: 3,
    title: "Feature requests and suggestions",
    excerpt: "Share your ideas for improving our forum and what features you'd like to see added.",
    author: "Developer",
    date: "June 22, 2023",
    replies: 8
  }
];
</script>

<style scoped>
.thread-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-top: 2rem;
}

.thread-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.2s, box-shadow 0.2s;
}

.thread-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.thread-link {
  display: block;
  padding: 1.5rem;
  color: inherit;
  text-decoration: none;
}

.thread-link:hover {
  text-decoration: none;
}

.thread-title {
  margin-top: 0;
  margin-bottom: 0.5rem;
  color: #333;
}

.thread-excerpt {
  margin-bottom: 1rem;
  color: #666;
}

.thread-meta {
  display: flex;
  font-size: 0.875rem;
  color: #888;
}

.thread-author {
  margin-right: 1rem;
}

.thread-date {
  margin-right: 1rem;
}

.thread-replies {
  font-weight: 500;
}
</style>