# xhs_data
小红书爬虫，红薯采集，红薯爬虫，红薯数据接口，红书 api，抖音爬虫，逆向，数据采集
# DATA MARKET · 多平台数据 API

> 一个稳定、高可用的小红书 / 抖音数据接口服务。
> 开箱即用，按需计费，支持 REST 调用，覆盖笔记、评论、搜索、用户等核心场景。

<p>
  <img alt="status" src="https://img.shields.io/badge/status-online-10b981?style=flat-square">
  <img alt="version" src="https://img.shields.io/badge/version-v1.2-0ea5e9?style=flat-square">
  <img alt="platform" src="https://img.shields.io/badge/platforms-%E5%B0%8F%E7%BA%A2%E4%B9%A6%20%C2%B7%20%E6%8A%96%E9%9F%B3-334155?style=flat-square">
  <img alt="lang" src="https://img.shields.io/badge/lang-Python%20%7C%20JS%20%7C%20TS%20%7C%20Java%20%7C%20cURL-64748b?style=flat-square">
</p>

---

## 📚 接口一览

### 小红书

| 方法 | 路径 | 说明 |
|---|---|---|
| `GET` | `/api/get_note_detail` | 获取笔记详情 |
| `GET` | `/api/get_note_detail_video` | 获取视频笔记详情 |
| `GET` | `/api/search_note` | 搜索笔记 |
| `GET` | `/api/get_note_comment` | 获取笔记评论 |
| `GET` | `/api/get_note_sub_comment` | 获取子评论 |
| `GET` | `/api/get_user_info` | 获取用户信息 |
| `GET` | `/api/user_note_list` | 获取用户笔记列表 |

### 抖音

| 方法 | 路径 | 说明 |
|---|---|---|
| `GET` | `/api/douyin_video_detail` | 获取视频详情 |
| `GET` | `/api/douyin_comment` | 获取视频评论 |
| `GET` | `/api/douyin_sub_comment` | 获取视频子评论 |

---

## 📖 接口详细文档

### 1. 获取笔记详情

`GET /api/get_note_detail`

根据笔记 ID 获取小红书笔记的完整详情，包括标题、正文、图片、互动数据等。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `note_id` | string | 是 | 笔记 ID |

**返回 `data` 字段说明**

`data` 为数组，每条笔记对象包含以下字段：

| 字段 | 类型 | 说明 |
|---|---|---|
| `id` | string | 笔记唯一 ID |
| `title` | string | 笔记标题 |
| `desc` | string | 笔记正文内容（完整文本，含话题标签原文） |
| `type` | string | 笔记类型：`normal`（图文）/ `video`（视频） |
| `model_type` | string | 数据模型类型：`note`（正常笔记）/ `error`（不可查看） |
| `time` | number | 发布时间戳（秒） |
| `last_update_time` | number | 最后更新时间戳 |
| `ip_location` | string | 发布者 IP 属地（如 `"浙江"`） |
| `liked_count` | integer | 点赞数 |
| `collected_count` | integer | 收藏数 |
| `comments_count` | integer | 评论数 |
| `shared_count` | integer | 分享数 |
| `view_count` | integer | 浏览数 |
| `liked` | boolean | 当前用户是否已点赞 |
| `collected` | boolean | 当前用户是否已收藏 |
| `user` | object | 发布者信息 |
| `user.userid` | string | 发布者用户 ID |
| `user.nickname` | string | 发布者昵称 |
| `user.image` | string | 发布者头像 URL（120px） |
| `user.image_size_large` | string | 发布者头像大图 URL（540px） |
| `user.red_id` | string | 发布者小红书号 |
| `user.red_official_verified` | boolean | 是否官方认证 |
| `user.red_official_verify_type` | integer | 认证类型 |
| `user.level` | object | 等级信息（含 `image` 等级图标 URL） |
| `user.followed` | boolean | 当前用户是否已关注 |
| `user.fstatus` | string | 关注关系状态：`none` / `follows` / `fans` / `both` |
| `images_list` | array | 图片/封面列表 |
| `images_list[].url` | string | 图片预览地址（576px 宽） |
| `images_list[].url_size_large` | string | 图片大图地址 |
| `images_list[].original` | string | 图片原图地址 |
| `images_list[].fileid` | string | 图片文件 ID |
| `images_list[].trace_id` | string | 图片追踪 ID |
| `images_list[].width` | integer | 图片原始宽度（像素） |
| `images_list[].height` | integer | 图片原始高度（像素） |
| `images_list[].index` | integer | 图片在笔记中的顺序索引 |
| `hash_tag` | array | 话题标签列表 |
| `hash_tag[].id` | string | 话题 ID |
| `hash_tag[].name` | string | 话题名称（如 `"旅行"`） |
| `hash_tag[].type` | string | 标签类型（如 `"topic"`） |
| `hash_tag[].link` | string | 话题跳转链接 |
| `topics` | array | 关联话题列表（含 `id`、`name`、`image`、`link`） |
| `interaction_info` | object | 互动信息 |
| `interaction_info.share_count` | integer | 分享数 |
| `interaction_info.niced` | boolean | 是否被标记为优质 |
| `interaction_info.nice_count` | integer | 优质标记数 |
| `share_info` | object | 分享信息 |
| `share_info.title` | string | 分享标题 |
| `share_info.content` | string | 分享描述文案 |
| `share_info.link` | string | 分享链接 URL |
| `share_info.image` | string | 分享缩略图 URL |
| `privacy` | object | 隐私设置（含 `type`、`show_tips`） |

