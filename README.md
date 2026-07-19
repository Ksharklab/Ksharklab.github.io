# 2321班全国蹭饭地图 V2

## 已实现
- GitHub Pages 公开地图
- 每位同学独立的随机编辑链接 + 6位编辑码
- 同学只能修改与该凭证绑定的一条资料
- 管理员新增、审核、删除、重置编辑链接
- 高德行政区查询：省份下所有地级市、自治州、地区和盟
- 只保存城市中心坐标，不保存宿舍、家庭地址或实时定位
- Supabase 数据库不允许浏览器直接读写，所有修改均由 Edge Function 校验

## 一、配置 Supabase
1. 创建 Supabase 免费项目。
2. 打开 SQL Editor，运行 `supabase/schema.sql`。
3. 在电脑安装 Node.js，然后在项目目录打开终端：
   ```bash
   npx supabase login
   npx supabase link --project-ref 你的项目编号
   npx supabase functions deploy
   npx supabase secrets set ADMIN_PASSWORD="设置一个足够长的管理员密码"
   ```
4. 在 Supabase 项目地址中找到：
   `https://xxxx.supabase.co`
   把它填进 `assets/config.js` 的 `SUPABASE_URL`。

## 二、配置高德地图
1. 在高德开放平台创建“Web端(JS API)”应用。
2. 创建 Key，并取得安全密钥 securityJsCode。
3. 把 Key 和安全密钥填进 `assets/config.js`。
4. 高德控制台的域名白名单填你的 GitHub Pages 域名，例如：
   `你的用户名.github.io`

## 三、上传 GitHub
把本压缩包内所有文件上传到仓库根目录。
在仓库 Settings → Pages：
- Source：Deploy from a branch
- Branch：main
- Folder：/ (root)

## 四、使用
1. 打开 `admin.html`，输入你设置的管理员密码。
2. 输入“同学01”等初始昵称并生成链接。
3. 把“专属链接”和“个人编辑码”私发给对应同学。
4. 同学填写昵称、学校、省份和地级市，并自主决定是否公开。
5. 管理员可取消审核、删除资料或重置泄露的链接。

## 安全说明
- `ADMIN_PASSWORD` 只能设置在 Supabase Secrets，绝不能写入 GitHub。
- Supabase 的 `service_role` 密钥绝不能放入网页代码。
- 专属编辑链接相当于密码，不要发在公开群聊。
- 链接泄露后，管理员点击“重置链接”，旧链接立即失效。
