<template>
  <div class="container vertical">

    <right-list
      v-for="(list, idx) in lists"
      :listIndex = "idx"
      :key="list"
    ></right-list>

  </div>
</template>

<script>
import { inject } from 'vue'
import RightList from '@/components/RightList'

export default {
  name: 'RightBlock',

  setup() {
    return { 
      lists: inject('listsArray')
    }
  },

  components: { RightList }
}
</script>