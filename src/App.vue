<script setup>
  import { ref } from "vue";
  
  const products = ref([
    {id: 1,name: '珍珠奶茶',title: '香濃奶茶搭配QQ珍珠',price: 50,quantity: 20},
    {id: 2,name: '冬瓜檸檬',title: '清新冬瓜配上新鮮檸檬',price: 45,quantity: 18},
    {id: 3,name: '翡翠檸檬',title: '綠茶與檸檬的完美結合',price: 55,quantity: 34},
    {id: 4,name: '四季春茶',title: '香醇四季春茶，回甘無比',price: 45,quantity: 10},
    {id: 5,name: '阿薩姆奶茶',title: '阿薩姆紅茶搭配香醇鮮奶',price: 50,quantity: 25},
    {id: 6,name: '檸檬冰茶',title: '檸檬與冰茶的清新組合',price: 45,quantity: 20},
    {id: 7,name: '芒果綠茶',title: '芒果與綠茶的獨特風味',price: 55,quantity: 18},
    {id: 8,name: '抹茶拿鐵',title: '抹茶與鮮奶的絕配',price: 60,quantity: 20},
  ]);
  
  const tempEdit = ref({});

  const delCount = (product) => {
    if (product.quantity > 0) {
      product.quantity -= 1;
    }
  };

  const addCount = (product) => {
    product.quantity += 1;
  };

  const addProduct = () => {
    products.value.push({
      id: new Date().getTime(),
      name: '',
      title: '',
      price: 0,
      quantity: 0
    });
  };

  const delProduct = (product) => {
    const index = products.value.findIndex(item => item.id === product.id)
    products.value.splice(index, 1);
  };

  const preparEdit = (product) => {
    tempEdit.value = { ...product };
  };
  
  const confirmEdit = () => {
    const index = products.value.findIndex(item => item.id === tempEdit.value.id);
    const { name, title } = tempEdit.value;
    products.value[index].name = name;
    products.value[index].title = title;
    tempEdit.value = {};
  };
</script>

<template>
  <h1>Week 01</h1>
  <button type="button" @click="addProduct">新增</button>
  <hr>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
        <th scope="col">刪除</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(product, index) in products" :key="index">
        <td width="200">
          <span>{{ product.name }}</span>
        </td>
        <td><small>{{ product.title }}</small></td>
        <td>{{ product.price }}</td>
        <td>
          <button type="button" @click="delCount(product)">-</button>
          {{ product.quantity }}
          <button type="button" @click="addCount(product)">+</button>
        </td>
        <td>
          <button type="button" @click="delProduct(product)">刪除</button>
          <button type="button" @click="preparEdit(product)">編輯</button>
        </td>
      </tr>
    </tbody>
  </table>
  <hr>
  <div v-if="tempEdit.id">
    <h2>編輯</h2>
    當前編輯物件：<br>
    品項：<input type="text" v-model="tempEdit.name"><br>
    描述：<input type="text" v-model="tempEdit.title">
    <button type="button" @click="confirmEdit">確認編輯</button>
    <button type="button" @click="tempEdit = {}">取消編輯</button>
  </div>
</template>

<style scoped>

</style>
