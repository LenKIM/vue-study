<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer">
      <i class="fas fa-plus " v-on:click="addTodo"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <!--
        you can use custom content here to overwrite
        default content
      -->
      <h3 slot="header" class="closeModalBtn">
        경고
        <i class="closeModalBtn fas fa-times" @click="showModal=false"></i>
      </h3>

      <h3 slot="body">
        아무것도 입력하지 않았습니다.
      </h3>

      <!--           모달 푸터-->
<!--      <div class="modal-footer">-->
<!--        <slot name="footer">-->
<!--          default footer-->
<!--          <button class="modal-default-button" @click="$emit('close')">-->
<!--            OK-->
<!--          </button>-->
<!--        </slot>-->
<!--      </div>-->
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal'

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        // this.$emit('이벤트 이름', 인자1, 인자2, ...)
        // this.$emit('addTodoItem', this.newTodoItem)
        this.$store.commit('addOneItem', this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}

.inputBox {
  background: aliceblue;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}

.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}

.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

.addBtn {
  color: white;
  vertical-align: middle;
}

.closeModalBtn {
  color: #42b983;
}
</style>