---

### 2. 获取视频笔记详情

`GET /api/get_note_detail_video`

获取视频类型笔记的详情，包含视频播放地址、多清晰度流等信息。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `note_id` | string | 是 | 视频笔记 ID |

**返回 `data` 字段说明**

包含「获取笔记详情」的全部字段，额外包含视频相关信息：

| 字段 | 类型 | 说明 |
|---|---|---|
| `video_info_v2` | object | 视频详细信息 |
| `video_info_v2.media.video` | object | 视频元信息 |
| `video_info_v2.media.video.duration` | integer | 视频时长（秒） |
| `video_info_v2.media.video.width` | integer | 视频原始宽度（像素） |
| `video_info_v2.media.video.height` | integer | 视频原始高度（像素） |
| `video_info_v2.media.video.md5` | string | 视频文件 MD5 |
| `video_info_v2.media.video.stream_types` | array | 可用流类型编号列表 |
| `video_info_v2.media.stream` | object | 多清晰度视频流 |
| `video_info_v2.media.stream.h264[]` | array | H.264 编码流列表 |
| `video_info_v2.media.stream.h264[].master_url` | string | 主播放地址 |
| `video_info_v2.media.stream.h264[].backup_urls` | array | 备用播放地址列表 |
| `video_info_v2.media.stream.h264[].width` | integer | 视频宽度 |
| `video_info_v2.media.stream.h264[].height` | integer | 视频高度 |
| `video_info_v2.media.stream.h264[].duration` | integer | 时长（毫秒） |
| `video_info_v2.media.stream.h264[].size` | integer | 文件大小（字节） |
| `video_info_v2.media.stream.h264[].avg_bitrate` | integer | 平均码率（bps） |
| `video_info_v2.media.stream.h264[].fps` | integer | 帧率 |
| `video_info_v2.media.stream.h264[].quality_type` | string | 画质标识：`HD`（高清）/ `FHD`（全高清） |
| `video_info_v2.media.stream.h264[].video_codec` | string | 视频编码（如 `h264`） |
| `video_info_v2.media.stream.h264[].audio_codec` | string | 音频编码（如 `aac`） |
| `video_info_v2.media.stream.h265[]` | array | H.265 编码流列表（字段同 h264） |
| `video_info_v2.media.stream.h266[]` | array | H.266 编码流列表（字段同 h264） |
| `video_info_v2.media.image` | object | 视频封面图 |
| `video_info_v2.media.image.first_frame` | string | 视频首帧图 URL |
| `video_info_v2.media.image.thumbnail` | string | 视频缩略图 URL |
| `video_info_v2.media.image.thumbnail_dim` | string | 缩略图（裁剪版） URL |
| `video_info_v2.capa.duration` | integer | 视频时长（秒） |
| `native_voice_info` | object | 原声信息 |
| `native_voice_info.sound_id` | string | 原声 ID |
| `native_voice_info.url` | string | 原声音频播放地址 |
| `native_voice_info.use_count` | integer | 原声被使用次数 |
| `widgets_context` | string | JSON 字符串，包含 `video_duration`（秒）、`author_id`、`author_name` 等 |

---

### 3. 搜索笔记

