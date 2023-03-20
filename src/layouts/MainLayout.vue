<script setup>
import { ref } from 'vue'
import ServerInfo from '@/components/ServerInfo.vue'
import ModelControl from '@/components/ModelControl.vue'
import ShowCode from '@/components/ShowCode.vue'

const servers = ref([
  { name: '服务1', online: true, weight: 1, port: 8000 },
  { name: '服务2', online: true, weight: 1, port: 8001 },
  { name: '服务3', online: true, weight: 1, port: 8002 },
  { name: '服务4', online: false, weight: 1, port: 8003 },
  { name: '服务5', online: false, weight: 1, port: 8004 },
  { name: '服务6', online: false, weight: 1, port: 8005 },
  { name: '服务7', online: true, weight: 1, port: 8006 },
  { name: '服务8', online: false, weight: 1, port: 8007 },
  { name: '服务9', online: true, weight: 1, port: 8008 }
])

const mode = ref('轮询')
</script>

<template>
  <n-grid x-gap="12" style="align-items: flex-end">
    <n-gi span="6">
      <ServerInfo :servers="servers" />
    </n-gi>
    <n-gi span="12">
      <n-gradient-text :size="60" type="success" class="title">
        基于Nginx的负载均衡管理界面
      </n-gradient-text>
      <n-message-provider>
        <ModelControl v-model:servers="servers" v-model:mode="mode" />
      </n-message-provider>
    </n-gi>
    <n-gi span="6">
      <n-message-provider>
        <ShowCode :servers="servers" :mode="mode" />
      </n-message-provider>
    </n-gi>
  </n-grid>
</template>

<style scoped>
.title {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 300px;
}
</style>
