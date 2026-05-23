# REVABOOK 系统功能地图 (FEATURE MAP)

本文件详细定义了系统功能，按 4 个主要角色 (Actors) 进行权限划分：读者 (User)、作者/出版社 (Creator)、员工 (Staff/Moderator) 和超级管理员 (Admin)。

---

## 1. 读者 / 听众 (User)
*使用移动端 App 消费内容的终端用户。*

*   **账号与个人资料 (Account & Profile)：**
    *   注册 / 登录 (邮箱, Google, Apple, Facebook)。
    *   管理个人信息、语言设置和偏好。
*   **发现内容 (Discovery / Marketplace)：**
    *   通过关键词、作者、体类搜索书籍/故事。
    *   按格式 (文字书, 漫画)、配音语言进行筛选。
    *   根据阅读/收听历史进行书籍推荐 (推荐引擎)。
*   **商店与钱包 (Store & Wallet)：**
    *   通过应用内购买 (IAP) 或支付网关为钱包充值 (硬币/积分)。
    *   购买 (Buy) 或 租赁 (Rent) 书籍/故事。
    *   查看交易记录。
*   **智能播放器 (Smart Player)：**
    *   **文字书：** 收听音频、自动滚动页面、**文本与语音同步高亮**。自定义播放速度 (0.5x - 2.0x)。
    *   **漫画：** 手动翻页模式，音频自动匹配当前页面/对话气泡。
    *   下载以供离线收听/阅读 (受 DRM 保护)。
*   **互动 (Interaction)：**
    *   评分 (Rating)、评论 (Review) 书籍。
    *   **报错 (Feedback)：** 选中错误的文本/音频片段 (翻译错误, 读错) 并向作者发送报告。

---

## 2. 作者 / 出版社 (Creator)
*创建并拥有内容版权的人员，使用 Creator Studio (Web/PC App)。*

*   **内容管理 (Content Management)：**
    *   创建新书籍项目，分类 (文字/漫画)。
    *   上传手稿 (Text/Word 文件) 或图片 (ZIP/PDF)。
    *   管理章节 (Chapters) 列表。
*   **AI Studio 与制作流程 (Production Workflow)：**
    *   激活自动分析进程 (OCR/NLP)。
    *   选择要翻译的语言 (多语言)。
    *   为每个角色分配 AI 配音。
    *   激活批量翻译与配音 (Batch Processing) 进程。
*   **交互式 AI 纠错 (Interactive AI Correction)：**
    *   查看来自读者的报错列表。
    *   **AI 聊天助手 (AI Chat Agent)：** 开启 AI 聊天窗口，下达局部纠错指令 (例如："重新翻译此句", "更换配音")。点击 "Apply" 保存并覆盖修正内容。
*   **业务与分析 (Sales & Analytics)：**
    *   设置售价、租赁价。
    *   查看统计看板：实时查看阅读量、收听量、营收。
    *   申请将营收提取 (Withdraw) 到银行账户。

---

## 3. 员工 / 审核员 (Staff / Moderator)
*系统的运营团队，使用内部管理工具 (Internal Admin Tool)。*

*   **内容审核 (Content Moderation)：**
    *   在书籍/故事上架市场前进行审核 (批准或拒绝)，检查是否侵犯版权、包含 18+ 敏感内容或暴力内容。
    *   处理来自社区的内容违规报告。
*   **客户支持 (Customer Support - CS)：**
    *   解决用户投诉 (充值错误, 无法下载书籍)。
    *   处理作者的工单 (Ticket)。
*   **质量保证 (QA - Quality Assurance)：**
    *   随机抽查 AI 翻译/配音，评估系统质量。

---

## 4. 系统管理员 (System Admin)
*拥有最高权限，管理整个平台。*

*   **全局看板 (Global Dashboard)：**
    *   监控系统健康状况 (System Health)、在线用户数、平台总营收。
*   **财务管理 (Financial Management)：**
    *   配置平台佣金比例 (例如：平台抽取 30%，作者获得 70%)。
    *   审批作者的大额提现申请。
*   **角色管理 (User & Staff Management)：**
    *   封禁/解封违规的用户或作者账号。
    *   创建员工账号，分配权限 (基于角色的访问控制 - RBAC)。
*   **系统配置 (System Config)：**
    *   管理第三方服务 (ElevenLabs, OpenAI, Stripe 等) 的 API Key。
    *   调整 AI 配置 (例如：切换 AI 模型以节省成本)。
