<template>
  <div>      
    <input placeholder="Enter a label" type="text" v-model="computedLabel" style="margin-bottom: 12px; width: 100%;">      
    <div v-for="(option, idx) in options" style="display: flex; margin-bottom: 8px;" :key="option.key">
      <input type="radio" @input="preventCheck">   
      <input :placeholder="getPlaceholder(idx)" type="text" @input="updateOptionLabel($event, idx)" style="width: 100%;">  
      <button type="button" style="margin-left: 8px; cursor: pointer;" @click="removeOption(option)">X</button> 
    </div>
    <button type="button" style="margin-top: 12px;" @click="addOption">Add option</button>    
  </div>
</template>

<script>
export default {
  name: 'MultipleChoice',
  props: ['label', 'options'],
  data() {
    return {
      // options: [
      //   {
      //     key: Date.now(),
      //     label: ''
      //   }
      // ]
    }
  },
  computed: {
    computedLabel: {
      get() {
        return this.label
      },
      set(val) {
        this.$emit('updateLabel', val)
      }
    }
    // computedOptions: { 
    //   get() {
    //     return this.options.map((option, index) => {
    //       option.key = index
    //       return option
    //     })
    //   },
    //   set(val) {
    //     this.$emit('updateOptions', val)
    //   }         
    // }
  },
  methods: {
    updateOptionLabel(e, idx) {
      this.$emit('updateOptionLabel', {idx: idx, val: e.target.value})
    },
    removeOption(option) {
      const index = this.options.findIndex(e => e.key === option.key)
      this.options.splice(index, 1)
    },
    addOption() {
      this.options.push({
        key: Date.now(),
        content: ''
      })
    },
    getPlaceholder(idx) {
      return `Option ${idx+1}`
    },
    preventCheck(e) {
      e.target.checked = false
    },
    toSnakeCase(string) {
      return string.charAt(0).toLowerCase() + string.slice(1) // lowercase the first character
      .replace(/\W+/g, " ") // Remove all excess white space and replace & , . etc.
      .replace(/([a-z])([A-Z])([a-z])/g, "$1 $2$3") // Put a space at the position of a camelCase -> camel Case
      .split(/\B(?=[A-Z]{2,})/) // Now split the multi-uppercases customerID -> customer,ID
      .join(' ') // And join back with spaces.
      .split(' ') // Split all the spaces again, this time we're fully converted
      .join('_') // And finally snake_case things up
      .toLowerCase() // With a nice lower case
    }
  }
}
</script>

<style>

</style>
