# Sphinx 国际化

[![GitHub issues](https://img.shields.io/github/issues/xinetzone/sphinx-intl-deploy)](https://github.com/xinetzone/sphinx-intl-deploy/issues) [![GitHub forks](https://img.shields.io/github/forks/xinetzone/sphinx-intl-deploy)](https://github.com/xinetzone/sphinx-intl-deploy/network) [![GitHub stars](https://img.shields.io/github/stars/xinetzone/sphinx-intl-deploy)](https://github.com/xinetzone/sphinx-intl-deploy/stargazers) [![GitHub license](https://img.shields.io/github/license/xinetzone/sphinx-intl-deploy)](https://github.com/xinetzone/sphinx-intl-deploy/blob/main/LICENSE)  ![repo size](https://img.shields.io/github/repo-size/xinetzone/sphinx-intl-deploy.svg) [![contributors](https://img.shields.io/github/contributors/xinetzone/sphinx-intl-deploy.svg)](https://github.com/xinetzone/sphinx-intl-deploy/graphs/contributors) [![watcher](https://img.shields.io/github/watchers/xinetzone/sphinx-intl-deploy.svg)](https://github.com/xinetzone/sphinx-intl-deploy/watchers) ![](https://github.com/xinetzone/sphinx-intl-deploy/actions/workflows/docs.yml/badge.svg)

本项目支持将项目文档翻译为多语言。

下面以翻译项目 [`sphinx-doc/sphinx-intl`](https://github.com/sphinx-doc/sphinx-intl.git) 为中文，展示如何配置 `.github/workflows/deploy.yml`。

## 直接使用

1. 克隆本项目后，克隆需要翻译的项目 `sphinx-doc/sphinx-intl` 以及 HTML w3css 主题：

```yaml
- name: 克隆需要翻译的项目以及 HTML w3css 主题
  run: |
    git clone https://github.com/sphinx-doc/sphinx-intl.git draft
    git clone https://github.com/xinetzone/xin-css.git draft/doc/_static/xin-css
    git clone https://github.com/xinetzone/w3css.git draft/doc/_static/w3css
```

2. 构建 Sphinx 文档：

对于 BSD/Linux 系统：

```yaml
- name: 构建 Sphinx 文档
  run: |
    cp locales/ -rf draft/doc/locale/
    cd draft/doc
    make gettext
    make -e SPHINXOPTS="-Dlanguage='zh_CN'" html
```

对于 Windows 系统的 cmd：

```yaml
- name: 构建 Sphinx 文档
  run: |
    cp locales/ -rf draft/doc/locale/
    cd draft/doc
    make gettext
    set SPHINXOPTS=-D language=zh_CN
    make html
```

对于 Windows 系统的 PowerShell：

```yaml
- name: 构建 Sphinx 文档
  run: |
    cp locales/ -rf draft/doc/locale/
    cd draft/doc
    make gettext
    Set-Item env:SPHINXOPTS "-D language=zh_CN"
    make html
```

## 集成于需要翻译的项目

如果需要集成本项目到需要翻译的项目中，只需要将本项目的 `locales/` 下的语言文件（如 `zh_CN/`）复制到该项目的文档源目录（比如 `sphinx-doc/sphinx-intl` 项目的 `doc/locale`）下即可。

## 基本功能

- 支持英译汉功能。
- 支持翻译后的内容自动化部署到 GitHub Pages。
- 可能支持其他语言直接的翻译功能。（需要实践）

## 高级功能

- [ ] 实现网站多语言切换。
- [ ] 借助 GitHub Actions 实现类似于 [Transifex](https://www.transifex.com/) 的功能，即支持：
    - 上传需要翻译的文档，并提供 `po` 在线编辑器。
    - 支持注册功能。

- [ ] 利用 AI 技术辅助 `sphinx-intl` 完成 `po` 的初始化工作。即输出的 `po` 文件不再是空字符串，而是有转换后的可能翻译不太准确的信息。

## 小技巧

`po` 文件的高亮可以使用 vscode 插件 [gettext](https://marketplace.visualstudio.com/items?itemName=mrorz.language-gettext)。