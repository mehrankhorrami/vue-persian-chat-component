<template>
  <div class="faq-box w-full flex flex-col gap-1.5">
    <div class="faq-item w-full bg-slate-100 rounded-lg p-3 flex flex-col gap-1.5" v-for="(faq, index) in faqs" :key="index">
      <button class="flex flex-row w-full text-[14px] !font-bold text-right items-center" @click="toggle(index)">
        <span class="w-full">{{ faq.question }}</span>
        <svg
            :class="['transition-all', faq.show ? 'rotate-180' : '']"
            width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M9.96004 4.47498L6.70004 7.73498C6.31504 8.11998 5.68504 8.11998 5.30004 7.73498L2.04004 4.47498"
                stroke="black" stroke-opacity="0.88" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round"
                stroke-linejoin="round"/>
        </svg>
      </button>
      <div v-if="faq.show" class="text-[14px]">
        {{ faq.answer }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FaqBox',
  props: {
    faqs: {
      type: Array,
      required: true,
      default: () => [],
    },
  },
  methods: {
    toggle(index) {
      this.$set(this.faqs, index, {
        ...this.faqs[index],
        show: !this.faqs[index].show,
      });
    },
  },
};
</script>
