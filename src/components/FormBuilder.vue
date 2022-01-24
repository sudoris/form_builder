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
              @updateOptionLabel="field.options[$event.idx].label = $event.val"
              @removeOption="field.options.splice(index, 1)">
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
    updateOptionLabel(payload) {
      console.log(payload)
    },
    updateLabel(value, index) {
      
    },
    generatePreview() {
      const schema = this.generateSchema()
    },
    generateSchema() {
      const schema = {}
      
      for (const field of fields) {
        if (!schema.properties) {
          schema.properties = {}
        }

        if (field.label) {
          const key = this.toSnakeCase(field.label)
          schema.properties[key] = {}
          schema.properties[key].dataType = this.getDataType(field.fieldType)
          schema.properties[key].fieldType = field.fieldType
          
          // if (field.fieldType )
        }

      }
    },
    getDataType(fieldType) {
      const dataTypeMap = {
        ShortText: 'string',
        MultipleChoice: 'string'
      }
      return dataTypeMap[fieldType]
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
    },
    addField() {
      this.fields.push({ 
        key: Date.now(), 
        fieldType: 'ShortText', 
        label: '', 
        options: [
          {
            key: Date.now(),
            label: ''
          }
        ]
      })
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
