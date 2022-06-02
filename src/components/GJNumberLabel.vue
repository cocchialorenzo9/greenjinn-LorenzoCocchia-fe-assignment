<template>
<!-- component that layouts the provided number and displays the description for each of those -->
<div class="gj-number-label">
  <div class="gj-number-label__number">
    <slot name="number">
      <span class="gj-number-label__number-value">{{ number }}</span>
    </slot>
  </div>
  <div class="gj-number-label__description">
    <slot name="description">
      <span class="gj-number-label__description-value">{{ description }}</span>
    </slot>
  </div>
</div>
</template>

<script>
export default {
  name: "GJNumberLabel",
  props: {
      number: {
        type: Number,
        required: true
      },
      description: {
        type: String,
        required: true
      }
  }
}
</script>

<style scoped>

</style>