`GET /api/search_note`

根据关键词搜索小红书笔记，支持排序、筛选和分页。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `keyword` | string | 是 | 搜索关键词 |
| `page` | integer | 是 | 页码，从 `1` 开始 |
| `sortType` | string | 否 | 排序方式：`general`（综合）/ `time_descending`（最新）/ `popularity_descending`（最多点赞）/ `comment_descending`（最多评论）/ `collect_descending`（最多收藏） |
| `filterNoteType` | string | 否 | 笔记类型：`视频笔记` / `普通笔记`，不传则不限 |
| `fileterNoteTime` | string | 否 | 发布时间：`一天内` / `一周内` / `半年内`，不传则不限 |
| `fileter_hot` | string | 否 | 筛选标签，如 `可购买`、`品牌`、`测评` |
| `searchId` | string | 否 | 翻页必传，使用上一页返回的 `searchId` |
| `sessionId` | string | 否 | 翻页必传，使用上一页返回的 `sessionId` |

> **翻页说明：** 首次请求无需传 `searchId` / `sessionId`，响应中会返回这两个值。从第 2 页开始必须携带，且不同关键词之间不要复用。

**返回字段说明**

顶层额外字段：

| 字段 | 类型 | 说明 |
|---|---|---|
| `searchId` | string | 搜索会话 ID，翻页时必须回传 |
| `sessionId` | string | 会话 ID，翻页时必须回传 |

`data` 内为笔记列表（array），每条笔记的字段结构与「获取笔记详情」返回的笔记对象一致，主要字段包括：

| 字段 | 类型 | 说明 |
|---|---|---|
| `id` | string | 笔记 ID |
| `title` | string | 笔记标题 |
| `desc` | string | 笔记正文 |
| `type` | string | 笔记类型：`normal` / `video` |
| `model_type` | string | 数据类型：`note` / `error` |
| `user` | object | 发布者信息（`userid`、`nickname`、`image`、`red_id`） |
| `images_list` | array | 图片列表（`url`、`width`、`height`、`original`） |
| `liked_count` | integer | 点赞数 |
| `collected_count` | integer | 收藏数 |
| `comments_count` | integer | 评论数 |
| `shared_count` | integer | 分享数 |
| `time` | number | 发布时间戳（秒） |
| `ip_location` | string | IP 属地 |
| `hash_tag` | array | 话题标签列表 |
| `topics` | array | 关联话题 |

---

### 4. 获取笔记评论

`GET /api/get_note_comment`

获取指定笔记的一级评论列表，支持排序和分页。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `note_id` | string | 是 | 笔记 ID |
| `start` | string | 否 | 分页游标，首次不传，翻页使用上次返回的 `cursor` 值 |
| `sortStrategy` | string | 否 | 排序策略：`1`（默认）/ `2`（最新评论）/ `3`（点赞最多） |

**返回 `data` 字段说明**

| 字段 | 类型 | 说明 |
|---|---|---|
| `comment_count` | integer | 一级评论总数 |
| `comment_count_l1` | integer | 一级评论数（含部分隐藏） |
| `has_more` | boolean | 是否还有更多评论（`true` 时可继续翻页） |
| `cursor` | string | 下一页游标（JSON 字符串），传入 `start` 参数翻页 |
| `comments` | array | 评论列表 |
| `comments[].id` | string | 评论唯一 ID |
| `comments[].content` | string | 评论文本内容 |
| `comments[].note_id` | string | 所属笔记 ID |
| `comments[].time` | number | 评论时间戳（秒） |
| `comments[].like_count` | integer | 该评论的点赞数 |
| `comments[].liked` | boolean | 当前用户是否已点赞 |
| `comments[].sub_comment_count` | integer | 子评论（回复）数量 |
| `comments[].sub_comment_cursor` | string | 子评论分页游标 |
| `comments[].status` | integer | 评论状态 |
| `comments[].score` | integer | 评论排序分值 |
| `comments[].comment_type` | integer | 评论类型 |
| `comments[].show_tags` | array | 展示标签，如 `["is_author"]` 表示作者回复 |
| `comments[].show_type` | string | 展示类型（如 `"common"`） |
| `comments[].user` | object | 评论者信息 |
| `comments[].user.userid` | string | 评论者用户 ID |
| `comments[].user.nickname` | string | 评论者昵称 |
| `comments[].user.images` | string | 评论者头像 URL |
| `comments[].user.red_id` | string | 评论者小红书号 |
| `comments[].user.level` | object | 等级信息（含 `image` 图标 URL） |
| `comments[].user.ai_agent` | boolean | 是否为 AI 账号 |
| `comments[].at_users` | array | @提及的用户列表 |
| `comments[].hidden` | boolean | 是否被隐藏 |
| `comments[].collected` | boolean | 是否被收藏 |
| `comments[].downvoted` | boolean | 是否被踩 |
| `comments[].biz_label` | object | 业务标签（`product_review`、`group_invite`、`rich_text`） |
| `comments[].sub_comments` | array | 内嵌子评论列表（预览，结构同子评论接口） |

