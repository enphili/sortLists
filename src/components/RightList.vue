<template>
  <div class="right-list-wrap">

    <div class="header-block">
      <span>List {{ listIndex + 1 }}</span>
      <button class="btn" @click.prevent="sortItems">{{ isItemSort ? 'Перемешать' : 'Сортировать' }}</button>
    </div>

    <div class="sort-wrap" v-if="isItemSort">
      <random-wrap
        v-for="item in checkedItems"
        :key="item"
        :item="item"
      ></random-wrap>

    </div>

    <sort-wrap 
      v-else
      :items="sortItemsArray"
      @delItem="delItem"
    ></sort-wrap>

  </div>
</template>

<script>
import { ref, inject, computed } from 'vue'
import { shuffle } from '@/utils/shuffle.js'
import RandomWrap from '@/components/RandomWrap'
import SortWrap from '@/components/SortWrap'

export default {
  name: 'RightList',
  props: ['listIndex'],

  setup(props) {
    const isItemSort = ref(true)
    const listsArray = inject('listsArray')

    const checkedItems = computed(() => listsArray[props.listIndex].filter(item => item.isChecked === true))

    const sortItemsArray = computed(() => {
      const temp = []
      checkedItems.value.forEach(item => {
        const temp2 = []
        for (let i = 0; i < item.quantity; i++) {
          temp2.push({color: item.color, index: item.itemIndex})
        }
        temp.push(...temp2)
      })
      return shuffle(temp)
    })

    const sortItems = () => {
      shuffle(sortItemsArray.value)
      if (isItemSort.value === true) {
        isItemSort.value = false
      } else {
        isItemSort.value = true
      }
    }

    const delItem = num => {
      listsArray[props.listIndex][num].quantity--
      if (listsArray[props.listIndex][num].quantity <= 0) {
        listsArray[props.listIndex][num].isChecked = false
      }
    }

    return { sortItems, isItemSort, checkedItems, sortItemsArray, delItem }
  },

  components: { RandomWrap, SortWrap }
}
</script>