<template>
  <div class="random-wrap">

    <div 
      class="item"
      v-for="block in item.quantity"
      :key="block"
      :style="{ backgroundColor: item.color }"
      @click="item.quantity--, item.quantity <=0 ? item.isChecked = false : ''"
    ></div>

  </div>
</template>

<script>
export default {
  name: 'RandomWrap',
  props: ['item']

}
</script>
