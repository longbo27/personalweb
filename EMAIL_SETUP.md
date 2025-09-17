# 联系表单邮件发送设置指南

## 📧 邮件发送方式

目前网站支持两种邮件发送方式，您可以选择其中一种：

### 方法1: EmailJS (推荐) ⭐

**优点：**
- 免费额度：200封/月
- 无需后端服务器
- 设置简单
- 支持自定义邮件模板

**设置步骤：**

1. **注册 EmailJS 账户**
   - 访问 [https://www.emailjs.com/](https://www.emailjs.com/)
   - 注册免费账户

2. **创建邮件服务**
   - 登录后，进入 "Email Services"
   - 选择您的邮件提供商（Gmail, Outlook, Yahoo等）
   - 按照提示连接您的邮箱账户

3. **创建邮件模板**
   - 进入 "Email Templates"
   - 创建新模板，使用以下变量：
     ```
     发件人: {{from_name}} ({{from_email}})
     主题: {{subject}}
     消息: {{message}}
     ```

4. **获取配置信息**
   - Service ID: 在 "Email Services" 页面找到
   - Template ID: 在 "Email Templates" 页面找到
   - Public Key: 在 "Account" 页面找到

5. **更新代码**
   - 打开 `contact-form.js` 文件
   - 替换以下值：
     ```javascript
     const serviceID = 'YOUR_SERVICE_ID';        // 替换为您的 Service ID
     const templateID = 'YOUR_TEMPLATE_ID';      // 替换为您的 Template ID
     const publicKey = 'YOUR_PUBLIC_KEY';        // 替换为您的 Public Key
     ```

6. **添加 EmailJS SDK**
   - 在 `index.html` 的 `</head>` 标签前添加：
     ```html
     <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
     <script>
         emailjs.init('YOUR_PUBLIC_KEY');
     </script>
     ```

### 方法2: Formspree

**优点：**
- 免费额度：50封/月
- 无需注册邮件服务
- 设置更简单

**设置步骤：**

1. **注册 Formspree 账户**
   - 访问 [https://formspree.io/](https://formspree.io/)
   - 注册免费账户

2. **创建表单**
   - 登录后，点击 "New Form"
   - 设置表单名称和接收邮箱
   - 获取表单 ID

3. **更新代码**
   - 打开 `contact-form.js` 文件
   - 替换以下值：
     ```javascript
     const formspreeEndpoint = 'https://formspree.io/f/YOUR_FORM_ID';
     ```

## 🔧 当前配置

- **接收邮箱**: xian@longbo.cloud
- **表单字段**: 姓名、邮箱、主题、消息
- **验证**: 客户端验证 + 服务端验证

## 📝 测试建议

1. **本地测试**
   - 在浏览器中打开网站
   - 填写联系表单
   - 检查控制台是否有错误

2. **邮件接收测试**
   - 发送测试邮件
   - 检查垃圾邮件文件夹
   - 确认邮件格式正确

## 🚀 高级配置

### 自定义邮件模板 (EmailJS)

```html
<!-- 邮件模板示例 -->
<div style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto;">
    <h2>新联系表单消息</h2>
    <p><strong>发件人:</strong> {{from_name}} ({{from_email}})</p>
    <p><strong>主题:</strong> {{subject}}</p>
    <hr>
    <p><strong>消息内容:</strong></p>
    <p style="white-space: pre-wrap;">{{message}}</p>
    <hr>
    <p><small>此邮件来自您的个人网站联系表单</small></p>
</div>
```

### 添加更多字段

如果需要添加更多表单字段，请：

1. 更新 HTML 表单
2. 更新 `getFormData()` 方法
3. 更新邮件模板变量

## 🛠️ 故障排除

### 常见问题

1. **邮件发送失败**
   - 检查 API 密钥是否正确
   - 确认邮箱服务已正确连接
   - 查看浏览器控制台错误信息

2. **邮件进入垃圾箱**
   - 设置 SPF 记录
   - 配置 DKIM
   - 在邮件模板中添加发件人信息

3. **表单验证问题**
   - 检查 JavaScript 控制台
   - 确认所有必填字段都有验证

## 📞 技术支持

如果您在设置过程中遇到问题，可以：

1. 查看浏览器控制台错误信息
2. 检查网络连接
3. 确认 API 配置正确
4. 测试不同的邮件服务提供商

---

**注意**: 建议先使用 EmailJS 进行测试，因为它提供更好的调试信息和错误处理。


