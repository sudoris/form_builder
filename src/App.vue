<template>
  <div id="app">
    <FormBuilder v-if="true" />
    <Fractal v-if="false" v-model="formData" :schema="schema" />
  </div>
</template>

<script>
import FormBuilder from './components/FormBuilder.vue'
import Fractal from 'fractal'

const sampleSchema = {  
  title: 'My Form',    
  properties: {
    name: {
      title: 'Name',
      dataType: 'string',
      fieldType: 'text',    
    },
    favoriteFood: {
      title: 'Favorite Food',
      dataType: 'string',
      fieldType: 'text'
    },
    favoriteCountry: {
      title: 'Favorite Country',
      dataType: 'string',
      fieldType: 'select',
      options: ['USA', 'Canada', 'Germany', 'Japan', 'Taiwan'],
      placeholder: 'Choose favorite country'
    },
    // comment: {
    //   title: 'Comment',
    //   dataType: 'string',
    //   fieldType: 'textarea'
    // },
    allergies: {
      title: "Allergies",
      dataType: 'array',
      fieldType: 'checkbox',
      items: [{label: 'Seafood', value: 'seafood'}, {label: 'Peanuts', value: 'peanuts'}, {label: 'Cats', value: 'cats'}]
    },
    gender: {
      title: "Gender",
      dataType: 'string',
      fieldType: 'radio',
      items: [{label: 'Female', value: 0}, {label: 'Male', value: 1}]
    },
    contact: {
      title: 'Contact',            
      dataType: 'object',
      fieldType: 'container',       
      styles: {
        fieldWrapperStyles: {
          display: 'flex'          
        }
      },        
      properties: {
        address: {
          title: 'Address',
          dataType: 'string',
          fieldType: 'text'  
        },
        email: {
          title: 'Email',
          dataType: 'string',
          fieldType: 'text'  
        }           
      }      
    }  
  }
}

export default {
  name: 'App',
  components: {
    Fractal,
    FormBuilder
  },
  data() {
    return {
      formData: {},
      schema: sampleSchema
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  width: 95%;
  margin: 12px auto;
}



</style>
