<template>
  <chat-component :faqs="faqs"></chat-component>
</template>

<script>
import ChatComponent from "@/components/Chat-component.vue";

export default {
  name: 'App',
  components: {
    ChatComponent
  },
  data() {
    return {
      faqs: [
        {
          question: 'What is Vue.js?',
          answer: 'Vue.js is a progressive JavaScript framework for building user interfaces.',
          show: false,
        },
        {
          question: 'What is Tailwind CSS?',
          answer: 'Tailwind CSS is a utility-first CSS framework for rapid UI development.',
          show: false,
        },
        {
          question: 'How do I use props in Vue?',
          answer: 'Props are custom attributes you can register on a component. When a value is passed to a prop attribute, it becomes a property on that component instance.',
          show: false,
        },
      ],
    }
  }
}
</script>