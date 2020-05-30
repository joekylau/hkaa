<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <div class="text-justify">
        <v-breadcrumbs :items="items"></v-breadcrumbs>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  computed: {
    items: function() {
      return [
        {
          text: this.$t('Home'),
          to: '/'
        },
        {
          text: this.$t('AboutUs'),
          to: '/about-us'
        },
        {
          text: this.$t('Founder'),
          to: '/about-us/founder'
        }
      ];
    }
  }
}
</script>

<style scoped>

</style>
