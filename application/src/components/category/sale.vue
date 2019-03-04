<template>
  <b-container fluid>
    <b-row class="my-1">
      <b-col cols="1"></b-col>
      <b-col>
        
      </b-col>
      <b-col></b-col>
      <b-col cols="1"></b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: "sale",
  data() {
    return {
      id: this.$route.params.id
    };
  },

  mounted() {
    console.log(this.id)
  },

  methods: {}
};
</script>

<style scoped>

</style>