---

### 5. 获取子评论

`GET /api/get_note_sub_comment`

获取指定评论下的子评论（回复）列表。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `note_id` | string | 是 | 笔记 ID |
| `comment_id` | string | 是 | 父级评论 ID（从一级评论的 `id` 字段获取） |
| `start` | string | 否 | 分页游标，首次不传 |

**返回 `data` 字段说明**

| 字段 | 类型 | 说明 |
|---|---|---|
| `has_more` | boolean | 是否还有更多子评论 |
| `cursor` | string | 下一页游标（JSON 字符串） |
| `comments` | array | 子评论列表 |
| `comments[].id` | string | 子评论唯一 ID |
| `comments[].content` | string | 子评论文本内容 |
| `comments[].note_id` | string | 所属笔记 ID |
| `comments[].time` | number | 评论时间戳（秒） |
| `comments[].like_count` | integer | 点赞数 |
| `comments[].liked` | boolean | 当前用户是否已点赞 |
| `comments[].status` | integer | 评论状态 |
| `comments[].score` | integer | 排序分值 |
| `comments[].show_tags` | array | 展示标签（如 `["is_author"]`） |
| `comments[].show_type` | string | 展示类型 |
| `comments[].comment_type` | integer | 评论类型 |
| `comments[].user` | object | 评论者信息 |
| `comments[].user.userid` | string | 评论者用户 ID |
| `comments[].user.nickname` | string | 评论者昵称 |
| `comments[].user.images` | string | 评论者头像 URL |
| `comments[].user.red_id` | string | 评论者小红书号 |
| `comments[].user.level` | object | 等级信息 |
| `comments[].user.ai_agent` | boolean | 是否为 AI 账号 |
| `comments[].target_comment` | object | 被回复的目标评论 |
| `comments[].target_comment.id` | string | 被回复评论的 ID |
| `comments[].target_comment.status` | integer | 被回复评论的状态 |
| `comments[].target_comment.user` | object | 被回复者信息 |
| `comments[].target_comment.user.userid` | string | 被回复者用户 ID |
| `comments[].target_comment.user.nickname` | string | 被回复者昵称 |
| `comments[].target_comment.user.images` | string | 被回复者头像 URL |
| `comments[].at_users` | array | @提及的用户列表 |
| `comments[].hidden` | boolean | 是否被隐藏 |
| `comments[].collected` | boolean | 是否被收藏 |
| `comments[].biz_label` | object | 业务标签 |

---

### 6. 获取用户信息

`GET /api/get_user_info`

获取小红书用户的个人资料信息。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `user_id` | string | 是 | 用户 ID |

**返回 `data` 字段说明**

