<template>
  <div>
    <form @submit.prevent="handleSubmit">
        <div class="mb-6">
          <label for="fullName" class="block mb-2 text-sm font-medium text-gray-900">نام و نام خانوادگی</label>
          <input
              type="text"
              id="fullName"
              v-model="fullName"
              placeholder="نام و نام خانوادگی خود را وارد نمایید."
              class="block w-full px-3 py-2 text-gray-900 !border !border-gray-300 rounded-lg text-base focus:!ring-blue-500 focus:!border-blue-500 !outline-none"
          />
          <span class="text-red-600 text-sm" v-if="errors.fullName">{{ errors.fullName }}</span>
        </div>
        <div class="mb-6">
          <label for="mobileNumber" class="block mb-2 text-sm font-medium text-gray-900">شماره همراه</label>
          <input
              type="tel"
              id="mobileNumber"
              v-model="mobileNumber"
              placeholder="09xxxxxxxxx"
              class="block w-full px-3 py-2 text-gray-900 !border !border-gray-300 rounded-lg text-base focus:!ring-blue-500 focus:!border-blue-500 !outline-none"
          />
          <span class="text-red-600 text-sm" v-if="errors.mobileNumber">{{ errors.mobileNumber }}</span>
        </div>
        <div class="mb-6">
          <label for="subject" class="block mb-2 text-sm font-medium text-gray-900">موضوع</label>
          <input
              type="text"
              id="subject"
              v-model="subject"
              placeholder="موضوع پیام خود را وارد نمایید."
              class="block w-full px-3 py-2 text-gray-900 !border !border-gray-300 rounded-lg text-base focus:!ring-blue-500 focus:!border-blue-500 !outline-none"
          />
          <span class="text-red-600 text-sm" v-if="errors.subject">{{ errors.subject }}</span>
        </div>
        <div class="mb-6">
          <label for="message" class="block mb-2 text-sm font-medium text-gray-900">پیام</label>
          <textarea
              id="message"
              v-model="message"
              placeholder="لطفا پیام خود را با دقت وارد نمایید."
              class="block w-full px-3 py-2 text-gray-900 !border !border-gray-300 rounded-lg text-base focus:!ring-blue-500 focus:!border-blue-500 !outline-none"
          />
          <span class="text-red-600 text-sm" v-if="errors.message">{{ errors.message }}</span>
        </div>
      <button
          type="submit"
          class="block w-full text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 text-center me-2 mb-2"
      >ارسال
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "formComponent",
  data() {
    return {
      fullName: '',
      mobileNumber: '',
      subject: '',
      message: '',
      errors: {}
    }
  },
  methods: {
    handleSubmit() {
      this.errors = this.validateForm()
      if (Object.keys(this.errors).length === 0) {
        const formData = {
          fullName: this.fullName,
          mobileNumber: this.mobileNumber,
          subject: this.subject,
          message: this.message
        }
        this.$emit('submitted', formData);
        this.clearForm()
      }
    },
    validateForm() {
      const errors = {}
      if (!this.fullName) {
        errors.fullName = 'نام و نام خانوادگی اجباری است.'
      }
      if (!this.mobileNumber) {
        errors.mobileNumber = 'شماره همراه اجباری است.'
      } else if (!/^09\d{9}$/.test(this.mobileNumber)) {
        errors.mobileNumber = 'شماره همراه معتبر نمی باشد.'
      }
      if (!this.subject) {
        errors.subject = 'موضوع اجباری است.'
      }
      if (!this.message) {
        errors.message = 'پیام اجباری است.'
      }
      return errors;
    },
    clearForm() {
      this.fullName = ''
      this.mobileNumber = ''
      this.subject = ''
      this.message = ''
    }
  }
}
</script>