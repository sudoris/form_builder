<template>
  <div class="shorttext-container">          
    <input id="label" placeholder="Enter a label" type="text" v-model="computedLabel" style="margin-bottom: 12px;">  
    <input type="text" readonly>
  </div>
</template>

<script>
export default {
  name: 'ShortText',
  props: ['label'],  
  data() {
    return {
      
    }
  },
  computed: {
    computedLabel: {
      get() {
        return this.label;
      },
      set(val) {
        this.$emit('updateLabel', val);
      }
    }
  }
}
</script>

<style>
.shorttext-container {
  display: flex;
  flex-direction: column;
}
</style>
