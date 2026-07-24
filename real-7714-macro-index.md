# real-7714.csl 宏索引

> 源样式：GB/T 7714—2025（注释，双语），共 20 个 macro。
> bibliography 的两个 layout（默认中文 + `locale="en"` 英文）结构相同：均只直接调用 `entry-layout`，由它按 type 分派。

## 1. 宏总表

| 宏 | 用途 | 用到的 CSL 变量 | 调用的子宏 | bibliography 中被哪些 type 调用 |
|---|---|---|---|---|
| author | 主要责任者 | composer、author、illustrator、director、host、editor、editorial-director、compiler、collection-editor；container-title（条件） | — | 全部 type（standard 除外） |
| title | 题名（附类型/载体标识） | title、volume-title、scale；container-title（条件） | volume、number、entry-type-id、entry-medium-id | 全部 type |
| volume | 多卷书的卷次 | volume | — | 经 title：无 container-title 的条目；经 container-booklike：chapter 系 |
| number | 报告编号、标准号、专利申请号、档号 | call-number、number、archive_location；archive（条件） | — | 经 title：除 article / article-journal / standard 外的 type |
| entry-type-id | 文献类型标识（J、M、C 等） | archive、CSTR、DOI、URL（均作条件判断） | — | 经 title：全部 type |
| entry-medium-id | 文献载体标识（OL 等） | medium；URL、DOI（条件） | — | 经 title：全部 type |
| secondary-contributors | 其他责任者（译者） | translator | — | 期刊报纸系、chapter 系、book 系、兜底 |
| container-contributors | 图书主要责任者 | container-author、editor、editorial-director、compiler、collection-editor | — | 经 container-booklike：chapter 系 |
| container-booklike | 图书题名 | container-title | container-contributors、volume | chapter 系 |
| container-periodical | 连续出版物中的出处项 | container-title、issued、available-date、volume、issue、locator、page、number | date、locator | article-journal / article-magazine / article-newspaper |
| edition | 版本项（版次） | edition | — | chapter 系、book 系、兜底 |
| version | 版本号（数据集/软件等） | version | — | article / dataset、电子资源兜底 |
| publisher | 出版信息与页码 | publisher、publisher-place、archive、archive-place；CSTR、DOI、URL（条件） | date、locator | chapter 系、periodical、article / dataset、book 系、档案系、兜底 |
| date | 出版日期 | issued、accessed；publisher、archive（条件） | — | paper-conference（直接）；经 container-periodical / publisher：期刊报纸系、chapter 系、periodical、book 系、档案系、兜底 |
| locator | 引文页码 | locator、page | — | 同 date 的分布 |
| dimensions | 地图的尺寸 | dimensions | — | book 系（仅 map 实际输出） |
| creation-accessed-date | 创建/发布/修改日期与引用日期 | issued、accessed | — | post 系、article / dataset、电子资源兜底 |
| access | 获取和访问路径、永久标识符 | URL、CSTR、DOI | — | 全部 type |
| entry-layout | 参考文献表格式（按 type 分派的总入口） | volume、number、event-title；container-title、publisher、archive、CSTR、DOI、URL（分支条件） | author、title、secondary-contributors、container-periodical、container-booklike、edition、publisher、version、date、locator、dimensions、creation-accessed-date、access | bibliography layout 直接调用，覆盖全部 type |
| note-layout | 注释中引用的格式（首引/复引） | first-reference-note-number、locator | entry-layout | 不被 bibliography 调用（citation 专用） |

type 系简称：期刊报纸系 = article-journal / article-magazine / article-newspaper；chapter 系 = chapter / entry-dictionary / entry-encyclopedia；book 系 = book / classic / map / patent / report；post 系 = post / post-weblog / webpage；档案系 = collection / manuscript / personal_communication。

## 2. type → 宏调用顺序（bibliography layout）

| type 分支 | 宏调用顺序 |
|---|---|
| article-journal / article-magazine / article-newspaper | author → title → secondary-contributors → container-periodical → access |
| post / post-weblog / webpage | author → title → creation-accessed-date → access |
| chapter / entry-dictionary / entry-encyclopedia（须有 container-title） | author → title → secondary-contributors → container-booklike → edition → publisher → access |
| periodical | author → title → publisher → access（title 后另直取 volume 变量） |
| paper-conference | author → title → date → locator → access（与 event-title 变量组合） |
| standard | title → access（不调用 author；另直取 number 变量） |
| article / dataset | author → title → version → publisher → creation-accessed-date → access |
| book / classic / map / patent / report（须有 publisher） | author → title → secondary-contributors → edition → publisher → dimensions → access |
| collection / manuscript / personal_communication（须有 archive） | author → title → publisher → access |
| 任意 type 且有 CSTR / DOI / URL（电子资源兜底） | author → title → version → creation-accessed-date → access |
| 其他（兜底：thesis、无 container-title 的 chapter 等） | author → title → secondary-contributors → edition → publisher → access |

补充：citation（注释）layout 只调用 note-layout——首次引用走 entry-layout，复引输出 first-reference-note-number 与 locator。

---

*本索引由 AI 助手基于 CSL 源文件自动分析整理，仅作查阅参考；若与源文件有出入，以 CSL 源文件为准。*
