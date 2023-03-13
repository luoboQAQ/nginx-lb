<script setup>
import { computed } from 'vue'
import { CloudCheckmark16Regular, CloudDismiss16Regular } from '@vicons/fluent'

const myServers = defineProps(['servers'])

const onlineNum = computed(() => myServers.servers.filter(server => server.online).length)
</script>

<template>
    <n-card title="系统状态" :segmented="{ content: true, footer: 'soft' }">
      <div class="status">
        <p>当前在线： {{ onlineNum }}</p>
        <p>服务总数： {{ servers.length }}</p>
      </div>
        <template #footer>
            <p v-for="server in servers" :key="server.name" class="detail">
                {{ server.name }}: &nbsp;&nbsp;&nbsp;&nbsp;
                <n-icon :component="server.online ? CloudCheckmark16Regular : CloudDismiss16Regular"
                    :color="server.online ? '#18a058' : '#d03050'" size="40" />
            </p>
        </template>
    </n-card>
</template>

<style scoped>
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