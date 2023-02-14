<template>
  <div class="donates-container__donates">
    <div class="donate-item" v-for="donate in donates" :key="donate.id">
      {{ donate.date }} <b>${{ donate.amount }}</b>
    </div>
  </div>
</template>

<script>
export default {
  name: "DonatesView",
  props: {
    donates: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style></style>
