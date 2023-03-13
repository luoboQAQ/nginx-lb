<script setup>
import { ref } from 'vue'
import { useMessage } from 'naive-ui'

const props = defineProps(['mode', 'servers'])
const emit = defineEmits(['update:mode', 'update:servers'])
const message = useMessage();

const tableMode = ref("轮询")
const serversMode = ref([
    { name: '服务1', online: false, weight: 1, port: 8000 },
    { name: '服务2', online: false, weight: 1, port: 8001 },
    { name: '服务3', online: false, weight: 1, port: 8002 },
    { name: '服务4', online: false, weight: 1, port: 8003 },
    { name: '服务5', online: false, weight: 1, port: 8004 },
    { name: '服务6', online: false, weight: 1, port: 8005 },
    { name: '服务7', online: false, weight: 1, port: 8006 },
    { name: '服务8', online: false, weight: 1, port: 8007 },
    { name: '服务9', online: false, weight: 1, port: 8008 }])

function loadMode() {
    tableMode.value = props.mode
    serversMode.value = props.servers.map(server => {
        return {
            name: server.name,
            online: server.online,
            weight: server.weight,
            port: server.port
        }
    })
}

function updateMode() {
    let check = false
    serversMode.value.forEach(server => {
        if (server.online) {
            check = true
        }
    })
    if (!check) {
        message.error('请至少选择一个服务')
        return
    }

    emit('update:mode', tableMode.value)
    const servers = serversMode.value.map(server => {
        return {
            name: server.name,
            online: server.online,
            weight: server.weight,
            port: server.port
        }
    })
    emit('update:servers', servers)
}

function cleanMode() {
    tableMode.value = "轮询"
    serversMode.value = [
    { name: '服务1', online: false, weight: 1, port: 8000 },
    { name: '服务2', online: false, weight: 1, port: 8001 },
    { name: '服务3', online: false, weight: 1, port: 8002 },
    { name: '服务4', online: false, weight: 1, port: 8003 },
    { name: '服务5', online: false, weight: 1, port: 8004 },
    { name: '服务6', online: false, weight: 1, port: 8005 },
    { name: '服务7', online: false, weight: 1, port: 8006 },
    { name: '服务8', online: false, weight: 1, port: 8007 },
    { name: '服务9', online: false, weight: 1, port: 8008 }]
}

</script>

<template>
    <n-card title="模式管理" :segmented="{ content: true, footer: 'soft' }">
        <p style="font-size: 20px;">
            当前模式： {{ mode }}
        </p>
        <template #footer>
            <n-form-item label="模式选择" size="large">
                <n-radio-group v-model:value="tableMode">
                    <n-radio-button value="轮询">轮询</n-radio-button>
                    <n-radio-button value="权重">权重</n-radio-button>
                    <n-radio-button value="IP Hash">IP Hash</n-radio-button>
                </n-radio-group>
            </n-form-item>
            <n-form-item label="服务器选择" size="large">
                <div style="display: flex; flex-wrap: wrap;">
                    <div v-for="server in serversMode" :key="server.name"
                        style="max-width: calc(100% / 3 - 10px); margin: 5px;">
                        <n-checkbox :label="server.name" v-model:checked="server.online">
                            {{ server.name }}
                        </n-checkbox>
                        <n-input-number :min="1" :max="10" placeholder="请输入权重" :disabled="tableMode !== '权重'"
                            v-model:value="server.weight" />
                    </div>
                </div>
            </n-form-item>
            <div style="display: flex;">
                <n-button type="info" style="margin-right: auto;" @click="loadMode">载入当前配置</n-button>
                <n-button type="primary" @click="updateMode">提交</n-button>&nbsp;&nbsp;&nbsp;&nbsp;
                <n-button @click="cleanMode">清空</n-button>
            </div>
        </template>
    </n-card>
</template>

<style scoped></style>