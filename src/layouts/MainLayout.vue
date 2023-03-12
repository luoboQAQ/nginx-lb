<template>
  <n-grid x-gap="12">
    <n-gi span="6">
      <n-card :bordered="false" title="系统状态" class="light-green">
        <p>当前在线： 1</p>
        <p>服务总数： 10</p>
        <p v-for="server in servers" :key="server.name">
          {{ server.name }}: <n-icon :component="server.online ? CloudCheckmark16Regular : CloudDismiss16Regular"
            size="40" />
        </p>
      </n-card>
    </n-gi>
    <n-gi span="12">
      <div class="green">
        基于Nginx的负载均衡管理界面
      </div>
      <n-card>
        当前模式： 轮询
      </n-card>
      <n-card title="模式切换">
        <n-radio-group v-model="mode">
          <n-radio label="轮询">轮询</n-radio>
          <n-radio label="权重">权重</n-radio>
          <n-radio label="IP">IP</n-radio>
        </n-radio-group>
        <n-checkbox-group v-model="mode">
          <n-checkbox v-for="server in servers" :key="server.name" :label="server.name">
            {{ server.name }}
            <n-input-number v-model="server.weight" :min="1" :max="10" />
          </n-checkbox>
        </n-checkbox-group>
        <n-button type="primary">
          提交
        </n-button>
        <n-button>清空</n-button>
      </n-card>
    </n-gi>
    <n-gi span="6">
      <n-log :log="`1
          2
          3
          4
                5
                6`" />
    </n-gi>
  </n-grid>
</template>

<script setup>
import { ref } from 'vue'
import { CloudCheckmark16Regular, CloudDismiss16Regular } from '@vicons/fluent'

const servers = ref([
  { name: 'server1', online: true },
  { name: 'server2', online: false },
  { name: 'server3', online: true },
  { name: 'server4', online: false },
  { name: 'server5', online: true },
  { name: 'server6', online: false },
  { name: 'server7', online: true },
  { name: 'server8', online: false },
  { name: 'server9', online: true }])

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
