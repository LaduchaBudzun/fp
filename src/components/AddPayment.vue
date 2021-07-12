<template>
  <div>
    <button class="add_new" @click="addNew">{{ button }}</button>
    <div v-if="form">
      <input v-model="date" placeholder="date" />
      <input v-model.trim="category" placeholder="category" />
      <input v-model="value" type="number" placeholder="value" />
      <button @click="onClick">Add Data</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddPayment",
  data() {
    return {
      date: "",
      category: "",
      value: null,
      form: false,
      button: "ADD NEW COST +",
    };
  },
  methods: {
    addNew() {
      if (this.form == false) {
        this.form = true;
        this.button = "HIDE";
      } else if (this.form == true) {
        this.form = false;
        this.button = "ADD NEW COST +";
      }
    },
    onClick() {
      const { category, value } = this;
      const data = {
        date: this.date || this.getCurrentDate,
        category,
        value,
      };
      console.log("add", data);
      this.$emit("addNewPayment", data); //событие отправляет в App.vue
    },
  },
  computed: {
    getCurrentDate() {
      const today = new Date();
      const d = today.getDate();
      const m = today.getMonth() + 1;
      const y = today.getFullYear();
      return `${d}.${m}.${y}`;
    },
  },
};
</script>

<style>
</style>