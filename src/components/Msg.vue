<template>
  <div class="w-full" :style="self ? 'text-align:right;' : ''">
    <div
      class="bg-gray-300 inline-block px-2 py-2 m-3"
      :style="self ? 'background:#AAFFAA;' : ''"
    >
      {{ text }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Msg",
  props: ["text", "self", "id"],
  
};
</script>

<style></style>
