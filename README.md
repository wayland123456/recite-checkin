# 高三英语背诵打卡

1 班 / 18 班英语背诵打卡页。学生手机打开 → 选班级 → 点自己名字 → 点今天背的那一组，即完成打卡。

- **背诵内容**：3500词乱序版（40 组）、写作100句（20 组）
- **教师后台**：页面底部「教师入口」，口令见 `index.html` 里的 `CONFIG.adminPin`（默认 `8888`），
  支持筛选（今日未打卡 / 零进度 / 按连续天数）+ 导出 Excel（CSV）
- **单文件零依赖**：全部逻辑在 `index.html` 内，无 CDN、无构建、无外部图片

## 怎么改名单

打开 `index.html`，找到顶部的 `CONFIG.classes`：

```js
classes: {
  '1':  { label: '高三(1)班',  students: [ '01 敖雪婷', '02 杨夏添', /* ... */ ] },
  '18': { label: '高三(18)班', students: [ '01 代湘语', '02 周琳涵', /* ... */ ] }
},
```

- 名字前加 `01 ` 会自动拆成学号单独显示
- **同名学生**要区分开写，例如 `'10 余欣怡（大）'` / `'20 余欣怡（小）'`。
  系统按「学号 + 姓名」认人，同名只要学号不同就不会串记录
- 组数在 `CONFIG.contents` 里改 `total` 即可

## 数据存在哪

未配置云端时，打卡记录存在**学生自己手机的浏览器本地**（localStorage，键名 `en_checkin_v1`）。
也就是说学生之间的数据不互通，教师后台只能看到当前设备上的记录。

要让全班数据汇总到教师后台，需在 `CONFIG.supabase` 填入 Supabase 项目的 `url` 与 `key`
（anon key），并在 Supabase 建一张 `checkins` 表（`cls / student / content / grp / d`，
其中 `cls,student,content,grp` 建联合唯一约束）。

## 说明

页面已设置 `<meta name="robots" content="noindex,nofollow,noarchive">`，避免被搜索引擎收录。
