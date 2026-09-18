# 战备数据包（HD2 自定义战备地址）

这是「Helldivers2 Call For Stratagems On Phone」客户端可以使用的**自定义战备数据库**。

包含绝地潜兵 2（Helldivers 2）截至 2026-09-18 的全部 109 个战备，以及清单文件。

## 目录结构



```
stratagem-host/

├── index.html                 ← 落地页（托管后浏览器打开可见，建议保留）

├── index.json                 ← 战备地址指向这个文件（清单）

└── database/

&#x20;   ├── stratagem\_db.json      ← 战备数据（客户端解析的格式）

&#x20;   └── icons/                 ← 109 个战备图标（.svg）
```

## 一、托管：让手机能访问到这些文件

任选一种「静态文件托管」，把 `stratagem-host/` **里面的内容**（index.json 与 database 文件夹）

放到网站的根目录，得到形如下面的地址：



```
https://你的域名/index.json
```

推荐方式（免费、稳定、可自己随时更新）：

### 方式 A：GitHub Pages（推荐）



1. 在 GitHub 新建一个仓库（例如 `hd2-stratagems`，设为 Public）。

2. 把 `stratagem-host/` 里的 `index.json` 和 `database/` 文件夹上传到仓库根目录。

3. 仓库 `Settings → Pages → Source` 选择 `Deploy from a branch`，分支选 `main`，目录选 `/ (root)`，保存。

4. 等 1\~2 分钟，地址即：



```
https://你的GitHub用户名.github.io/hd2-stratagems/index.json
```

以后要新增战备：在「战备管理站」工具里导出新数据包，把 `index.json` 和 `database/stratagem_db.json` 覆盖上传，手机端点「更新数据库」即可。

### 方式 B：Gitee Pages / Cloudflare Pages / 任意对象存储

原理相同：只要 `https://.../index.json` 能直接打开看到 JSON，客户端就能用。

（注意不要用需要登录、带防盗链的网盘链接。）

## 二、在手机 App 里使用



1. 打开 App → `设置 > 信息 > 数据库版本`。

2. 在弹窗里选择 **自定义** 通道。

3. 把上面的 `index.json` 地址粘贴到输入框。

4. 点击 `更新数据库`，等待下载完成（会提示 `数据库更新完成`）。

> 若想回到官方数据库：同样的弹窗里选择 
>
> `绝地潜兵2`
>
>  通道再更新即可。
> 版本检查：地址中的 
>
> `date`
>
>  与手机端记录不一致时，
>
> `数据库版本`
>
>  会显示「可更新」。

## 三、以后怎么加新战备

使用配套的「战备管理站」网页工具：



1. 打开 `stratagem-studio/index.html`。

2. 点「新增战备」：填英文名、中文名、上传图标（SVG）、按方向键录入箭头序列（上 = 1 下 = 2 左 = 3 右 = 4）。

3. 点「导出数据包」下载 zip，解压后得到新的 `index.json` 与 `database/`。

4. 把新文件覆盖上传到你的托管位置 → 手机端再点一次「更新数据库」。

## 四、格式说明（给想直接改 JSON 的人）

`index.json` 清单字段：



| 字段                  | 说明                             |
| ------------------- | ------------------------------ |
| `date`              | 版本时间，手机端据此判断是否可更新（改成新时间即可触发更新） |
| `db_path`           | 战备数据文件相对路径                     |
| `icons_path`        | 图标目录相对路径                       |
| `name`              | 数据库标识（改成自己的名字，避免与官方库图标冲突）      |
| `nameEn` / `nameZh` | 显示名称                           |

`stratagem_db.json` 中每行战备为：



```
\[id, 英文名, 中文名, 图标文件名(不含.svg), "方向码JSON", 排序号]
```

方向码：`1`= 上，`2`= 下，`3`= 左，`4`= 右；例如增援为 `[1,2,4,3,1]`。

## 五、数据来源

战备数据与图标来自官方维护的 [HD2CFS-Database](https://github.com/WisteFinch/HD2CFS-Database)（MIT 许可），

图标来自 [Helldivers-2-Stratagems-icons-svg](https://github.com/nvigneux/Helldivers-2-Stratagems-icons-svg)。