<script setup lang="ts">
import { ref, onMounted } from "vue";

interface Child {
  name: string;
  age: number | null;
}

interface User {
  fullName: string;
  age: number | null;
}

interface FormData {
  user?: User;
  children?: Child[];
}

const formData = ref<FormData>({});

onMounted(() => {
  const saved = localStorage.getItem("formData");
  if (saved) {
    formData.value = JSON.parse(saved);
  }
});

// Функция для правильного окончания
function formatAge(age: number | null): string {
  if (age === null) return "Не указано";

  const n = Number(age);
  if (n % 10 === 1 && n % 100 !== 11) {
    return `${n} год`;
  } else if ([2, 3, 4].includes(n % 10) && ![12, 13, 14].includes(n % 100)) {
    return `${n} года`;
  } else {
    return `${n} лет`;
  }
}
</script>

<template>
  <div class="preview-container">
    <h2 class="title">Персональные данные</h2>
    <p class="user-info">
      {{ formData.user?.fullName || "Не указано" }},
      {{ formatAge(formData.user?.age) }}
    </p>

    <h3 class="title" style="margin-top: 50px">Дети</h3>
    <div v-if="formData.children?.length === 0"><em>Нет детей</em></div>
    <div v-else v-for="(child, index) in formData.children" :key="index">
      <p class="child-info">{{ child.name }}, {{ formatAge(child.age) }}</p>
    </div>
  </div>
</template>

<style scoped>
.preview-container {
  width: 616px;
  margin: auto;
}
.child-info {
  width: 143px;
  background: #f1f1f1;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0px;
  vertical-align: middle;
}
.title {
  margin-top: 40px;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0px;
  vertical-align: middle;
}
.user-info {
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0px;
  vertical-align: middle;
}
@media (max-width: 768px) {
  .preview-container {
    width: 310px;
  }
}
</style>
  