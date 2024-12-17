# vite-config-tips

## Check proxy on commandline tip e.g

```typescript
proxy: {
  "/api": {
    target: process.env.VITE_APP_SERVER_URL,
    changeOrigin: true,
    rewrite: (path) => path.replace(/^\/api/, "/api"),
    secure: false,
    ws: true,
    configure: (proxy, options) => {
      // Middleware để log request khi chuyển tiếp
      proxy.on("proxyReq", (proxyReq, req) => {
        console.log(
          [Proxy] ${req.method} ${req.url} -> ${options.target}${req.url}
        );
      });
      proxy.on("error", (err, req, res) => {
        console.error([Proxy Error]: ${err.message});
      });
    },
  },
},
```
