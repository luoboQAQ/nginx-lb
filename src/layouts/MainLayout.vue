<template>
  <n-grid x-gap="12">
    <n-gi span="6">
      <n-card title="系统状态" :segmented="{ content: true, footer: 'soft' }">
        <p class="status">当前在线： {{ onlineNum }}</p>
        <p class="status">服务总数： {{ servers.length }}</p>
        <template #footer>
          <p v-for="server in servers" :key="server.name" class="detail">
            {{ server.name }}: &nbsp;&nbsp;&nbsp;&nbsp;
            <n-icon :component="server.online ? CloudCheckmark16Regular : CloudDismiss16Regular"
              :color="server.online ? '#18a058' : '#d03050'" size="40" />
          </p>
        </template>
      </n-card>
    </n-gi>
    <n-gi span="12">
      <n-gradient-text :size="60" type="success" class="title">
        基于Nginx的负载均衡管理界面
      </n-gradient-text>
      <n-card>
        <p style="font-size: 20px;">
          当前模式： {{ mode }}
        </p>
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
import { ref, computed } from 'vue'
import { CloudCheckmark16Regular, CloudDismiss16Regular } from '@vicons/fluent'

const servers = ref([
  { name: '服务1', online: true },
  { name: '服务2', online: true },
  { name: '服务3', online: true },
  { name: '服务4', online: false },
  { name: '服务5', online: false },
  { name: '服务6', online: false },
  { name: '服务7', online: true },
  { name: '服务8', online: false },
  { name: '服务9', online: true }])

const mode = ref('轮询')

const onlineNum = computed(() => servers.value.filter(server => server.online).length)

</script>

<style scoped>
.title {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 300px;
}

.detail {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
}

.status {
  font-size: 30px;
}
</style>
