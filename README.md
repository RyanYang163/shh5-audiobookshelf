# Audiobookshelf

| 项 | 值 |
|---|---|
| 应用 ID | `shh5-audiobookshelf` |
| 形态 | Docker 应用（Compose） · WebUI 外开（浏览器新标签） |
| 版本 | 1.0.0 |
| 上游项目 | https://github.com/advplyr/audiobookshelf |
| 上游许可证 | GPL-3.0 |
| 宿主端口 | 18805 |

## 简介

有声书与播客服务器：自动刮削元数据、记录进度，配套 iOS/Android 客户端。

## 打包

```bash
./build.sh                # 默认 x86_64
./build.sh aarch64        # ARM（Deb 应用）
```

产物在 `build/output/`，同级生成 `<包名>.sha256`。

## 提交前必办事项

- ⚠️ 必须锁定 ≥2.33.0：2.33.0 之前存在登录页自定义消息的 Stored XSS（GHSA-cx29-ghq2-9cm4），另有 Path Traversal 记录。
- ⚠️ 官方明确「不建议使用 healthcheck」，理由是持续 ping + 自动重启会增加日志噪音。本 compose 尊重官方建议未定义 healthcheck，但若 TOS 审核强制要求，需自行补一个轻量检查。
- 需要三个挂载点：/config（SQLite）、/metadata、以及媒体目录。
- [ ] 真机安装、启动、停止、卸载残留四项实测
- [ ] 首屏加载 ≤ 5 秒（指引 H10）
- [ ] x86_64 与 aarch64 分别构建并测试（指引 H7）
- [ ] 提交前跑一遍指引 13.9 上架前自查清单

## 隐私政策

见 [PRIVACY.md](./PRIVACY.md)（对应审核项 C3–C8）。

## 许可证与出处

本仓库**仅包含 TOS 平台集成所需的配置文件与打包脚本**，应用本体的源码与二进制来自上游项目：https://github.com/advplyr/audiobookshelf

上游许可证：**%s**。本封装保留上游许可证声明，未修改上游代码（Deb 形态下按上游许可证要求随包提供 LICENSE）。

应用名称与图标为上游项目的标识；本仓库图标为自行绘制的简易图形，不含上游商标元素（对应审核项 H19）。
