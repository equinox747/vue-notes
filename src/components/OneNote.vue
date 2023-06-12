<template>
  <div class="notes__item">
    <h3 class="notes__item-title"> {{ note.title }}</h3>
    <span class="notes__item-date"> {{ note.data }}</span>
    <p class="notes__item-desc"> {{ note.desc }}</p>
    <div class="notes__item-control">
        <a href="#!" class="notes__item-edit" @click="$emit('edit', note.id)"><img src="../assets/img/edit.svg" alt="">edit</a>
        <a href="#!" class="notes__item-del" @click="$emit('del' , note.id)"><img src="../assets/img/del.svg" alt="">delete</a>
     </div>
  </div>


</template>

<script>


export default {
   props: {
       note: {
           type: Object,
           default:{
            title: '',
            desc: '',
            date: '',
            id:0
           }
      }
   },

}
</script>

<style>
.notes__item {
    display: grid;
    gap: 5px;
    padding: 20px;
    border-radius: 15px;
    box-shadow: var(--secondaryShadow), var(--primaryShadow);
    overflow-wrap: anywhere;
}
.notes__item-date {
    font-size: 14px;
    justify-content: flex-end;
    gap: 30px;
}
.notes__item-control {
    display: flex;
    justify-content: flex-end;
    gap: 30px;
}
.notes__item-edit, .notes__item-del {
    display: flex;
    align-content: center;
    gap: 8px;
    text-transform: capitalize;
}
</style>