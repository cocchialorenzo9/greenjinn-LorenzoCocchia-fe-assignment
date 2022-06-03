<template>
<!-- component that takes the title and a list of number-description couples and
shows them through GJNumbersView-->
<div class="gj-numbers-view">
  <h1>{{ title }}</h1>
  <div class="gj-numbers-view__list">
    <!-- for each element in GJList, create a GJNumbersView component -->
    <GJNumberLabel v-for="(number, description) in gjList"
                   :key="number"
                   :number="number"
                   :description="description">
    </GJNumberLabel>
  </div>
</div>
</template>

<script>
import GJNumberLabel from './GJNumberLabel.vue'

export default {
  name: "GJNumbersView",
  components: {
    GJNumberLabel
  },
  props: {
    title: {
      type: String,
      required: true
    },
    gjList: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>

</style>