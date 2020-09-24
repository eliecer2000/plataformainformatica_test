<template>
  <v-overlay :value="status">
    <v-progress-circular indeterminate size="100"></v-progress-circular>
  </v-overlay>
</template>
<script>
export default {
  name: 'Overlay',
  props: {
    status: {
      type: [Boolean],
      required: true,
    },
  },
}
</script>
