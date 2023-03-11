<template>
  <n-grid x-gap="12">
    <n-gi span="6">
      <n-card :bordered="false" title="系统状态" class="light-green">
        <p>当前在线： 1</p>
        <p>服务总数： 10</p>
      </n-card>
    </n-gi>
    <n-gi span="12">
      <div class="green">
        基于Nginx的负载均衡管理界面
      </div>
    </n-gi>
    <n-gi span="6">
      <div class="light-green" />
    </n-gi>
  </n-grid>
</template>

<script setup>
import { ref } from 'vue'
const servers = ref([
  { name: 'server1', online: true },
  { name: 'server2', online: false },
  { name: 'server3', online: true },
  { name: 'server4', online: false },
  { name: 'server5', online: true },
  { name: 'server6', online: false },
  { name: 'server7', online: true },
  { name: 'server8', online: false },
  { name: 'server9', online: true },
  { name: 'server10', online: false }])

</script>

<style scoped>
.light-green {
  background-color: rgba(0, 128, 0, 0.12);
}

.green {
  height: 108px;
  background-color: rgba(0, 128, 0, 0.24);
}
</style>
