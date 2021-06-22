<template>
  <div class="container">
    <left-block></left-block>
    <right-block></right-block>
  </div>
</template>

<script>
import { getRandomNumber } from '@/utils/getRandomNumber.js'
import { ref, onMounted, provide } from 'vue'
import LeftBlock from '@/components/LeftBlock'
import RightBlock from '@/components/RightBlock'

export default {
  name: 'App',

  setup() {
    const colorsArray = ['#963DFF', '#2CC7DE', '#7AF53E', '#DEA72C', '#FF3533', '#1D22DE', '#FF8B21', '#2BF5AB', '#0703FF', '#FFFF00']
    const listsArray = ref([])
    const listCount = getRandomNumber(4, 6)

    onMounted(() => {
      for (let y = 0; y < listCount; y++) {
        const itemsCount = getRandomNumber(4, colorsArray.length)
        const list = []
        for (let i = 0; i < itemsCount; i++) {
          list.push({
            quantity: getRandomNumber(1, 19),
            color: colorsArray[i],
            isChecked: false,
            itemIndex: i
          })
        }
        listsArray.value.push(list)
      }
    })

    provide('listsArray', listsArray.value)

    return {}
  },

  components: { LeftBlock, RightBlock }
}
</script>