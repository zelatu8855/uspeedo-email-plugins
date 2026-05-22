# 开发说明

## 目录结构

```
uspeedo-email-plugin/
├── main.py                   # 插件入口
├── manifest.yaml             # 插件清单
├── requirements.txt          # Python 依赖
├── .env.example              # 调试环境变量示例
├── .difyignore               # 打包忽略规则
├── README.md                 # 使用说明
├── PRIVACY.md                # 隐私政策
├── GUIDE.md                  # 开发指南（本文档）
├── _assets/
│   ├── icon.svg              # 图标（亮色模式）
│   └── icon-dark.svg         # 图标（暗色模式）
├── provider/
│   ├── uspeedo-email.py      # 提供者：凭证验证
│   └── uspeedo-email.yaml    # 提供者定义 + 凭证 schema
└── tools/
    ├── uspeedo-email.py      # 工具：发送邮件
    └── uspeedo-email.yaml    # 工具参数定义
```

## 本地开发调试

```bash
# 1. 安装依赖
pip install -r requirements.txt

# 2. 配置调试 .env
cp .env.example .env
# 编辑 .env, 填入 REMOTE_INSTALL_URL 和 REMOTE_INSTALL_KEY

# 3. 启动插件
python main.py
```

## 打包发布

```bash
dify-plugin plugin package ./uspeedo-email-plugin
```

## 修改说明

本项目是对 GitHub 上 [uSpeedo/uspeedo-email-dify-plugin](https://github.com/uSpeedo/uspeedo-email-dify-plugin) 的重写版本，主要改进：

- **代码简化**：减少冗余的类型检查，合并重复逻辑
- **错误处理增强**：增加 Timeout / ConnectionError 细分异常处理
- **类型注解简化**：去除不必要的泛型注解，使用更简洁的写法
- **收件人解析优化**：`TargetEmailAddress` 直接传数组而非逗号字符串
- **错误信息截断**：API 返回的 body 截断至 500 字符避免日志爆炸
