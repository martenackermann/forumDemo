<template>
  <div class="contact-page">
    <h1>Contact Us</h1>
    
    <div class="contact-content">
      <div class="contact-info">
        <section class="contact-section">
          <h2>Get in Touch</h2>
          <p>
            We'd love to hear from you! Whether you have a question, feedback, or just want to say hello,
            feel free to reach out to us using the contact form or through any of the methods below.
          </p>
        </section>
        
        <section class="contact-section">
          <h2>Contact Information</h2>
          <ul class="contact-list">
            <li>
              <strong>Email:</strong> 
              <a href="mailto:info@forumexample.com">info@forumexample.com</a>
            </li>
            <li>
              <strong>Phone:</strong> +1 (555) 123-4567
            </li>
            <li>
              <strong>Address:</strong> 123 Forum Street, Web City, Internet 12345
            </li>
          </ul>
        </section>
        
        <section class="contact-section">
          <h2>Office Hours</h2>
          <p>
            Our support team is available to assist you during the following hours:
          </p>
          <ul>
            <li>Monday - Friday: 9:00 AM - 6:00 PM (EST)</li>
            <li>Saturday: 10:00 AM - 2:00 PM (EST)</li>
            <li>Sunday: Closed</li>
          </ul>
        </section>
      </div>
      
      <div class="contact-form-container">
        <h2>Send Us a Message</h2>
        <form class="contact-form" @submit.prevent="submitForm">
          <div class="form-group">
            <label for="name">Your Name</label>
            <input type="text" id="name" v-model="form.name" placeholder="Enter your name" required>
          </div>
          
          <div class="form-group">
            <label for="email">Your Email</label>
            <input type="email" id="email" v-model="form.email" placeholder="Enter your email" required>
          </div>
          
          <div class="form-group">
            <label for="subject">Subject</label>
            <input type="text" id="subject" v-model="form.subject" placeholder="Enter subject" required>
          </div>
          
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" v-model="form.message" rows="6" placeholder="Enter your message" required></textarea>
          </div>
          
          <button type="submit" class="submit-button">Send Message</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const form = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
});

const submitForm = () => {
  // In a real application, you would send the form data to a server
  alert('Thank you for your message! We will get back to you soon.');
  
  // Reset form
  form.value = {
    name: '',
    email: '',
    subject: '',
    message: ''
  };
};
</script>

<style scoped>
.contact-page {
  max-width: 1000px;
  margin: 0 auto;
  padding: 2rem 0;
}

h1 {
  margin-bottom: 2rem;
  text-align: center;
  color: #333;
}

.contact-content {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
}

.contact-info {
  flex: 1;
  min-width: 300px;
}

.contact-form-container {
  flex: 1;
  min-width: 300px;
  background-color: #f5f5f5;
  padding: 1.5rem;
  border-radius: 8px;
}

.contact-section {
  margin-bottom: 2rem;
}

h2 {
  color: #3498db;
  margin-bottom: 1rem;
  border-bottom: 1px solid #eee;
  padding-bottom: 0.5rem;
}

p {
  margin-bottom: 1rem;
  line-height: 1.7;
}

ul {
  margin: 1rem 0;
  line-height: 1.7;
  list-style: none;
  padding: 0;
}

.contact-list li {
  margin-bottom: 1rem;
}

.form-group {
  margin-bottom: 1.5rem;
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
  width: 100%;
}

.submit-button:hover {
  background-color: #2980b9;
}

@media (max-width: 768px) {
  .contact-content {
    flex-direction: column;
  }
}
</style>