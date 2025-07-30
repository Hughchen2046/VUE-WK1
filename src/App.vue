<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { ref } from 'vue'

// 初始化所有品項都要有 edit 欄位
const items = ref([
  { name: '珍珠奶茶', desc: '香濃奶茶搭配QQ珍珠', price: 50, stock: 20, edit: { name: false, desc: false, price: false } },
  { name: '冬瓜檸檬', desc: '清新冬瓜配上新鮮檸檬', price: 45, stock: 18, edit: { name: false, desc: false, price: false } },
  { name: '翡翠檸檬', desc: '綠茶與檸檬的完美結合', price: 55, stock: 34, edit: { name: false, desc: false, price: false } },
  { name: '四季春茶', desc: '香醇四季春茶，回甘無比', price: 45, stock: 10, edit: { name: false, desc: false, price: false } },
  { name: '阿薩姆奶茶', desc: '阿薩姆紅茶搭配香醇鮮奶', price: 50, stock: 25, edit: { name: false, desc: false, price: false } },
  { name: '檸檬冰茶', desc: '檸檬與冰茶的清新組合', price: 45, stock: 20, edit: { name: false, desc: false, price: false } },
  { name: '芒果綠茶', desc: '芒果與綠茶的獨特風味', price: 55, stock: 18, edit: { name: false, desc: false, price: false } },
  { name: '抹茶拿鐵', desc: '抹茶與鮮奶的絕配', price: 60, stock: 20, edit: { name: false, desc: false, price: false } }
])

function minus(idx) {
  if (items.value[idx].stock > 0) items.value[idx].stock--
}
function positive(idx) {
  items.value[idx].stock++
}

// 編輯模式切換
function editField(idx, field) {
  items.value[idx].edit[field] = true
}
function saveField(idx, field, event) {
  items.value[idx][field] = field === 'price'
    ? parseInt(event.target.value, 10)
    : event.target.value
  items.value[idx].edit[field] = false
}

// 新增品項
function addItem() {
  items.value.push({
    name: '新飲品',
    desc: '請編輯描述',
    price: 0,
    stock: 0,
    edit: { name: false, desc: false, price: false }
  })
}

// 刪除品項
function removeItem(idx) {
  items.value.splice(idx, 1)
}

</script>

<template>
  <header class="wd50">
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="第一週作業繳交" />
    </div>
  </header>
  <main class="container mt-48">

    <table>
      <thead>
        <tr class="row">
          <th scope="col" class="col-2">品項</th>
          <th scope="col" class="col-3">描述</th>
          <th scope="col" class="col-1">價格</th>
          <th scope="col" class="col-4">庫存</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, idx) in items" :key="item.name + idx" class="row">
          <!-- 名稱 -->
          <td class="col-2 text-align-center">
            <span v-if="!item.edit.name" @dblclick="editField(idx, 'name')">{{ item.name }}</span>
            <input v-else type="text" :value="item.name" @blur="saveField(idx, 'name', $event)"
              @keyup.enter="saveField(idx, 'name', $event)" />
          </td>
          <!-- 描述 -->
          <td class="col-3 text-align-center">
            <span v-if="!item.edit.desc" @dblclick="editField(idx, 'desc')">{{ item.desc }}</span>
            <input v-else type="text" :value="item.desc" @blur="saveField(idx, 'desc', $event)"
              @keyup.enter="saveField(idx, 'desc', $event)" />
          </td>
          <!-- 價格 -->
          <td class="col-2 text-align-center">
            <span>NT$ </span><span v-if="!item.edit.price" @dblclick="editField(idx, 'price')">{{ item.price }}</span>
            <input v-else type="number" :value="item.price" @blur="saveField(idx, 'price', $event)"
              @keyup.enter="saveField(idx, 'price', $event)" />
          </td>
          <!-- 庫存 -->
          <td class="col-4 text-align-center">
            <button type="button" @click="minus(idx)" class="btn-round">-</button>
            {{ item.stock }}
            <button type="button" @click="positive(idx)" class="btn-round">+</button>
          </td>
          <!-- 刪除按鈕 -->
          <td>
            <button type="button" @click="removeItem(idx)" class="border-radius-10">🗑</button>
          </td>
        </tr>
      </tbody>

    </table>
    <button @click="addItem" class="border-radius-10">新增品項</button>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.container {
  max-width: 1296px;
  margin: 0 auto;
}

.row {
  margin-left: -8px;
  margin-right: -8px;
}

.col-1 {
  padding-left: 8px;
  padding-right: 8px;
  width: calc(100%/12);
}

.col-2 {
  padding-left: 8px;
  padding-right: 8px;
  width: calc(100%/12 * 2);
}

.col-3 {
  padding-left: 8px;
  padding-right: 8px;
  width: calc(100%/12 * 3);
}

.col-4 {
  padding-left: 8px;
  padding-right: 8px;
  width: calc(100%/12 * 4);
}

.col-12 {
  padding-left: 8px;
  padding-right: 8px;
  width: 100%;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.mt-48 {
  margin-top: 48px;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: 24px;
  }

  .row-lg {
    margin-left: -12px;
    margin-right: -12px;
  }

  .col-lg-4 {
    padding-left: 12px;
    padding-right: 12px;
    width: calc(100%/12 *4);
  }

  .col-lg-8 {
    padding-left: 12px;
    padding-right: 12px;
    width: calc(100%/12 *8);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

.text-align-center {
  text-align: center;
}

p {
  font-size: 18px;
  color: blue;
}

.border-radius-10 {
  border-radius: 10px;
}

button {
  display: inline-block;
  background-color: rgb(57, 240, 139);
  cursor: pointer;
  margin: 1rem;
  padding: 0.5rem 1rem;
  font-size: 1rem;
}

.btn-round {
  width: 28px;
  height: 28px;
  padding: 0;
  margin: 0 0.5rem;
  border-radius: 10000px;
}
</style>
