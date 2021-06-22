<template>
  <div class="list-block">
      <div ref="dropIcon" class="drop-icon" @click="openList"></div>

      <label class="radio">
        <input 
        type="checkbox" 
        :checked="isAnyItemChoose"
        @click="chooseAllItems"
        >
        <span></span>List {{ listIndex + 1 }}</label>

      <ul ref="ul" :style="{ maxHeight: height + 'px' }">

        <list-item
          v-for="(item, idx) in items"
          :key="item"
          :itemIndex="idx"
          :item="item"
          :listIndex="listIndex"
          v-model:isChecked="item.isChecked"
        >
        </list-item>

      </ul>

    </div>
</template>

<script>
import { ref, computed } from 'vue';
import ListItem from '@/components/ListItem'

export default {
  name: 'ListBlock',
  props: ['listIndex', 'items'],

  setup(props) {
    const isListOpen = ref(false)
    const ul = ref(null)
    const height = ref('0')


    const chooseAllItems = e => {
      const listInput = e.target
      if (listInput.checked) {
        props.items.forEach(item => item.isChecked = true)
      } else {
        props.items.forEach(item => item.isChecked = false)
      }
    }

    const openList = e => {
      const elem = e.target
      if (isListOpen.value === true) {
        isListOpen.value = false
        elem.style.transform = `rotate(0deg)`
        height.value = 0
      } else {
        isListOpen.value = true
        elem.style.transform = `rotate(90deg)`
        height.value = ul.value.scrollHeight
      }
    }

    const isAnyItemChoose = computed(() => props.items.some(item => item.isChecked === true))


    return { chooseAllItems, openList, isListOpen, ul, height, isAnyItemChoose }
  },

  components: { ListItem }
}
</script>
