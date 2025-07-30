<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      You’ve successfully created a 飲料訂單系統.
    </h3>
    <h4>Made by Hugh</h4>
    <hr>
    <span>--V1.0--</span>
    <p>可以點選新增品項</p>
    <p>右側有刪除品項</p>
    <p>雙擊品項、描述、價格可以輸入內容來更動</p>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

h4,
span {
  font-weight: bold;
  color: blue;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