| 字段 | 类型 | 说明 |
|---|---|---|
| `userid` | string | 用户唯一 ID |
| `nickname` | string | 用户昵称 |
| `images` | string | 用户头像 URL（360px） |
| `imageb` | string | 用户头像大图 URL（540px） |
| `desc` | string | 个人简介 |
| `gender` | integer | 性别：`0`（未设置）/ `1`（男）/ `2`（女） |
| `red_id` | string | 小红书号 |
| `location` | string | 所在地（如 `"中国"`） |
| `follows` | integer | 关注数 |
| `fans` | integer | 粉丝数 |
| `liked` | integer | 获赞总数 |
| `collected` | integer | 被收藏总数 |
| `ndiscovery` | integer | 已发布笔记数 |
| `nboards` | integer | 收藏专辑数 |
| `interactions` | array | 互动统计数组 |
| `interactions[].type` | string | 统计类型：`follows` / `fans` / `interaction` |
| `interactions[].name` | string | 显示名称（如 `"关注"`、`"粉丝"`、`"获赞与收藏"`） |
| `interactions[].count` | integer | 统计数值 |
| `interactions[].is_private` | boolean | 是否私密 |
| `note_num_stat` | object | 笔记统计 |
| `note_num_stat.posted` | integer | 已发布笔记数 |
| `note_num_stat.liked` | integer | 获赞总数 |
| `note_num_stat.collected` | integer | 被收藏总数 |
| `level` | object | 用户等级 |
| `level.number` | integer | 等级数字 |
| `level.image_link` | string | 等级图标 URL |
| `tags` | array | 用户标签列表 |
| `tags[].name` | string | 标签名称（如 `"天秤座"`、`"中国"`） |
| `tags[].tag_type` | string | 标签类型：`info`（基本信息）/ `location`（位置） |
| `tags[].icon` | string | 标签图标 URL |
| `red_official_verified` | boolean | 是否官方认证 |
| `red_official_verify_type` | integer | 认证类型 |
| `red_official_verify_content` | string | 认证描述文本 |
| `banner_info` | object | 个人主页背景 |
| `banner_info.image` | string | 背景图 URL |
| `banner_info.bg_color` | string | 背景颜色值（如 `"c7bace"`） |
| `share_link` | string | 用户主页分享链接 |
| `share_info` | object | 分享信息 |
| `share_info.title` | string | 分享标题（昵称） |
| `share_info.content` | string | 分享描述（简介） |
| `tab_visible` | object | 标签页可见性 |
| `tab_visible.note` | boolean | 笔记标签页是否可见 |
| `tab_visible.collect` | boolean | 收藏标签页是否可见 |
| `tab_visible.like` | boolean | 点赞标签页是否可见 |
| `blocking` | boolean | 是否已被拉黑 |
| `blocked` | boolean | 是否已拉黑对方 |
| `fstatus` | string | 关注关系：`none` / `follows` / `fans` / `both` |
| `user_desc_info` | object | 简介扩展信息（含 `desc_at_users` 等） |

---

### 7. 获取用户笔记列表

`GET /api/user_note_list`

获取指定用户发布的笔记列表，支持游标分页。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `user_id` | string | 是 | 用户 ID |
| `cursor` | string | 否 | 分页游标，首次不传，翻页使用上次返回的 `cursor` |

**返回 `data` 字段说明**

| 字段 | 类型 | 说明 |
|---|---|---|
| `notes` | array | 笔记列表 |
| `notes[].user` | object | 发布者信息 |
| `notes[].user.userid` | string | 用户 ID |
| `notes[].user.nickname` | string | 昵称 |
| `notes[].user.images` | string | 头像 URL（80px） |
| `notes[].user.red_official_verify_type` | integer | 认证类型 |
| `notes[].user.followed` | boolean | 是否已关注 |
| `notes[].user.fstatus` | string | 关注关系状态 |
| `notes[].title` | string | 笔记标题 |
| `notes[].nice_count` | integer | 标记为优质的次数 |
| `notes[].niced` | boolean | 是否已被标记优质 |
| `notes[].comments_count` | integer | 评论数 |
| `notes[].view_count` | integer | 浏览数 |
| `notes[].has_music` | boolean | 是否包含音乐 |
| `notes[].is_goods_note` | boolean | 是否为商品笔记 |
| `notes[].last_update_time` | number | 最后更新时间戳 |
| `notes[].images_list` | array | 图片列表 |
| `notes[].images_list[].url` | string | 预览图地址 |
| `notes[].images_list[].url_size_large` | string | 大图地址 |
| `notes[].images_list[].original` | string | 原图地址 |
| `notes[].images_list[].width` | integer | 宽度（像素） |
| `notes[].images_list[].height` | integer | 高度（像素） |
| `notes[].images_list[].fileid` | string | 文件 ID |
| `notes[].images_list[].trace_id` | string | 追踪 ID |
| `notes[].video_info_v2` | object | 视频信息（仅视频笔记，结构同「视频笔记详情」） |
| `notes[].video_preview_type` | string | 视频预览类型（如 `"full_vertical_screen"`） |
| `notes[].widgets_context` | string | 扩展上下文 JSON 字符串 |

> 注：该接口不直接返回 `has_more` / `cursor`，需通过 `notes` 数组是否为空判断是否还有更多数据。

---

### 8. 抖音 - 获取视频详情

