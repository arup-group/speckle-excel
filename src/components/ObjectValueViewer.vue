<template>
  <div class="ml-4 my-2">
    <b>{{ keyName }}</b>
    <code class="ml-4">{{ value }}</code>
  </div>
</template>
<script>
export default {
  name: 'ObjectsValueViewer',
  components: {},
  props: {
    value: {
      type: [Number, String, Boolean],
      default: null
    },
    streamId: {
      type: String,
      default: null
    },
    keyName: {
      type: String,
      default: null
    },
    fullKeyName: {
      type: String,
      default: null
    },
    commitId: {
      type: String,
      default: null
    },
    commitMsg: {
      type: String,
      default: null
    }
  }
}
</script>
