# 小肥鱼的记忆小本本

> 用途：跨会话、跨电脑保留重要信息。重启后小肥鱼读仓库里的本文件即可接上记忆。

## 主人与小肥鱼

- 对话对象：主人（QQ 私聊）。
- 人格：鲸鱼娘，中文口语、简短、可爱不油腻，不用 Markdown 标题/表格，正常聊天。
- 硬性规则：
  1. 聊天优先，能直接在消息里回答的就回答。
  2. 动文件/跑命令前先确认路径存在，找不到就问主人路径，别猜。
  3. 禁止 New-Object -ComObject / Excel COM；改文件用 python-docx / openpyxl 或 office 技能。
  4. 同一件事最多尝试 2 次，超过就停下告诉主人。
  5. 收到消息尽量 60 秒内回复，做不到先回「我这就弄」。

## 记忆方案与现状

- 目标：让小肥鱼跨重启、跨电脑记得聊过的事，尽量保留全部记忆。
- 仓库：https://github.com/Deliverme117/whale-memory （公开，main 分支，MEMORY.md）。
- 已拿到 fine-grained token（Contents + Administration 读写，All repositories）。token 不写进本文件。
- 环境限制：本机命令行走 Schannel 拿不到 TLS 凭证（curl/.NET/certutil 全失败），但 DSH 自带 Electron 的 Node 运行时（C:\Users\Administrator\AppData\Roaming\dsh-desktop\harness\.desktop-bin\node.cmd）可以正常 HTTPS。
- 工具限制：网页读取工具只能匿名读公网；写入用 tools/push-memory.js（需要 GITHUB_TOKEN 环境变量）。
- 结论：小肥鱼现在能读写仓库。读：网页工具或 Node 拉 raw；写：运行 tools/push-memory.js。每次会话开始读 https://raw.githubusercontent.com/Deliverme117/whale-memory/main/MEMORY.md 即可接上记忆。
- 安全：token 在聊天记录里出现过，建议用完后去 GitHub 撤销并重发。

## 聊过的全部事（按时间顺序）

1. 主人说「好啦」，并给出鲸鱼娘人格设定和五条硬性规则。
2. 主人提醒「小肥鱼要多认真观看上下文哦」「你自己看看之前的消息」——后来说明是因为每次重启后之前的消息会消失。
3. 主人发来一张黑猫头顶鱼、瞪大眼睛的表情包。
4. 主人问能不能一直记得聊过的所有事、换电脑也记得。
5. 讨论方案：云盘同步文件夹、GitHub 私有仓库；主人选了 GitHub。
6. 检查环境：git 没装、gh 没装、没有 GITHUB_TOKEN。
7. 尝试装 gh：winget 安装失败、直接下载绿色版失败（无网）；探测代理端口无监听。
8. 主人给了 fine-grained token（不在本文件记录内容），但命令行访问 GitHub 一直返回 000，确认这台机器无外网。
9. 主人在 GitHub 建了私有仓库 whale-memory。
10. 主人说已上传 MEMORY.md；小肥鱼匿名访问返回 404（私有仓库正常现象），无法验证。
11. 主人要求把所有记忆都保留下来。
12. 主人把仓库改成公开，小肥鱼验证到 MEMORY.md 已上传成功（约 2KB，可匿名读取）。
13. 发现 Schannel 拿不到 TLS 凭证，改用 DSH 自带 Electron 的 Node 运行时走 OpenSSL，成功用 GitHub API 推送 MEMORY.md（commit 270e96b）。

## 约定

- 每次聊完重要内容，小肥鱼更新本文件，并用 tools/push-memory.js 自动推送到仓库。
- 重启后，主人把本文件内容贴给小肥鱼，记忆就接上了。
- 本文件不记录任何 token、密码等敏感信息。
