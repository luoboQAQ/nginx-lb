<script setup>
import { ref, computed } from 'vue'
import hljs from 'highlight.js/lib/core'
import nginx from 'highlight.js/lib/languages/nginx'

hljs.registerLanguage('nginx', nginx)

const props = defineProps(['servers','mode'])

function genCode() {
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
    props.servers.forEach(server => {
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
    return code;
}

const nginxCode = computed(() => {
    return genCode();
})

</script>

<template>
    <n-card title="Nginx配置预览" :segmented="{ content: true, footer: 'soft' }">
        <n-code :code="nginxCode" language="nginx" :hljs="hljs" />
    </n-card>
</template>

<style scoped></style>