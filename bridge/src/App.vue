<template>
  <div v-for="(item, index) in list" :key="index" class="api-test">
    <p class="api-test_id">{{ item.id }}</p>
    <p class="api-test_name">{{ item.name }}</p>
    <p class="api-test_email">{{ item.email }}</p>
    <p class="api-test_phone">{{ item.phone }}</p>
    <ul class="api-test_address">
      <li>{{ item.city }}</li>
      <li>{{ item.district }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

/** list: data */
const list = ref([])

/** api 호출 */
const fetchData = async () => {
  try {
    const response = await fetch('https://koreanjson.com/users')
    const data = await response.json()
    list.value = data
  } catch (error) {
    console.error('error :', error)
  }
}

/** mounted */
onMounted(() => {
  fetchData()
})
</script>

<style scoped>
.api-test {
  padding: 20px 0;
  display: flex;
  flex-direction: column;
}
.api-test_id {
  font-size: 20px;
  font-weight: bold;
}

.api-test_name {
  font-size: 16px;
}
.api-test_address {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  color: darkgray;
}
.api-test_address li {
  margin-right: 5px;
}
</style>
