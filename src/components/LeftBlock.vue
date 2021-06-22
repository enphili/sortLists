<template>
  <div class="container vertical">

    <list-block
      v-for="(list, idx) in lists"
      :listIndex = "idx"
      :key="list"
      :items="list"
    >
    </list-block>

  </div>
</template>

<script>
import { inject } from 'vue'
import ListBlock from '@/components/ListBlock'

export default {
  name: 'LeftBlock',

  setup() {
    return {
      lists: inject('listsArray')
    }
  },

  components: { ListBlock }
}
</script>
