<template>
  <div class="notes">
    <div class="container">
      <div class="notes__content">
        <h2 class="notes__title"  >{{ notes.length ?  "All notes" : "No notes"  }}</h2>
        <button class="notes__checker" @click="grid = !grid">
          <img src="@/assets/img/list.svg" alt="" class="notes__checker-icon" v-show="grid">
          <img src="@/assets/img/grid.svg" alt="" class="notes__checker-icon" v-show="!grid">
          <b> {{ grid ? "List" : "Grid" }}</b>
        </button>
      
      </div>
        <div class="notes__grid" :class="{column: !grid}">
          <OneNote v-for="note in notes" :key="note.id" :note="note" @del="$emit('del', note.id)" @edit="$emit('edit', note.id)"/>
        </div>
    </div>
  </div>
</template>

<script>
import OneNote from "./OneNote.vue"
export default {
  components: {
    OneNote
  },
  data() {
    return {
      grid: true
    }
  },
  props: {
    notes: {
      type: Array,
      default: []
    }
  }
};
</script>

<style>
.notes {
  padding: 50px 0;
}
.notes__content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
.notes__checker {
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 8px 12px;
    font-size: 14px;
    background: #fff;
    border: 0;
    box-shadow: var(--primaryShadow);
    border-radius: 5px;
}
.notes__grid {
  display: grid;
  gap: 20px;
}
.notes__grid.column {
  grid-template-columns: repeat(auto-fit, minmax(255px, 1fr));
}
</style>