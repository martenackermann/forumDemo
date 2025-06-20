<template>
  <div v-if="thread" class="thread-detail">
    <div class="thread-header">
      <h1>{{ thread.title }}</h1>
      <div class="thread-meta">
        <span class="thread-author">Posted by {{ thread.author }}</span>
        <span class="thread-date">{{ thread.date }}</span>
      </div>
    </div>
    
    <div class="thread-content">
      <p>{{ thread.content }}</p>
    </div>
    
    <div class="thread-replies">
      <h2>Replies ({{ thread.replies.length }})</h2>
      
      <div v-if="thread.replies.length === 0" class="no-replies">
        No replies yet. Be the first to reply!
      </div>
      
      <div v-else class="reply-list">
        <div v-for="(reply, index) in thread.replies" :key="index" class="reply-card">
          <div class="reply-header">
            <span class="reply-author">{{ reply.author }}</span>
            <span class="reply-date">{{ reply.date }}</span>
          </div>
          <div class="reply-content">
            <p>{{ reply.content }}</p>
          </div>
        </div>
      </div>
    </div>
    
    <div class="reply-form">
      <h3>Add a Reply</h3>
      <div class="form-group">
        <label for="author">Your Name</label>
        <input type="text" id="author" v-model="newReply.author" placeholder="Enter your name">
      </div>
      <div class="form-group">
        <label for="content">Your Reply</label>
        <textarea id="content" v-model="newReply.content" rows="4" placeholder="Write your reply here"></textarea>
      </div>
      <button @click="addReply" class="submit-button">Post Reply</button>
    </div>
    
    <div class="back-link">
      <NuxtLink to="/">← Back to Thread List</NuxtLink>
    </div>
  </div>
  
  <div v-else class="thread-not-found">
    <h1>Thread Not Found</h1>
    <p>The thread you're looking for doesn't exist or has been removed.</p>
    <NuxtLink to="/">← Back to Thread List</NuxtLink>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const threadId = parseInt(route.params.id);

// Sample thread data with replies
const threadsData = [
  {
    id: 1,
    title: "Welcome to our new forum!",
    author: "Admin",
    date: "June 20, 2023",
    content: "Hello everyone! Welcome to our brand new forum. This is a place where we can discuss various topics, share ideas, and help each other out. Feel free to introduce yourself and let us know what you're interested in. We're excited to build this community together!",
    replies: [
      {
        author: "John",
        date: "June 20, 2023",
        content: "Thanks for creating this forum! I'm excited to be part of this community."
      },
      {
        author: "Sarah",
        date: "June 21, 2023",
        content: "Hello everyone! I'm Sarah and I'm looking forward to the discussions here."
      },
      {
        author: "Mike",
        date: "June 21, 2023",
        content: "Great to see a new forum. I hope we can have some interesting conversations."
      },
      {
        author: "Lisa",
        date: "June 22, 2023",
        content: "Hi all! Just wanted to say hello and introduce myself."
      },
      {
        author: "David",
        date: "June 22, 2023",
        content: "Looking forward to connecting with everyone here!"
      }
    ]
  },
  {
    id: 2,
    title: "Tips for new forum members",
    author: "Moderator",
    date: "June 21, 2023",
    content: "Welcome to all our new members! Here are some helpful tips to get the most out of our forum:\n\n1. Complete your profile with a picture and brief bio\n2. Read the forum rules before posting\n3. Use the search function to find existing discussions\n4. Be respectful and constructive in your comments\n5. Report any inappropriate content to moderators\n\nHappy posting!",
    replies: [
      {
        author: "Emma",
        date: "June 21, 2023",
        content: "These are great tips! Thanks for sharing."
      },
      {
        author: "Tom",
        date: "June 22, 2023",
        content: "I'm new here. Thanks for the helpful advice!"
      },
      {
        author: "Alex",
        date: "June 23, 2023",
        content: "Point #4 is especially important. Respectful communication is key."
      }
    ]
  },
  {
    id: 3,
    title: "Feature requests and suggestions",
    author: "Developer",
    date: "June 22, 2023",
    content: "We're constantly working to improve our forum and would love to hear your suggestions! What features would you like to see added? What changes would make your experience better? Please share your ideas in this thread, and we'll consider them for future updates.",
    replies: [
      {
        author: "Rachel",
        date: "June 22, 2023",
        content: "It would be great to have a dark mode option!"
      },
      {
        author: "Chris",
        date: "June 23, 2023",
        content: "I'd love to see more customization options for user profiles."
      },
      {
        author: "Jessica",
        date: "June 23, 2023",
        content: "Could we get a mobile app version of the forum?"
      },
      {
        author: "Daniel",
        date: "June 24, 2023",
        content: "It would be helpful to have a way to bookmark threads for later reading."
      },
      {
        author: "Sophia",
        date: "June 24, 2023",
        content: "I think adding reaction emojis to posts would be a nice feature."
      },
      {
        author: "Ryan",
        date: "June 25, 2023",
        content: "Would love to see better notification options for thread updates."
      },
      {
        author: "Olivia",
        date: "June 25, 2023",
        content: "A way to categorize threads by topics would be really useful."
      },
      {
        author: "James",
        date: "June 26, 2023",
        content: "How about adding a reputation system for helpful users?"
      }
    ]
  }
];

