<template>
    <Transition name="modal">
      <div class="modal" @click="$emit('showOrClose' , 'close')">
        <div class="modal__content"  @click.stop>
            <h3 class="modal__content-title">Add note</h3>
            <form action="" class="modal__content-form" @submit.prevent="addOrChange">
                <input type="text" class="modal__content-inp" placeholder="Title" :value="title" @input="$emit('changeTitle', $event.target.value)" required>
                <textarea name="" id="" cols="30" rows="10" class="modal__content-area" placeholder="Content" :value="desc" @input="$emit('changeDesc', $event.target.value)" required></textarea>
                <div class="modal__content-btns">
                    <a href="#!" class="modal__content-cancel" @click="$emit('showOrClose' , 'close')">Cancel</a>
                    <button class="modal__content-add">Add</button>
                </div>
            </form>
        </div>
      </div>
      </Transition>
    </template>
    
    <script>
    export default {
        props: {
            title: {
                type: String,
                default: ''
            },
            desc: {
                type: String,
                default: ''
            },
            id: {
                type: String,
                default: null
            }
        },
        methods: {
            addOrChange() {
                this.$emit("showOrClose", "open")
                this.$emit("addOrChange", this.id)
            }
        }
    }
    </script>
    
    <style>
    .modal {
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.4);
        z-index: 100;
    }
    
    .modal-enter-active,
    .modal-leave-active {
        transition: .3s;
    }
    
    .modal-enter-from,
    .modal-leave-to {
        opacity: 0;
        transform: scale(1.2);
        
    }
    
    .modal-enter-to,
    .modal-leave-from{
        opacity: 1;
        transform: scale(1);
    }
    
    .modal__content {
        max-width: 400px;
        width: 100%;
        box-shadow: var(--primaryShadow), var(--secondaryShadow);
        padding: 30px;
        border-radius: 15px;
        background: #fff;
    }
    .modal__content-title {
        text-align: center;
        margin-bottom: 8px;
    }
    .modal__content-form {
        display: grid;
        place-items: center;
        gap: 12px;
    }
    .modal__content-inp, .modal__content-area {
        width: 100%;
        padding: 10px;
        border-radius: 5px;
        box-shadow: var(--primaryShadow);
        border: 0;
        font-size: 16px;
    }
    .modal__content-area {
        resize: vertical;
    }
    .modal__content-btns {
        display: flex;
        gap: 12px;
    }
    .modal__content-cancel {
        color: red;
    }
    .modal__content-add {
        background: transparent;
        border: 0;
        font-size: 16px;
        cursor: pointer;
        color: cornflowerblue;
    }
    
    </style>