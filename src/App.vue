<template>
  <div class="inputDesign">
    <input type="text" placeholder="write something in your ToDo List" @input="(e:any)=> text=e.target?.value" :value="text" />
    <button class="inputSubmit" @click="toDoList.push(text)">Submit</button>
  </div>
  <div class="tableWrapper">
    <ul>
      <div class="liWrapper" v-for="(a, index) in toDoList">
        <li v-if="editOn === false">{{ a }}</li>
        <template v-if="editOn === true">
          <input type="edit" @input="(b:any)=> editText=b.target?.value" :value="a" />
          <button @click="(toDoList[index] = editText), (editOn = false)">Save</button>
        </template>
        <div class="buttonWrapper">
          <button class="btn btn-danger" @click="toDoList.splice(index, 1)">⌫</button>
          <button class="btn btn-secondary" @click="editOn = true">✎</button>
        </div>
      </div>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const toDoList = ref<string[]>([]);
const text = ref('');
const editText = ref('');
const editOn = ref(false);
</script>
<style scoped>
input {
  width: 25vh;
  height: 3vh;
}

.inputSubmit {
  height: 3.5vh;
}
.inputDesign {
  display: flex;
  justify-content: center;
  align-items: center;
}
li {
  color: white;
  font-family: 'Inter', sans-serif;
  font-size: 56px;
}
.tableWrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}

.liWrapper {
  display: flex;
  justify-content: space-between;
}

.buttonWrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
