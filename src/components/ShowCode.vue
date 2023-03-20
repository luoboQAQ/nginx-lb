<script setup>
import { computed } from 'vue'
import { useMessage } from 'naive-ui'
import hljs from 'highlight.js/lib/core'
import nginx from 'highlight.js/lib/languages/nginx'
import axios from 'axios'

hljs.registerLanguage('nginx', nginx)

const props = defineProps(['servers', 'mode'])
const message = useMessage()

const nginxCode = computed(() => {
  let code = `worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    
    upstream backserver { `
  if (props.mode === 'IP Hash') {
    code += `
            ip_hash;`
  }
  props.servers.forEach((server) => {
    if (server.online) {
      code += `
            server 127.0.0.1:${server.port}`
      if (props.mode === '权重') {
        code += ` weight ${server.weight};`
      } else {
        code += `;`
      }
    }
  })
  code += `
    }

    server {
        listen        80;
        server_name   localhost;
        
        location / {
            proxy_pass http://backserver;
        }
    }
    `
  return code
})

function postNginxConfig() {
  axios
    .post('http://localhost:8080/nginx/changeconf', {
      config: nginxCode.value
    })
    .then(function () {
      message.success('配置已发送至本地')
    })
    .catch(function () {
      message.error('配置发送失败')
    })
}
</script>

<template>
  <n-card title="Nginx配置预览" :segmented="{ content: true, footer: 'soft' }">
    <n-code :code="nginxCode" language="nginx" :hljs="hljs" />
    <br />
    <n-button type="primary" @click="postNginxConfig">发送配置至本地</n-button>
  </n-card>
</template>

<style scoped></style>