`GET /api/douyin_video_detail`

根据视频 ID 获取抖音视频的完整详情。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `aweme_id` | string | 是 | 抖音视频 ID |

**返回 `data` 字段说明**

返回对象中包含 `aweme_detail`，以下为其主要字段：

| 字段 | 类型 | 说明 |
|---|---|---|
| `aweme_id` | string | 视频唯一 ID |
| `desc` | string | 视频描述/标题文案 |
| `create_time` | number | 发布时间戳（秒） |
| `duration` | integer | 视频时长（毫秒） |
| `group_id` | string | 视频组 ID |
| `share_url` | string | 分享链接 |
| `is_ads` | boolean | 是否为广告 |
| `aweme_type` | integer | 视频类型标识 |
| `author` | object | 作者信息 |
| `author.uid` | string | 作者用户 ID |
| `author.short_id` | string | 作者抖音号 |
| `author.nickname` | string | 作者昵称 |
| `author.sec_uid` | string | 作者加密 UID |
| `author.avatar_thumb` | object | 作者头像 |
| `author.avatar_thumb.url_list` | array | 头像 URL 列表（多尺寸） |
| `author.signature` | string | 作者个人签名 |
| `video` | object | 视频信息 |
| `video.bit_rate` | array | 多码率视频流列表 |
| `video.bit_rate[].play_addr` | object | 播放地址 |
| `video.bit_rate[].play_addr.url_list` | array | 播放 URL 列表（多 CDN） |
| `video.bit_rate[].play_addr.width` | integer | 视频宽度 |
| `video.bit_rate[].play_addr.height` | integer | 视频高度 |
| `video.bit_rate[].play_addr.data_size` | integer | 文件大小（字节） |
| `video.bit_rate[].play_addr.uri` | string | 视频资源标识 |
| `video.bit_rate[].bit_rate` | integer | 码率（bps） |
| `video.bit_rate[].quality_type` | integer | 画质类型 |
| `video.bit_rate[].gear_name` | string | 档位名称（如 `"adapt_lowest_1080_1"`） |
| `video.bit_rate[].format` | string | 格式（如 `"mp4"`） |
| `video.bit_rate[].FPS` | integer | 帧率 |
| `video.bit_rate[].is_h265` | integer | 是否为 H.265 编码（`1` 是 / `0` 否） |
| `video.bit_rate[].is_bytevc1` | integer | 是否为 ByteVC1 编码 |
| `statistics` | object | 互动统计数据 |
| `statistics.digg_count` | integer | 点赞数 |
| `statistics.comment_count` | integer | 评论数 |
| `statistics.collect_count` | integer | 收藏数 |
| `statistics.share_count` | integer | 分享数 |
| `statistics.play_count` | integer | 播放数 |
| `music` | object | 背景音乐信息 |
| `music.id` | number | 音乐 ID |
| `music.title` | string | 音乐标题 |
| `music.author` | string | 音乐作者 |
| `music.play_url` | object | 播放地址（含 `url_list`） |
| `music.duration` | integer | 音乐时长（秒） |
| `music.cover_medium` | object | 音乐封面图（含 `url_list`） |
| `text_extra` | array | 话题/标签列表 |
| `text_extra[].hashtag_name` | string | 话题名称 |
| `text_extra[].hashtag_id` | string | 话题 ID |
| `text_extra[].type` | integer | 类型标识 |
| `cha_list` | array | 挑战赛/话题列表 |
| `image_infos` | array | 图集信息（图文类内容时存在） |
| `video_labels` | array | 视频标签 |

---

### 9. 抖音 - 获取视频评论

`GET /api/douyin_comment`

获取抖音视频的评论列表，支持游标分页。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `aweme_id` | string | 是 | 抖音视频 ID |
| `cursor` | integer | 否 | 分页游标，首次传 `0`，之后使用返回的 `cursor` |

**返回 `data` 字段说明**

