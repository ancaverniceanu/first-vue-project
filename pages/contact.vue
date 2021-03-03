<template>
  <div>
    <Header />
    <div class="p-10">
      <p>Page created just to test routing</p>
    </div>
  </div>
</template>
<script>
import Header from '../components/Header.vue'
export default {
  name: 'Contact',
  components: {
    Header,
  },
}
</script>
