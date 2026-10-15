# Zerui Liu — 个人学术主页

基于 [academicpages](https://github.com/academicpages/academicpages.github.io)（Jekyll 主题）搭建，内容取自 `cv.tex` 里的学术 CV。

## 内容写在哪

| 要改的东西 | 文件 |
|---|---|
| 站点全局设置（姓名、简介、头像、邮箱、ORCID、GitHub 等） | `_config.yml` |
| 顶栏导航 | `_data/navigation.yml` |
| 首页 | `_pages/about.md` |
| CV 页 | `_pages/cv.md` |
| 论文（一篇一个文件） | `_publications/` |
| 报告 / 会议 | `_talks/` |
| 头像 | `images/profile.jpg`（方形图片效果最好） |
| 可下载的 PDF（论文、海报等） | `files/`（放进去后 URL 是 `/files/文件名`） |

## 本地预览

需要 Ruby 3.x + Jekyll：

```sh
bundle install
bundle exec jekyll serve
# 然后打开 http://localhost:4000
```

> 注意：这台机器上只有 macOS 自带的 Ruby 2.6，没有 Jekyll，所以本次修改**没有在本地构建验证过**。
> 想本地预览就先 `brew install ruby`，或者直接推到 GitHub 让 Actions 构建。

## 部署

仓库名必须是 `<你的用户名>.github.io`，即 **`LRayleighJ.github.io`**：

```sh
git init
git add .
git commit -m "Set up personal academic website"
git branch -M master
git remote add origin git@github.com:LRayleighJ/LRayleighJ.github.io.git
git push -u origin master
```

推上去之后：仓库 **Settings → Pages → Build and deployment → Source 选 "GitHub Actions"**。
`.github/workflows/jekyll.yml` 会自动构建并发布，网址是 <https://lrayleighj.github.io>。

## 关于论文条目

- 已发表论文的 `paperurl` 目前指向 DOI 链接（点过去是出版社页面，不是直接下载 PDF）。
  `publications.txt` 里的 arXiv 编号确认对应关系之后，可以把 `paperurl` 换成 `https://arxiv.org/abs/<编号>`。
- **两篇在投/在写的论文做了脱敏处理**：只保留题目和一句话说明，
  具体数值（交叉功率、Ω_HI 约束、各项百分比等）和结果都没有写进网站，`files/` 里也没有放草稿 PDF。
  等正式发表或挂上 arXiv 之后再补数值。
- `date:` 是按出版年份和卷期推的，排序用；要精确到月份就自己改一下。

## 注意：上传 PDF 会重新暴露数值

`cv_zerui.pdf` / `cv.tex` 里保留了完整的项目细节和数值。如果以后想把 CV 的 PDF 挂到网站
（放 `files/` 并在导航或页面里链接），那些数字就会跟着一起公开 —— 在论文发表前请谨慎。

## 其他

- 报告地图（talkmap）相关文件已从构建中排除，`_config.yml` 里 `talkmap_link` 为 `false`，需要时再打开。
- `_teaching/`、`_portfolio/`、`_posts/` 三个集合目前在 `_config.yml` 里还留着配置但目录是空的，
  模板里的示例内容已经删掉了（想加教学经历/作品集/博客时直接放文件即可，或把集合配置一并删掉）。
- 模板维护用的 workflow（`scrape_talks.yml`、`bad-pr.yml`、`jekyll-build.yml`）已删除，
  `.github/workflows/` 下只剩 `jekyll.yml`（负责构建 + 部署），推送时自动触发。
