<script setup>
import { ref } from 'vue'

defineProps(['mode', 'servers'])
defineEmits(['update:mode', 'update:servers'])

const tableMode = ref(null)
const serversMode = ref(null)
const weightMode = ref([1, 1, 1, 1, 1, 1, 1, 1, 1])

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
                <n-checkbox-group v-model:value="serversMode" style="display: flex; flex-wrap: wrap;">
                    <div v-for="(server, index) in servers" :key="server.name" style="max-width: calc(100% / 3 - 10px); margin: 5px;">
                        <n-checkbox :label="server.name" :value="server.name">
                            {{ server.name }}
                        </n-checkbox>
                        <n-input-number :min="1" :max="10" placeholder="请输入权重" :disabled="tableMode !== '权重'"
                            v-model:value="weightMode[index]" />
                    </div>
                </n-checkbox-group>
            </n-form-item>
            <div style="display: flex;">
                <n-button type="info" style="margin-right: auto;">载入当前配置</n-button>
                <n-button type="primary">提交</n-button>&nbsp;&nbsp;&nbsp;&nbsp;
                <n-button>清空</n-button>
            </div>
        </template>
    </n-card>
</template>

<style scoped></style>