<script setup>
  import { ref } from "vue";
  
  const products = ref([
    {name: '珍珠奶茶',title: '香濃奶茶搭配QQ珍珠',price: 50,quantity: 20},
    {name: '冬瓜檸檬',title: '清新冬瓜配上新鮮檸檬',price: 45,quantity: 18},
    {name: '翡翠檸檬',title: '綠茶與檸檬的完美結合',price: 55,quantity: 34},
    {name: '四季春茶',title: '香醇四季春茶，回甘無比',price: 45,quantity: 10},
    {name: '阿薩姆奶茶',title: '阿薩姆紅茶搭配香醇鮮奶',price: 50,quantity: 25},
    {name: '檸檬冰茶',title: '檸檬與冰茶的清新組合',price: 45,quantity: 20},
    {name: '芒果綠茶',title: '芒果與綠茶的獨特風味',price: 55,quantity: 18},
    {name: '抹茶拿鐵',title: '抹茶與鮮奶的絕配',price: 60,quantity: 20},
  ]);

  products.value.map(item => {
    item.isEdit = false;
    item.tempName = item.name;
    return item;
  })

  const delCount = (item) => {
    if (item.quantity > 0) {
      item.quantity -= 1;
    }
  };

  const addCount = (item) => {
    item.quantity += 1;
  };

  const edit = (item) => {
    item.isEdit = true;
  };

  const save = (item) => {
    item.isEdit = false;
    item.name = item.tempName;
  };
</script>

<template>
 <h1>Week 01</h1>
 <table>
  <thead>
    <tr>
      <th scope="col" colspan="2">品項</th>
      <th scope="col">描述</th>
      <th scope="col">價格</th>
      <th scope="col">庫存</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(product, index) in products">
      <td width="200">
        <input v-if="product.isEdit" type="text" v-model="product.tempName">
        <span v-else>{{ product.name }}</span>
      </td>
      <td>
        <button v-if="product.isEdit" type="button" @click="save(product)">儲存</button>
        <button v-else type="button" @click="edit(product)">編輯</button>
      </td>
      <td><small>{{ product.title }}</small></td>
      <td>{{ product.price }}</td>
      <td>
        <button type="button" @click="delCount(product)">-</button>
        {{ product.quantity }}
        <button type="button" @click="addCount(product)">+</button>
      </td>
    </tr>
  </tbody>
</table>
</template>

<style scoped>

</style>