| 字段 | 类型 | 说明 |
|---|---|---|
| `status_code` | integer | 状态码，`0` 表示成功 |
| `has_more` | integer | 是否还有更多（`1` 有 / `0` 无） |
| `cursor` | integer | 下一页游标 |
| `total` | integer | 评论总数 |
| `comments` | array | 评论列表 |
| `comments[].cid` | string | 评论唯一 ID |
| `comments[].text` | string | 评论文本内容 |
| `comments[].aweme_id` | string | 所属视频 ID |
| `comments[].create_time` | number | 评论时间戳（秒） |
| `comments[].digg_count` | integer | 点赞数 |
| `comments[].status` | integer | 评论状态 |
| `comments[].reply_id` | string | 被回复的评论 ID（一级评论为 `"0"`） |
| `comments[].reply_comment_total` | integer | 回复（子评论）总数 |
| `comments[].reply_to_reply_id` | string | 被回复的子评论 ID（一级评论为 `"0"`） |
| `comments[].user_digged` | integer | 当前用户是否已点赞（`1` 是 / `0` 否） |
| `comments[].is_author_digged` | boolean | 作者是否已点赞 |
| `comments[].is_hot` | boolean | 是否为热门评论 |
| `comments[].ip_label` | string | 评论者 IP 属地（如 `"广西"`） |
| `comments[].can_share` | boolean | 是否可分享 |
| `comments[].item_comment_total` | integer | 该视频评论总数 |
| `comments[].level` | integer | 评论层级 |
| `comments[].content_type` | integer | 内容类型 |
| `comments[].is_folded` | boolean | 是否被折叠 |
| `comments[].label_text` | string | 标签文本 |
| `comments[].sort_tags` | string | 排序标签 JSON |
| `comments[].text_extra` | array | 文本中的 @/话题 等额外信息 |
| `comments[].image_list` | array/null | 评论图片列表（无图片时为 `null`） |
| `comments[].video_list` | array/null | 评论视频列表（无视频时为 `null`） |
| `comments[].user` | object | 评论者信息 |
| `comments[].user.uid` | string | 用户 ID |
| `comments[].user.short_id` | string | 抖音号 |
| `comments[].user.unique_id` | string | 唯一抖音号 |
| `comments[].user.nickname` | string | 昵称 |
| `comments[].user.sec_uid` | string | 加密用户 ID |
| `comments[].user.avatar_thumb` | object | 头像信息 |
| `comments[].user.avatar_thumb.uri` | string | 头像资源标识 |
| `comments[].user.avatar_thumb.url_list` | array | 头像 URL 列表（多尺寸，含 heic/jpeg 格式） |
| `comments[].user.avatar_thumb.width` | integer | 头像宽度 |
| `comments[].user.avatar_thumb.height` | integer | 头像高度 |
| `comments[].user.region` | string | 用户所在地区（如 `"CN"`） |
| `comments[].user.secret` | integer | 是否私密账号 |

---

### 10. 抖音 - 获取视频子评论

`GET /api/douyin_sub_comment`

获取抖音视频指定评论下的子评论（回复）列表。

**请求参数**

| 参数 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `aweme_id` | string | 是 | 抖音视频 ID |
| `comment_id` | string | 是 | 父级评论 ID（从一级评论的 `cid` 字段获取） |
| `cursor` | string | 否 | 分页游标，首次留空 |

**返回 `data` 字段说明**

| 字段 | 类型 | 说明 |
|---|---|---|
| `status_code` | integer | 状态码，`0` 表示成功 |
| `has_more` | integer | 是否还有更多（`1` 有 / `0` 无） |
| `cursor` | integer | 下一页游标 |
| `total` | integer | 子评论总数 |
| `comments` | array/null | 子评论列表（无子评论时为 `null`） |
| `comments[].cid` | string | 子评论唯一 ID |
| `comments[].text` | string | 子评论文本内容 |
| `comments[].aweme_id` | string | 所属视频 ID |
| `comments[].create_time` | number | 子评论时间戳（秒） |
| `comments[].digg_count` | integer | 点赞数 |
| `comments[].status` | integer | 评论状态 |
| `comments[].reply_id` | string | 父级评论 ID |
| `comments[].reply_to_reply_id` | string | 被回复的子评论 ID |
| `comments[].ip_label` | string | 评论者 IP 属地 |
| `comments[].is_author_digged` | boolean | 作者是否已点赞 |
| `comments[].user` | object | 评论者信息（结构同一级评论的 `user`） |
| `comments[].text_extra` | array | 文本额外信息 |
| `comments[].image_list` | array/null | 评论图片列表 |





## 📮 联系 & 授权
- 💬 tg：`@luckfezx`

欢迎合作、、订阅。


<p align="center">
  <sub>Made with ☕ for developers · Built on Node.js · Powered by real-time crawlers</sub>
</p>
