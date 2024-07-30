# Persian Chat Component
A Persian chat component using Vue and Tailwind.

![Example Image](https://github.com/mehrankhorrami/vue-persian-chat-component/blob/master/chat-component-demo.png)

## Project setup
```
npm i vue-persian-chat-component
```

## Usage
main.js
```
import Vue from 'vue';
import App from './App.vue';
import Chat from 'vue-persian-chat-component';
import 'vue-persian-chat-component/dist/ChatComponent.css';

Vue.config.productionTip = false;

Vue.component('ChatComponent', Chat);

new Vue({
  render: h => h(App),
}).$mount('#app')
```
App.vue
```
<template>
  <ChatComponent :faqs="faqs" @submitted="onChatFormSubmitted"/>
</template>

<script>
    export default {
      name: 'App',
    
      data: () => ({
        faqs: [
          {
            question: 'چطور ثبت نام کنم؟',
            answer: 'پاسخ سوال خود را اینجا قرار دهید.',
            show: false,
          },
          {
            question: 'چطور میتوانم کالاهای خود را ثبت کنم؟',
            answer: 'پاسخ سوال خود را اینجا قرار دهید.',
            show: false,
          },
          {
            question: 'آیا خدمات مربوط به ثبت و انتشار کالا رایگان است؟',
            answer: 'پاسخ سوال خود را اینجا قرار دهید.',
            show: false,
          },
          {
            question: 'چطور از کد تخفیف استفاده کنیم؟',
            answer: 'پاسخ سوال خود را اینجا قرار دهید.',
            show: false,
          },
          {
            question: 'چطور میتوانم با پشتیبانی تماس بگیرم؟',
            answer: 'پاسخ سوال خود را اینجا قرار دهید.',
            show: false,
          },
        ],
      }),

      methods: {
        onChatFormSubmitted(formData) {
          console.log(formData);
        }
      }
    };
</script>
```
