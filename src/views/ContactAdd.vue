<template>
  <div class="page">
    <h4>Thêm mới Liên hệ</h4>
    <ContactForm :contact="empty" @submit:contact="save" />
    <p>{{ message }}</p>
  </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      empty: { name: "", email: "", phone: "", address: "" },
      message: "",
    };
  },
  methods: {
    async save(data) {
      try {
        await ContactService.create(data);
        this.message = "Thêm thành công!";
        setTimeout(() => this.$router.push({ name: "contactbook" }), 800);
      } catch (e) {
        this.message = "Lỗi!";
      }
    },
  },
};
</script>
