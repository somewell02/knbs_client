<template>
  <base-layout>
    <h1 class="text-center mt-6 mb-6 text-h4">FAQ</h1>

    <div class="faqs-container">
      <div
        v-for="(item, idx) in items"
        :key="`faq-${item.id}`"
        :class="[
          'faq',
          { 'active': item.isActive }
        ]"
      >
        <h3 class="faq-title">
          {{ item.question }}
        </h3>
        <p class="faq-text">
          {{ item.answer }}
        </p>
        <button class="faq-toggle" @click="item.isActive = !item.isActive">
          <v-icon icon="mdi-chevron-down" size="20"></v-icon>
        </button>
      </div>
    </div>
  </base-layout>
</template>

<script>
import BaseLayout from "@/layouts/BaseLayout.vue";

import {faqs} from "../api";

export default {
  name: "FaqView",
  components: {BaseLayout},

  data: () => ({
    items: []
  }),

  mounted() {
    faqs.getFaqs().then(data => {
      this.items = data.map(item => ({
        ...item,
        isActive: false
      }));
    })
  }
}
</script>

<style scoped>
.faqs-container {
  margin: 0 auto;
  max-width: 800px;
}

.faq {
  background-color: transparent;
  border: 1px solid #9FA4A8;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  overflow: hidden;
  margin: 20px 0;
  transition: 0.3s ease;
}

.faq.active {
  background-color: #fff;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1), 0 3px 6px rgba(0, 0, 0, 0.1);
}

.faq.active::after, .faq.active::before {
  color: #2ecc71;
  content: '\f075';
  font-size: 7rem;
  position: absolute;
  opacity: 0.2;
  top: 20px;
  left: 20px;
  z-index: 0;
}

.faq.active::before {
  color: #3498db;
  top: -10px;
  left: -30px;
  transform: rotateY(180deg);
}

.faq-title {
  margin: 0 35px 0 0;
}

.faq-text {
  display: none;
  margin: 30px 0 0;
}

.faq.active .faq-text {
  display: block;
}

.faq-toggle {
  border: none;
  border-radius: 50%;
  color: black;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  padding: 0;
  position: absolute;
  top: 30px;
  right: 30px;
  height: 30px;
  width: 30px;
}

.faq-toggle:focus {
  outline: none;
}

.faq.active .faq-toggle {
  background-color: #eaeaea;
}
</style>