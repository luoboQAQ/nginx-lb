<script setup>
import { ref, computed } from 'vue'
import ServerInfo from '@/components/ServerInfo.vue'
import ModelControl from '@/components/ModelControl.vue'
import ShowCode from '@/components/ShowCode.vue';

const servers = ref([
  { name: '服务1', online: true, weight: 1 },
  { name: '服务2', online: true, weight: 1 },
  { name: '服务3', online: true, weight: 1 },
  { name: '服务4', online: false, weight: 1 },
  { name: '服务5', online: false, weight: 1 },
  { name: '服务6', online: false, weight: 1 },
  { name: '服务7', online: true, weight: 1 },
  { name: '服务8', online: false, weight: 1 },
  { name: '服务9', online: true, weight: 1 }])

const mode = ref('轮询')

</script>

<template>
  <n-grid x-gap="12">
    <n-gi span="6">
      <ServerInfo :servers="servers" />
    </n-gi>
    <n-gi span="12">
      <n-gradient-text :size="60" type="success" class="title">
        基于Nginx的负载均衡管理界面
      </n-gradient-text>
      <ModelControl v-model:servers="servers" v-model:mode="mode" />
    </n-gi>
    <n-gi span="6">
      <ShowCode />
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
