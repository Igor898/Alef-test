<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";

interface Child {
  name: string;
  age: number | null;
}

interface User {
  fullName: string;
  age: number | null;
}

const user = ref<User>({
  fullName: "",
  age: null,
});

const children = ref<Child[]>([]);

const router = useRouter();

function addChild() {
  if (children.value.length < 5) {
    children.value.push({ name: "", age: null });
  }
}

function removeChild(index: number) {
  children.value.splice(index, 1);
}

function isValidAge(childAge: number | null): boolean {
  return (
    childAge !== null && user.value.age !== null && childAge <= user.value.age
  );
}

function saveData() {
  const allChildrenValid = children.value.every((child) =>
    isValidAge(child.age)
  );

  if (!allChildrenValid) {
    alert("Возраст ребёнка не может быть больше возраста пользователя.");
    return;
  }

  const data = {
    user: user.value,
    children: children.value,
  };

  localStorage.setItem("formData", JSON.stringify(data));
  router.push("/preview");
}
</script>

<template>
  <div class="form-container">
    <h2 style="margin: 40px 0">Персональные данные</h2>
    <div>
      <input class="user_input" v-model="user.fullName" placeholder="Имя" />
    </div>
    <div style="margin-bottom: 30px">
      <input
        class="user_input"
        v-model.number="user.age"
        placeholder="Возраст"
      />
    </div>

    <div class="d-flex" style="margin-bottom: 10px">
      <h3>Дети (макс. 5)</h3>
      <button
        class="add-child"
        @click="addChild"
        :disabled="children.length >= 5"
      >
        + Добавить ребенка
      </button>
    </div>

    <div v-for="(child, index) in children" :key="index" class="child-block">
      <div class="d-flex">
        <div>
          <input
            class="child_input"
            v-model="child.name"
            placeholder="Имя"
            style="margin-right: 15px"
          />
        </div>
        <div>
          <input
            class="child_input"
            v-model.number="child.age"
            placeholder="Возраст"
          />
        </div>
      </div>
      <button class="delete" @click="removeChild(index)">Удалить</button>
    </div>

    <div class="save-flex"><button class="save" @click="saveData">Сохранить</button></div>
  </div>
</template>
  
<style scoped>
.form-container {
  width: 616px;
  margin: auto;
}
.user_input {
  width: 100%;
  height: 56px;
  border-radius: 4px;
  border-width: 1px;
  border-color: #f1f1f1;
  margin-bottom: 15px;
  padding-left: 15px;
}
.d-flex {
  display: flex;
  justify-content: space-between;
}
.add-child {
  border-radius: 100px;
  border-width: 2px;
  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 10px;
  padding-left: 20px;
  border-color: #01a7fd;
  color: #01a7fd;
  background: none;
}
.child-block {
  display: flex;
  justify-content: space-between;
  margin-bottom: 15px;
}
.child_input {
  width: 260px;
  height: 56px;
  border-radius: 4px;
  border-width: 1px;
  border-color: #f1f1f1;
  padding-left: 15px;
}
.delete {
  border: none;
  background: none;
  color: #01a7fd;
}
.save {
  border-radius: 100px;
  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 10px;
  padding-left: 20px;
  background: #01a7fd;
  border: none;
  color: #ffffff;
  margin-bottom: 10px;
}
@media (max-width: 768px) {
  .form-container {
    width: 310px;
    margin: auto;
  }
  .d-flex {
    flex-direction: column;
  }
  .child_input {
    width: 230px;
    height: 56px;
    margin-bottom: 15px;
  }
  .child-block {
    margin-bottom: 0;
  }
  .add-child {
    margin: 20px;
  }
  .save-flex {
    display: flex;
    justify-content: center;
  }
}
</style>