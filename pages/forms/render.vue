<template>
  <div class="py-24">
    <div class="container space-y-4">
      <div>
        <label for="a" class="uppercase tracking-wider text-gray-700">label</label>
        <input
          type="text"
          name="a"
          class="border border-gray-500 px-2"
          v-model="inputtedTextData"
        />
      </div>
      <div v-for="(formItem, formIdx) in formArch" :key="formIdx">
        <label :for="formItem.id" class="uppercase tracking-wider text-gray-700">{{ formItem.id }}</label>
        <input
          :type="formItem.inputType || 'text'"
          :name="formItem.id"
          class="border border-gray-500 px-2"
          :value="inputData[formItem.target]"
          @input="$set(inputData, formItem.target, $event.target.value)"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

interface InputData {
  name: {
    first: string
    last: string
  }
  email: string
}

interface FormItem {
  id: string
  elmType: 'input' | 'select' | 'textarea'
  inputType?: 'text' | 'number' | 'email' | 'password'
  target: string
}

interface PageData {
  formArch: readonly FormItem[]
  inputData: InputData
  inputtedTextData: string
  inputtedEmailData: string
}

export default Vue.extend<PageData, {}, {}, {}>({
  layout: 'nolayout',
  data: () => ({
    formArch: [
      {
        id: 'firstname',
        elmType: 'input',
        inputType: 'text',
        target: 'name.first', // !
      },
      {
        id: 'lastname',
        elmType: 'input',
        inputType: 'text',
        target: 'name.last', // !
      },
      {
        id: 'email',
        elmType: 'input',
        inputType: 'email',
        target: 'email',
      },
    ],
    inputData: {
      name: {
        first: 'fst',
        last: 'lst',
      },
      email: 'em',
    },
    inputtedTextData: '',
    inputtedEmailData: '',
  }),
})
</script>