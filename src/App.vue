<template>
  <Header @getSearch="search = $event"/>
  <Notes :notes="filterNotes" @del="delNote" @edit="editNote" />
  <Model 
  v-show="showModal"
  :title="modalTitle"
  :desc="modalDesc"
  :id="curID"
  @changeTitle="modalTitle = $event"
  @changeDesc="modalDesc = $event"
  @addOrChange="addOrChange"
  @showOrClose="closeModal"
  />
  
  <a href="#" class="openModal" @click.prevent="showModal = true">
    <img src="./assets/img/edit.svg" alt="">
  </a>
  
  </template> 
  
  <script>
  import Header from "@/components/Header.vue"
  import Model from "@/components/Model.vue"
  import Notes from "@/components/Notes.vue"
  import { v4 as uuidv4 } from "uuid";
  
  export default {
    name: 'App',
    components: {
      Header,
      Model,
      Notes
    },
    data() {
      return {
        modalTitle: "",
        modalDesc: "",
        label: localStorage.label ? JSON.parse(localStorage.label) : [],
        showModal: false,
        curID: null,
        search: ''
      }
    },
    computed: {
     filterNotes() {
      return this.search ? this.label.filter(item => item.title.toLowerCase().includes(this.search.toLowerCase())) : this.label
     }
    },
    methods: {
      addOrChange(id) {
        let obj = {
          title: this.modalTitle,
          desc: this.modalDesc,
          date: new Date(Date.now()).toLocaleDateString(),
          id: id || uuidv4()
        }
        if (id) {
          let idx = this.label.findIndex((item) => item.id == id)
          this.label[idx] = obj
        } else {
          this.label.push(obj)
        }
        this.curID = null;
        this.label.push(obj)
        this.save()
      },
      closeModal(val) {
        if (val == "close") {
          this.modalTitle = "";
          this.modalDesc = "";
          this.showModal = !this.showModal;
          this.curID = null
        }
      },
      save() {
        localStorage.label = JSON.stringify(this.label)
      },
      delNote(id) {
        // console.log(id);
        let idx = this.label.findIndex(item => item.id == id)
        // console.log(idx);
        this.label.splice(idx, 1 )
        this.save()
      },
      editNote(id) {
        const obj = this.label.find(item => item.id == id)
        console.log(obj);
        this.modalTitle = obj.title;
        this.modalDesc = obj.desc;
        this.curID = obj.id
        this.showModal = true
      }
  
    }
  }
  </script>
  
  <style>
  .openModal {
    position: fixed;
    bottom: 3rem;
    right: 3rem;
    width: 60px;
    height: 60px;
    display: grid;
    place-items: center;
    background: #fff;
    box-shadow: var(--secondaryShadow), var(--primaryShadow);
    border-radius: 15px;
  }
  </style>
  