<template>
  <div>
    <div
      class="toast"
      :class="{ error: type === 'error', success: type === 'success' }"
    >
      {{ message }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Toast",
  props: ["message", "type"],
  data() {
    return {};
  },
};
</script>

<style>
.toast {
  display: inline-block;
  max-width: 250px;
  padding: 10px 20px;
  text-align: center;
  color: white;
  position: absolute;
  top: 10px;
  right: 10px;
  font-weight: bold;
  text-shadow: 0 1px 0 rgba(0, 0, 0, 0.5);
}
.error {
  background-color: rgba(255, 0, 0, 0.3);
  border: 1px solid rgba(255, 0, 0, 0.5);
}
</style>