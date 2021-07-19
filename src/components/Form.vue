<template>
  <div>
    <form @submit.prevent class="form-box">
      <input type="text" name="city" v-model="city" class="input" />
      <button @click="search">submit</button>
    </form>

    <Toast v-if="toast.show" :type="toast.type" :message="toast.message" />
  </div>
</template>

<script>
import Toast from "./Toast.vue";
export default {
  components: { Toast },
  name: "Form",
  data() {
    return {
      city: "",
      toast: {
        show: false,
        type: "",
        message: "",
      },
    };
  },
  methods: {
    search() {
      if (this.city === "") {
        this.toast = {
          show: true,
          type: "error",
          message: "Please enter a city.",
        };

        setTimeout(() => {
          this.toast = {
            show: false,
          };
        }, 5000);
        return;
      }
      this.$emit("search", this.city);
    },
  },
};
</script>

<style>
.form-box {
  width: 400px;
  height: auto;
  margin: 50px auto;
  padding: 5px;
}
.input {
  width: 100%;
  box-sizing: border-box;
  outline: none;
  margin-bottom: 10px;
  padding: 15px 20px;
  border-radius: 2px;
  border: none;
}
</style>