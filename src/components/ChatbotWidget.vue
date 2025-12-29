<template>
  <div class="chatbot-widget" :class="{ 'is-open': isOpen }">
    <button @click="toggleChat" class="chatbot-toggle-button">
      {{ isOpen ? 'Close Chat' : 'Open Chat' }}
    </button>
    <div v-if="isOpen" class="chatbot-content">
      <h3>Job Portal FAQ</h3>
      <div class="faq-list">
        <div v-for="(faq, index) in filteredFaqs" :key="index" class="faq-item">
          <p @click="toggleAnswer(index)" class="question">{{ faq.question }}</p>
          <p v-if="faq.showAnswer" class="answer">{{ faq.answer }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ChatbotWidget',
  data() {
    return {
      isOpen: false,
      faqs: [
        {
          question: 'How do I apply for a job?',
          answer: 'You can apply for a job by clicking on the \'Apply Now\' button on the job listing page.',
          showAnswer: false,
        },
        {
          question: 'How can I post a new job?',
          answer: 'To post a new job, navigate to the \'Add Job\' section and fill out the required details.',
          showAnswer: false,
        },
        {
          question: 'Is there a fee to apply?',
          answer: 'No, applying for jobs through our portal is completely free.',
          showAnswer: false,
        },
        {
          question: 'How do I contact support?',
          answer: 'You can reach our support team via the contact form on our website.',
          showAnswer: false,
        },
      ],
    };
  },
  computed: {
    filteredFaqs() {
      return this.faqs;
    },
  },
  methods: {
    toggleChat() {
      this.isOpen = !this.isOpen;
    },
    toggleAnswer(index) {
      this.faqs[index].showAnswer = !this.faqs[index].showAnswer;
    },
  },
};
</script>

<style scoped>
.chatbot-widget {
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 1000;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  width: 300px;
  max-height: 400px;
  display: flex;
  flex-direction: column;
  transition: all 0.3s ease-in-out;
}

.chatbot-widget.is-open {
  height: auto;
}

.chatbot-toggle-button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 8px;
  cursor: pointer;
  align-self: flex-end;
  margin: 10px;
}

.chatbot-content {
  padding: 10px;
  overflow-y: auto;
  flex-grow: 1;
}

.chatbot-content h3 {
  margin-top: 0;
  color: #333;
}

.faq-item {
  margin-bottom: 10px;
  border-bottom: 1px solid #eee;
  padding-bottom: 8px;
}

.faq-item .question {
  font-weight: bold;
  cursor: pointer;
  color: #0056b3;
}

.faq-item .answer {
  margin-top: 5px;
  padding-left: 10px;
  border-left: 3px solid #007bff;
  color: #555;
}
</style>
