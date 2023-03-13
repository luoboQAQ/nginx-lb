<script setup>
import {ref} from 'vue'

const nginxCode = ref(`
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;

    keepalive_timeout  65;

    # 反向代理后端服务器
    upstream backserver { 
            server 127.0.0.1:8000; 
            server 127.0.0.1:8001;
            server 127.0.0.1:8002; 
    }

    server {
        listen        80;
        server_name   localhost;
        
        location / {
            proxy_pass http://backserver;
        }
        
    }
    `)
</script>

<template>
    <n-card title="Nginx配置预览"> 
        <n-code :code="nginxCode" language="nginx" />
    </n-card>
</template>

<style scoped>
</style>