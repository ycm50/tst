# Netlify HTTP路径代理

这是一个使用Netlify Edge Functions实现的HTTP路径代理服务。

## 本地测试方法

1. 安装Netlify CLI（如果尚未安装）
```bash
npm install -g netlify-cli
```

2. 安装项目依赖
```bash
npm install
```

3. 启动本地开发服务器
```bash
npm run dev
# 或直接使用
netlify dev
```

4. 服务器启动后，你可以在浏览器中访问以下URL进行测试：
   - 根路径：`http://localhost:8888/` 将显示提示信息
   - 代理测试：`http://localhost:8888/https://example.com`
   - 或使用：`http://localhost:8888/proxy/https://example.com`

5. 使用curl命令进行测试（可选）
```bash
# 测试根路径
curl http://localhost:8888/

# 测试代理功能
curl http://localhost:8888/https://example.com

# 测试非HTTP协议的错误处理
curl http://localhost:8888/example.com
```

## 测试场景

1. **基本代理功能测试**
   - 访问不同类型的网站（静态网站、动态网站）
   - 验证页面内容是否正确显示

2. **相对路径资源测试**
   - 代理HTML页面，检查其中的图片、CSS、JavaScript等相对路径资源是否能正确加载
   - 验证页面样式和功能是否正常

3. **错误处理测试**
   - 输入不完整的URL（如没有http://前缀）
   - 输入不存在的网址
   - 验证错误提示是否符合预期

## 问题排查

如果在测试过程中遇到问题：

1. 确保Netlify CLI版本是最新的：
```bash
npm install -g netlify-cli@latest
```

2. 检查netlify.toml文件中的路径配置是否正确

3. 查看终端输出的错误信息，根据提示进行排查

4. 确认目标网站允许被代理访问（某些网站可能设置了X-Frame-Options或CORS限制）

## 部署方法

1. 登录Netlify
```bash
netlify login
```

2. 初始化项目（如果尚未初始化）
```bash
netlify init
```

3. 部署项目
```bash
netlify deploy --prod
```

## 使用方法

部署完成后，可以通过以下方式使用代理服务：

- 访问根路径：`https://your-netlify-site.netlify.app/` 将显示提示信息
- 使用代理：`https://your-netlify-site.netlify.app/proxy/https://target-url.com`
- 或直接使用：`https://your-netlify-site.netlify.app/https://target-url.com`

## 注意事项

- 请确保目标URL以http://或https://开头
- 代理服务会自动处理HTML内容中的相对路径资源链接