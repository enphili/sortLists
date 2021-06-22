<template>
  <div class="random-wrap">

    <div 
      class="item"
      v-for="elem in items"
      :key="elem"
      :style="{ backgroundColor: elem.color }"
      @click="$emit('delItem', elem.index)"
    ></div>

  </div>
</template>

<script>
export default {
  name: 'SortWrap',
  props: ['items'],
  emits: ['delItem']

}
</script>