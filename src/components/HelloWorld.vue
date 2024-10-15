<script setup>
import { ref } from "vue";
let users = ref([]);
let text = ref("");
let text1 = ref("");
let iseditup= ref(false)
let iseditID= ref(null)

function submit() {
  if(text.value!=="" && text1.value!==""){
    if (iseditup.value===true) {
    let iseditTodo= users.value.find(user=>user.id==iseditID.value)
    iseditTodo.text=text.value
    iseditTodo.text1=text1.value

    iseditup.value=false
    iseditID.value=null

    
    text.value = "";
    text1.value = "";
  }

  else{
    let addUsers = {
      id: users.value.length + 1,
      text: text.value,
      text1: text1.value,
    };
    users.value.push(addUsers);
    (text.value = ""), (text1.value = "");
  }
  }
  else{
    alert('barchasiga malumot tuldiring')
  }
}

const clearDelete = (id) => {
  users.value = users.value.filter((user) => user.id !== id);
};

function EditTodo(id){
  const findEdit = users.value.find(user=>user.id == id)
  text.value= findEdit.text
  text1.value= findEdit.text1
  iseditup.value=true
  iseditID.value=findEdit.id
}

</script>
<template>
  <div class="contianer">
    <h1>Todo Text</h1>
    <form @submit.prevent="submit">
      <input
        type="text"
        v-model="text"
        class="form-control"
        placeholder="Enter text name"
      />
      <input
        type="text"
        v-model="text1"
        class="form-control"
        placeholder="Enter text log..."
      />
      <button class="button" type="submit">add</button>
    </form>
    <h1>Todo ma'lumoti {{ users.length }}</h1>
    <ul>
      <li>N-r</li>
      <li>Text name</li>
      <li>Text log..</li>
      <li>edit</li>
      <li>delete</li>
    </ul>
    <span v-if="users.length == 0" class="add-lugat">Ma'lumotlar qolmadi</span>
    <ol>
      <li v-for="user in users" :key="user.id" class="ol">
        <span>{{ user.id }}.</span><span>{{ user.text }}</span>
        <span style="margin-left: 20px">{{ user.text1 }}</span>
        <button @click="EditTodo(user.id)">edit</button>
        <button @click="clearDelete(user.id)">delete</button>
      </li>
    </ol>
  </div>
</template>
<style scoped>
.contianer {
  width: 580px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid black;
  border-radius: 10px;
  background-color: rgb(242, 255, 0);
}
.form-control {
  width: 400px;
  padding: 10px;
  border-radius: 20px;
}
.form-control {
  display: block;
}
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
.button {
  width: 100px;
  padding: 8px;
  border-radius: 20px;
  border: none;
  background-color: rgb(26, 26, 29);
  color: wheat;
  cursor: pointer;
}
ul {
  width: 500px;
  display: flex;
  justify-content: space-between;
}
.ol {
  width: 500px;
  display: flex;
  justify-content: space-between;
}
button {
  cursor: pointer;
  background-color: rgb(140, 255, 0);
  border-radius: 10px;
}
.add-lugat {
  font-size: 25px;
  margin-top: 50px;
  width: 500px;
  text-align: center;
  border-radius: 20px;
  padding: 20px;
  border: 1px solid red;
}
li {
  margin-top: 10px;
  list-style: none;
}
</style>
