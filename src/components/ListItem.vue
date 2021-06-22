<template>
  <li>
    <div class="list-item-wrap">
      <label>

        <input 
        type="checkbox" 
        name="item" 
        :checked="item.quantity <= 0 ? false : isChecked" 
        @change="$emit('update:isChecked', $event.target.checked)"
        >item {{ itemIndex + 1 }}

      </label>
      <div class="number-input-wrap">

        <input 
        type="number" 
        class="number-input" 
        min="0" 
        :value="item.quantity" 
        @input="item.quantity = +$event.target.value < 0 ? 0 : +$event.target.value"
        @change="notNegative"
        >

        <input type="color" class="color-input" v-model="item.color">
      </div>
    </div>
  </li>
</template>

<script>

export default {
  name: 'ListItem',
  emits: ['update:isChecked'],
  props: ['listIndex', 'itemIndex', 'isChecked', 'item'],

  setup() {
    const notNegative = e => {
      e.target.value = Math.floor(Math.max(e.target.value,0))
    }
  
    return { notNegative }
  }
}
</script>
