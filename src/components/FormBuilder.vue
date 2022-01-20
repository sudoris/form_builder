<template>
  <div>
    <div class="container">
      <div class="menu">
        <p v-for="field in fields">
          {{field.fieldType}}
        </p>
      </div>
      <div class="fields-container">
        <div class="fields" v-for="(field, index) in fields" :key="field.key">
          <div class="content">
            <component 
              :is="field.fieldType" 
              :label="field.label" @updateLabel="field.label = $event" 
              :options="field.options" 
              @updateOptions="updateOptions($event)">
            </component>
          </div>
          <div class="settings">      
            <select v-model="field.fieldType">
              <option disabled value="">Select a field type</option>
              <option value="ShortText">Short text</option>
              <option value="MultipleChoice">Multiple choice</option>
            </select>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div></div>
      <div>
        <button type="button" class="" @click="addField" style="margin-right: 8px;">Add Field</button>
        <button type="button" class="" @click="generatePreview">Preview Form</button>
      </div>
    </div>    
  </div>  
</template>

<script>
import ShortText from './ShortText.vue'
import MultipleChoice from './MultipleChoice.vue'

export default {
  name: 'FormBuilder',
  components: {
    ShortText,
    MultipleChoice
  },
  data() {
    return {
      schema: {},            
      fields: [
        { 
          key: Date.now(), 
          fieldType: 'ShortText', 
          label: '', 
          options: [
            {
              key: Date.now(),
              label: ''
            }
          ]
        }
      ]
    }
  },
  methods: {
    updateOptions(value) {

    },
    updateLabel(value, index) {
      
    },
    generatePreview() {

    },
    addField() {
      this.fields.push({ key: Date.now(), fieldType: 'ShortText', label: '', options: [] })
    }
  }
}
</script>

<style>
.container {
  width: 100%;
  display: flex;
  padding: 12px;
  justify-content: space-around;
  gap: 4%;
}

.fields-container {
  display: flex;
  flex-direction: column;  
}

.fields {
  display: flex;
  justify-content: space-around;
  width: 100%;
  gap: 4%;
  margin-bottom: 36px;
}

/* .col-1 {
  width: 20%;
}

.col-2 {
  width: 40%;
} */

.footer {
  margin-top: 22px;
  padding: 12px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.settings {}

input[type=text] {
    background: transparent;
    border: none;
    border-bottom: 1px solid #000000;
}
</style>
