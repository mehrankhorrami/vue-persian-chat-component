<template>
  <div
      class="pchat-wrapper fixed left-[20px] right-[20px] bottom-[20px] md:left-[40px] md:right-auto md:bottom-[40px] flex flex-col gap-4 items-end z-[999]">
    <div
        v-if="isOpen"
        class="pchat-body bg-white border-[#E2E8F0] border-8 rounded-2xl rounded-bl-none w-full h-full md:w-[420px] md:h-[65vh] py-6 px-3 flex flex-col gap-6 shadow-xl"
    >
      <div class="pchat-body-header flex flex-row items-center justify-center gap-4 px-3">
        <svg v-if="isSendTicketEnabled && faqs.length > 0" @click="toggleIsSendTicketEnabled" class="cursor-pointer"
             width="24" height="24"
             viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M14.4299 5.92999L20.4999 12L14.4299 18.07" stroke="#111827" stroke-width="1.5" stroke-miterlimit="10"
                stroke-linecap="round" stroke-linejoin="round"/>
          <path d="M3.5 12H20.33" stroke="#111827" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round"
                stroke-linejoin="round"/>
        </svg>
        <span v-if="!isSendTicketEnabled && faqs.length > 0" class="w-full font-bold text-[20px]">پشتیبان</span>
        <span v-else class="w-full font-bold text-[20px]">ارسال پیام برای پشتیبان</span>
        <svg @click="toggleIsOpen" class="cursor-pointer" width="30" height="30" viewBox="0 0 30 30" fill="none"
             xmlns="http://www.w3.org/2000/svg">
          <path d="M10 20L20.0001 9.99988" stroke="#111827" stroke-width="1.5" stroke-linecap="round"
                stroke-linejoin="round"/>
          <path d="M20.0001 20L10 9.99988" stroke="#111827" stroke-width="1.5" stroke-linecap="round"
                stroke-linejoin="round"/>
        </svg>
      </div>

      <div v-if="!isSendTicketEnabled && faqs.length > 0"
           class="flex flex-col gap-6 overflow-x-hidden overflow-y-auto pchat-custom-scroll px-3 h-full">
        <p>در اینجا می توانید تعدادی از پرسش های متداول را ببینید یا در صورت تمایل برای ما پیام ارسال کنید.</p>
        <div>
          <faq-box :faqs="faqs"/>
        </div>
        <div class="flex flex-col gap-3 justify-center items-center">
          <p class="">جواب سوالتان را پیدا نکردید؟</p>
          <button
              class="bg-blue-600 hover:bg-blue-700 rounded-lg text-white px-4 py-2 max-w-[200px]"
              @click="toggleIsSendTicketEnabled"
          >ارسال پیام برای
            پشتیبان
          </button>
        </div>
      </div>
      <div v-else class="flex flex-col gap-6 px-3 overflow-x-hidden overflow-y-auto pchat-custom-scroll">
        <form-component @submitted="handleSubmitted"/>
      </div>

    </div>

    <div
        v-if="isHelpDialogOpen && !isOpen"
        class="pchat-notif fixed left-[20px] right-[20px] bottom-[80px] md:left-[40px] md:right-auto md:bottom-[120px] flex flex-col gap-2 items-end z-[999] bg-gray-100 rounded-lg w-full md:w-[300px]"
        style="padding: 8px;"
    >
      <p class="w-full font-bold text-[16px] flex flex-row text-right">
        <span class="w-full">پشتیبانی</span>
        <svg @click="closeHelpDialogHandle" width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg" class="cursor-pointer"><path d="M10 20L20.0001 9.99988" stroke="#111827" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M20.0001 20L10 9.99988" stroke="#111827" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path></svg>
      </p>
      <p class="text-right w-full">اگر سوالی دارید برای ما پیام ارسال کنید.</p>
    </div>

    <button
        class="pchat-btn w-[60px] h-[60px] bg-[#172554] rounded-full flex items-center justify-center shadow-xl"
        @click="toggleIsOpen"
    >
      <svg v-if="!isOpen" width="36" height="36" viewBox="0 0 36 36" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path
            d="M25.5 3H10.5C6.36 3 3 6.345 3 10.47V19.44V20.94C3 25.065 6.36 28.41 10.5 28.41H12.75C13.155 28.41 13.695 28.68 13.95 29.01L16.2 31.995C17.19 33.315 18.81 33.315 19.8 31.995L22.05 29.01C22.335 28.635 22.785 28.41 23.25 28.41H25.5C29.64 28.41 33 25.065 33 20.94V10.47C33 6.345 29.64 3 25.5 3ZM19.5 20.625H10.5C9.885 20.625 9.375 20.115 9.375 19.5C9.375 18.885 9.885 18.375 10.5 18.375H19.5C20.115 18.375 20.625 18.885 20.625 19.5C20.625 20.115 20.115 20.625 19.5 20.625ZM25.5 13.125H10.5C9.885 13.125 9.375 12.615 9.375 12C9.375 11.385 9.885 10.875 10.5 10.875H25.5C26.115 10.875 26.625 11.385 26.625 12C26.625 12.615 26.115 13.125 25.5 13.125Z"
            fill="white"/>
      </svg>
      <svg v-else width="36" height="36" viewBox="0 0 36 36" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M12 24L24.0001 11.9999" stroke="white" stroke-width="1.5" stroke-linecap="round"
              stroke-linejoin="round"/>
        <path d="M24.0001 24L12 11.9999" stroke="white" stroke-width="1.5" stroke-linecap="round"
              stroke-linejoin="round"/>
      </svg>
    </button>
  </div>
</template>

<script>
import FaqBox from "@/components/FAQ-box-component.vue";
import FormComponent from "@/components/Form-component.vue";

export default {
  name: 'chatComponent',
  components: {FormComponent, FaqBox},
  props: {
    faqs: {
      type: Array,
      required: true,
      default: () => [],
    },
  },
  data() {
    return {
      isOpen: false,
      isHelpDialogOpen: localStorage.getItem('isHelpDialogOpen') !== 'false',
      isSendTicketEnabled: false
    }
  },
  methods: {
    toggleIsOpen() {
      this.isOpen = !this.isOpen;
      this.isHelpDialogOpen = false;
      localStorage.setItem('isHelpDialogOpen', 'false');
      this.isSendTicketEnabled = false;
    },
    closeHelpDialogHandle() {
      this.isHelpDialogOpen = false;
      localStorage.setItem('isHelpDialogOpen', 'false');
    },
    toggleIsSendTicketEnabled() {
      this.isSendTicketEnabled = !this.isSendTicketEnabled;
    },
    handleSubmitted(formData) {
      console.log(formData);
      this.$emit('submitted', formData);
    }
  }
}

</script>