// Find the current thread based on the ID from the route
const thread = computed(() => {
  return threadsData.find(t => t.id === threadId) || null;
});

// New reply form data
const newReply = ref({
  author: '',
  content: '',
  date: ''
});

// Function to add a new reply
const addReply = () => {
  if (!newReply.value.author || !newReply.value.content) {
    alert('Please fill in all fields');
    return;
  }
  
  // Format current date
  const today = new Date();
  const month = today.toLocaleString('default', { month: 'long' });
  const day = today.getDate();
  const year = today.getFullYear();
  
  // Add the reply to the thread
  thread.value.replies.push({
    author: newReply.value.author,
    date: `${month} ${day}, ${year}`,
    content: newReply.value.content
  });
  
  // Clear the form
  newReply.value.author = '';
  newReply.value.content = '';
  
  // Show confirmation
  alert('Your reply has been posted!');
};
</script>

<style scoped>
.thread-detail {
  max-width: 800px;
  margin: 0 auto;
}

.thread-header {
  margin-bottom: 2rem;
  border-bottom: 1px solid #e0e0e0;
  padding-bottom: 1rem;
}

.thread-meta {
  display: flex;
  font-size: 0.875rem;
  color: #888;
  margin-top: 0.5rem;
}

.thread-author {
  margin-right: 1rem;
}

.thread-content {
  margin-bottom: 3rem;
  line-height: 1.7;
}

.thread-content p {
  margin-bottom: 1rem;
}

.thread-replies {
  margin-bottom: 3rem;
}

.reply-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-top: 1.5rem;
}

.reply-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 1.5rem;
  background-color: #f9f9f9;
}

.reply-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.75rem;
  font-size: 0.875rem;
}

.reply-author {
  font-weight: 600;
  color: #333;
}

.reply-date {
  color: #888;
}

.reply-content {
  line-height: 1.6;
}

.reply-form {
  background-color: #f5f5f5;
  padding: 1.5rem;
  border-radius: 8px;
  margin-bottom: 2rem;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-family: inherit;
  font-size: 1rem;
}

.submit-button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

.submit-button:hover {
  background-color: #2980b9;
}

.back-link {
  margin-top: 2rem;
}

.no-replies {
  padding: 1.5rem;
  background-color: #f9f9f9;
  border-radius: 8px;
  text-align: center;
  color: #888;
}

.thread-not-found {
  text-align: center;
  padding: 3rem 0;
}
</style>