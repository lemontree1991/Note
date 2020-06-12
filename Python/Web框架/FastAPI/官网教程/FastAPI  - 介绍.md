# FastAPI

[![FastAPI](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Clogo-teal.png)](https://fastapi.tiangolo.com/)

*FastAPI framework, high performance, easy to learn, fast to code, ready for production*

[![Build Status](https://travis-ci.com/tiangolo/fastapi.svg?branch=master) ](https://travis-ci.com/tiangolo/fastapi)[![Coverage](https://img.shields.io/codecov/c/github/tiangolo/fastapi) ](https://codecov.io/gh/tiangolo/fastapi)[![Package version](https://badge.fury.io/py/fastapi.svg) ](https://pypi.org/project/fastapi)[![Join the chat at https://gitter.im/tiangolo/fastapi](https://badges.gitter.im/tiangolo/fastapi.svg)](https://gitter.im/tiangolo/fastapi?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

------

**文档**： [https://fastapi.tiangolo.com](https://fastapi.tiangolo.com/)

**源码**： https://github.com/tiangolo/fastapi

------

FastAPI 是一个用于构建 API 的现代、快速（高性能）的 web 框架，使用基于类型提示的 Python 3.6 及更高版本。

关键特性:

- **快速**：可与 **NodeJS** 和 **Go** 比肩的极高性能（归功于 Starlette 和 Pydantic）。[最快的 Python web 框架之一](https://fastapi.tiangolo.com/zh/#_11)。
- **高效编码**：提高功能开发速度约 200％ 至 300％。*
- **更少 bug**：减少约 40％ 的人为（开发者）导致错误。*
- **智能**：极佳的编辑器支持。处处皆可自动补全，减少调试时间。
- **简单**：设计的易于使用和学习，减少阅读文档时间。
- **简短**：减少代码重复。通过不同的参数声明实现丰富功能。bug 更少。
- **健壮**：生产可用级别的代码。以及自动生成的交互式文档。
- **标准化**：基于 API 的相关开放标准并完全兼容：[OpenAPI](https://github.com/OAI/OpenAPI-Specification) (以前被称为 Swagger) 和 [JSON Schema](http://json-schema.org/)。

\* 根据对某个构建线上应用的内部开发团队所进行的测试估算得出。

## 评价

"*[...] 最近我一直在使用* *FastAPI**。[...] 实际上我正在计划将其用于我所在的微软团队的所有**机器学习服务**。其中一些服务正被集成进* *Windows* *核心产品和一些* *Office* *产品。*"

Kabir Khan - **微软** [(ref)](https://github.com/tiangolo/fastapi/pull/26)

------

"***FastAPI** 让我兴奋的欣喜若狂。它太棒了！*"

Brian Okken - **[Python Bytes](https://pythonbytes.fm/episodes/show/123/time-to-right-the-py-wrongs?time_in_sec=855) 播客主持人** [(ref)](https://twitter.com/brianokken/status/1112220079972728832)

------

"*老实说，你的作品看起来非常可靠和优美。在很多方面，这就是我想让* *Hug* *成为的样子 - 看到有人实现了它真的很鼓舞人心。*"

Timothy Crosley - **[Hug](http://www.hug.rest/) 作者** [(ref)](https://news.ycombinator.com/item?id=19455465)

------

"*如果你正打算学习一个**现代框架**用来构建 REST API，来看下* *FastAPI* *[...] 它快速、易用且易于学习 [...]*"

"*我们已经将* *API* *服务切换到了* *FastAPI* *[...] 我认为你会喜欢它的 [...]*"

Ines Montani - Matthew Honnibal - **[Explosion AI](https://explosion.ai/) 创始人 - [spaCy](https://spacy.io/) 作者** [(ref)](https://twitter.com/_inesmontani/status/1144173225322143744) - [(ref)](https://twitter.com/honnibal/status/1144031421859655680)

------

"*我们采用了* *FastAPI* *来创建用于获取**预测结果**的* *REST* *服务。[用于 Ludwig]*"

Piero Molino， Yaroslav Dudin 和 Sai Sumanth Miryala - **Uber** [(ref)](https://eng.uber.com/ludwig-v0-2/)

------

## **Typer**，命令行中的 Fast API

[![img](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Clogo-margin-vector.svg)](https://typer.tiangolo.com/)

如果你正在开发一个在终端中运行的命令行应用而不是 web API，不妨试下 [**Typer**](https://typer.tiangolo.com/)。

**Typer** 是 FastAPI 的小伙伴。它打算成为**命令行中的 FastAPI**。 ⌨️ 🚀

## 依赖

Python 3.6 及更高版本

FastAPI 站在以下巨人的肩膀之上：

- [Starlette](https://www.starlette.io/)负责 web 部分。
- [Pydantic](https://pydantic-docs.helpmanual.io/)负责数据部分。

## 安装

```pip install fastapi```

你还需要一个 ASGI 服务器，生产环境可以使用 [Uvicorn](http://www.uvicorn.org/) 或者 [Hypercorn](https://gitlab.com/pgjones/hypercorn)。

```pip install uvicorn```

## 示例

### 创建

- 创建一个 `main.py` 文件并写入以下内容:

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

<details open="" style="box-sizing: inherit; user-select: text !important; margin: 1.5625em 0px; padding: 0px 0.6rem; overflow: visible; color: rgba(0, 0, 0, 0.87); font-size: 0.64rem; break-inside: avoid; background-color: var(--md-admonition-bg-color); border-left: 0.2rem solid rgb(68, 138, 255); border-radius: 0.1rem; box-shadow: rgba(0, 0, 0, 0.05) 0px 0.2rem 0.5rem, rgba(0, 0, 0, 0.1) 0px 0px 0.05rem; display: block; font-family: Roboto, -apple-system, BlinkMacSystemFont, Helvetica, Arial, sans-serif; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px;"></p><summary style="box-sizing: inherit; user-select: text !important; position: relative; margin: 0px -0.6rem; padding: 0.4rem 1.8rem 0.4rem 2rem; font-weight: 700; background-color: rgba(68, 138, 255, 0.1); display: block; min-height: 1rem; border-top-right-radius: 0.1rem; cursor: pointer;">或者使用<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: currentcolor; font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: initial; font-size: 0.85em; word-break: break-word; background-color: transparent; border-radius: initial; -webkit-box-decoration-break: clone; margin: initial; box-shadow: none;">async def</code>...</summary><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px;"></p><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px;">如果你的代码里会出现<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">async</code><span>&nbsp;</span>/<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">await</code>，应使用<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">async def</code>：</p><div class="highlight" style="box-sizing: inherit; user-select: text !important;"><pre id="__code_1" style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; position: relative; margin: 1em 0px; line-height: 1.4;"><span style="box-sizing: inherit; user-select: text !important;"></span><button class="md-clipboard md-icon" title="复制" data-clipboard-target="#__code_1 > code" style="box-sizing: inherit; user-select: text !important; -webkit-tap-highlight-color: transparent; margin: 0px; padding: 0px; font-size: inherit; background: transparent; border: 0px; position: absolute; top: 0.4rem; right: 0.5em; z-index: 1; width: 1.5em; height: 1.5em; color: var(--md-default-fg-color--lightest); border-radius: 0.1rem; cursor: pointer; transition: color 125ms ease 0s;"><svg viewBox="0 0 24 24"><path d="M19,21H8V7H19M19,5H8A2,2 0 0,0 6,7V21A2,2 0 0,0 8,23H19A2,2 0 0,0 21,21V7A2,2 0 0,0 19,5M16,1H4A2,2 0 0,0 2,3V17H4V3H16V1Z"></path></svg></button><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0.525rem 1.17647em; font-size: 0.85em; word-break: normal; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: slice; display: block; margin: 0px; overflow: auto; box-shadow: none; touch-action: auto;"><span class="kn" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">from</span> <span class="nn" style="box-sizing: inherit; user-select: text !important; color: rgb(236, 64, 122);">fastapi</span> <span class="kn" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">import</span> <span class="n" style="box-sizing: inherit; user-select: text !important;">FastAPI</span>

<span class="n" style="box-sizing: inherit; user-select: text !important;">app</span> <span class="o" style="box-sizing: inherit; user-select: text !important; color: inherit;">=</span> <span class="n" style="box-sizing: inherit; user-select: text !important;">FastAPI</span><span class="p" style="box-sizing: inherit; user-select: text !important;">()</span>


<span class="nd" style="box-sizing: inherit; user-select: text !important; color: rgb(102, 102, 102);">@app</span><span class="o" style="box-sizing: inherit; user-select: text !important; color: inherit;">.</span><span class="n" style="box-sizing: inherit; user-select: text !important;">get</span><span class="p" style="box-sizing: inherit; user-select: text !important;">(</span><span class="s2" style="box-sizing: inherit; user-select: text !important; color: rgb(13, 144, 79);">"/"</span><span class="p" style="box-sizing: inherit; user-select: text !important;">)</span>
<span class="hll" style="box-sizing: inherit; user-select: text !important; display: block; margin: 0px -1.17647em; padding: 0px 1.17647em; background-color: rgba(255, 235, 59, 0.5);"><span class="k" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">async</span> <span class="k" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">def</span> <span class="nf" style="box-sizing: inherit; user-select: text !important; color: rgb(194, 24, 91);">read_root</span><span class="p" style="box-sizing: inherit; user-select: text !important;">():</span>
</span>    <span class="k" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">return</span> <span class="p" style="box-sizing: inherit; user-select: text !important;">{</span><span class="s2" style="box-sizing: inherit; user-select: text !important; color: rgb(13, 144, 79);">"Hello"</span><span class="p" style="box-sizing: inherit; user-select: text !important;">:</span> <span class="s2" style="box-sizing: inherit; user-select: text !important; color: rgb(13, 144, 79);">"World"</span><span class="p" style="box-sizing: inherit; user-select: text !important;">}</span>


<span class="nd" style="box-sizing: inherit; user-select: text !important; color: rgb(102, 102, 102);">@app</span><span class="o" style="box-sizing: inherit; user-select: text !important; color: inherit;">.</span><span class="n" style="box-sizing: inherit; user-select: text !important;">get</span><span class="p" style="box-sizing: inherit; user-select: text !important;">(</span><span class="s2" style="box-sizing: inherit; user-select: text !important; color: rgb(13, 144, 79);">"/items/</span><span class="si" style="box-sizing: inherit; user-select: text !important; color: rgb(24, 54, 145);">{item_id}</span><span class="s2" style="box-sizing: inherit; user-select: text !important; color: rgb(13, 144, 79);">"</span><span class="p" style="box-sizing: inherit; user-select: text !important;">)</span>
<span class="hll" style="box-sizing: inherit; user-select: text !important; display: block; margin: 0px -1.17647em; padding: 0px 1.17647em; background-color: rgba(255, 235, 59, 0.5);"><span class="k" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">async</span> <span class="k" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">def</span> <span class="nf" style="box-sizing: inherit; user-select: text !important; color: rgb(194, 24, 91);">read_item</span><span class="p" style="box-sizing: inherit; user-select: text !important;">(</span><span class="n" style="box-sizing: inherit; user-select: text !important;">item_id</span><span class="p" style="box-sizing: inherit; user-select: text !important;">:</span> <span class="nb" style="box-sizing: inherit; user-select: text !important; color: rgb(194, 24, 91);">int</span><span class="p" style="box-sizing: inherit; user-select: text !important;">,</span> <span class="n" style="box-sizing: inherit; user-select: text !important;">q</span><span class="p" style="box-sizing: inherit; user-select: text !important;">:</span> <span class="nb" style="box-sizing: inherit; user-select: text !important; color: rgb(194, 24, 91);">str</span> <span class="o" style="box-sizing: inherit; user-select: text !important; color: inherit;">=</span> <span class="kc" style="box-sizing: inherit; user-select: text !important; color: rgb(167, 29, 93);">None</span><span class="p" style="box-sizing: inherit; user-select: text !important;">):</span>
</span>    <span class="k" style="box-sizing: inherit; user-select: text !important; color: rgb(59, 120, 231);">return</span> <span class="p" style="box-sizing: inherit; user-select: text !important;">{</span><span class="s2" style="box-sizing: inherit; user-select: text !important; color: rgb(13, 144, 79);">"item_id"</span><span class="p" style="box-sizing: inherit; user-select: text !important;">:</span> <span class="n" style="box-sizing: inherit; user-select: text !important;">item_id</span><span class="p" style="box-sizing: inherit; user-select: text !important;">,</span> <span class="s2" style="box-sizing: inherit; user-select: text !important; color: rgb(13, 144, 79);">"q"</span><span class="p" style="box-sizing: inherit; user-select: text !important;">:</span> <span class="n" style="box-sizing: inherit; user-select: text !important;">q</span><span class="p" style="box-sizing: inherit; user-select: text !important;">}</span>
</code></pre></div><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px;"><strong style="box-sizing: inherit; user-select: text !important;">Note</strong>:</p><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px 0.6rem;">如果你不知道是否会用到，可以查看文档的<span>&nbsp;</span><em style="box-sizing: inherit; user-select: text !important;">"In a hurry?"</em><span>&nbsp;</span>章节中<span>&nbsp;</span><a href="https://fastapi.tiangolo.com/async/#in-a-hurry" target="_blank" style="box-sizing: inherit; user-select: text !important; -webkit-tap-highlight-color: transparent; color: var(--md-text-link-color); text-decoration: none; word-break: break-word; transition: color 125ms ease 0s;">关于<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: currentcolor; font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">async</code><span>&nbsp;</span>和<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: currentcolor; font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">await</code><span>&nbsp;</span>的部分</a>。</p></details>

### 运行

通过以下命令运行服务器：

```bash
uvicorn main:app --reload
INFO: Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO: Started reloader process [28720]
INFO: Started server process [28722]
INFO: Waiting for application startup.
INFO: Application startup complete.
```

<details open="" style="box-sizing: inherit; user-select: text !important; margin: 1.5625em 0px; padding: 0px 0.6rem; overflow: visible; color: rgba(0, 0, 0, 0.87); font-size: 0.64rem; break-inside: avoid; background-color: var(--md-admonition-bg-color); border-left: 0.2rem solid rgb(68, 138, 255); border-radius: 0.1rem; box-shadow: rgba(0, 0, 0, 0.05) 0px 0.2rem 0.5rem, rgba(0, 0, 0, 0.1) 0px 0px 0.05rem; display: block; font-family: Roboto, -apple-system, BlinkMacSystemFont, Helvetica, Arial, sans-serif; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: inherit; user-select: text !important; position: relative; margin: 0px -0.6rem; padding: 0.4rem 1.8rem 0.4rem 2rem; font-weight: 700; background-color: rgba(68, 138, 255, 0.1); display: block; min-height: 1rem; border-top-right-radius: 0.1rem; cursor: pointer;">关于<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: currentcolor; font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: initial; font-size: 0.85em; word-break: break-word; background-color: transparent; border-radius: initial; -webkit-box-decoration-break: clone; margin: initial; box-shadow: none;">uvicorn main:app --reload</code><span>&nbsp;</span>命令......</summary><div id="details-content"><slot name="user-agent-default-slot"><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px;"></p><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px;"></p><p style="box-sizing: inherit; user-select: text !important; margin: 1em 0px;"><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">uvicorn main:app</code><span>&nbsp;</span>命令含义如下:</p><ul style="box-sizing: inherit; user-select: text !important; margin: 1em 0px 0.6rem 0.625em; list-style-type: disc; padding: 0px;"><li style="box-sizing: inherit; user-select: text !important; margin-bottom: 0.5em; margin-left: 1.25em;"><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">main</code>：<code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">main.py</code><span>&nbsp;</span>文件（一个 Python "模块"）。</li><li style="box-sizing: inherit; user-select: text !important; margin-bottom: 0.5em; margin-left: 1.25em;"><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">app</code>：在<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">main.py</code><span>&nbsp;</span>文件中通过<span>&nbsp;</span><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">app = FastAPI()</code><span>&nbsp;</span>创建的对象。</li><li style="box-sizing: inherit; user-select: text !important; margin-bottom: 0px; margin-left: 1.25em;"><code style="box-sizing: inherit; user-select: text !important; color: var(--md-code-fg-color); font-feature-settings: &quot;kern&quot;; font-family: &quot;Roboto Mono&quot;, SFMono-Regular, Consolas, Menlo, monospace; direction: ltr; padding: 0px 0.294118em; font-size: 0.85em; word-break: break-word; background-color: var(--md-code-bg-color); border-radius: 0.1rem; -webkit-box-decoration-break: clone;">--reload</code>：让服务器在更新代码后重新启动。仅在开发时使用该选项。</li></ul></slot></div></details>

### 检查

使用浏览器访问 http://127.0.0.1:8000/items/5?q=somequery。

你将会看到如下 JSON 响应：

```json
{"item_id": 5, "q": "somequery"}
```

你已经创建了一个具有以下功能的 API：

- 通过 *路径* `/` 和 `/items/{item_id}` 接受 HTTP 请求。
- 以上 *路径* 都接受 `GET` *操作*（也被称为 HTTP *方法*）。
- `/items/{item_id}` *路径* 有一个 *路径参数* `item_id` 并且应该为 `int` 类型。
- `/items/{item_id}` *路径* 有一个可选的 `str` 类型的 *查询参数* `q`。

### 交互式 API 文档

现在访问 http://127.0.0.1:8000/docs。

你会看到自动生成的交互式 API 文档（由 [Swagger UI](https://github.com/swagger-api/swagger-ui)生成）：

![Swagger UI](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Cindex-01-swagger-ui-simple.png)

### 备选 API 文档

访问 http://127.0.0.1:8000/redoc。

你会看到另一个自动生成的文档（由 [ReDoc](https://github.com/Rebilly/ReDoc)）生成：

![ReDoc](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Cindex-02-redoc-simple.png)

## 升级示例

修改 `main.py` 文件来从 `PUT` 请求中接收请求体。

我们借助 Pydantic 来使用标准的 Python 类型声明请求体。

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = None


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}


@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    return {"item_name": item.name, "item_id": item_id}
```

服务器将会自动重载（因为在上面的步骤中你向 `uvicorn` 命令添加了 `--reload` 选项）。

### 升级交互式 API 文档

访问 http://127.0.0.1:8000/docs。

- 交互式 API 文档将会自动更新，并加入新的请求体：

![Swagger UI](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Cindex-03-swagger-02.png)

- 点击 "Try it out" 按钮，之后你可以填写参数并直接调用 API：

![Swagger UI interaction](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Cindex-04-swagger-03.png)

- 然后点击 "Execute" 按钮，用户界面将会和 API 进行通信，发送参数，获取结果并在屏幕上展示：

![Swagger UI interaction](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Cindex-05-swagger-04.png)

### 升级备选文档

访问 http://127.0.0.1:8000/redoc。

- 备选文档同样会体现新加入的请求参数和请求体：

![ReDoc](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5Cindex-06-redoc-02.png)

### 回顾

总的来说，你就像声明函数的参数类型一样只声明了**一次**请求参数、请求体等的类型。

你使用了标准的现代 Python 类型来完成声明。

你不需要去学习新的语法、了解特定库的方法或类，等等。

只需要使用标准的 **Python 3.6 及更高版本**。

举个例子，比如声明 `int` 类型：

```
item_id: int
```

或者一个更复杂的 `Item` 模型：

```
item: Item
```

......在进行一次声明之后，你将获得：

- 编辑器支持，包括：

    - 自动补全
    - 类型检查

- 数据校验：

    - 在校验失败时自动生成清晰的错误信息
    - 对多层嵌套的 JSON 对象依然执行校验

- 转换

     

    来自网络请求的输入数据为 Python 数据类型。包括以下数据：

    - JSON
    - 路径参数
    - 查询参数
    - Cookies
    - 请求头
    - 表单
    - 文件

- 转换

     

    输出的数据：转换 Python 数据类型为供网络传输的 JSON 数据：

    - 转换 Python 基础类型 （`str`、 `int`、 `float`、 `bool`、 `list` 等）
    - `datetime` 对象
    - `UUID` 对象
    - 数据库模型
    - ......以及更多其他类型

- 自动生成的交互式 API 文档，包括两种可选的用户界面：

    - Swagger UI
    - ReDoc

------

回到前面的代码示例，**FastAPI** 将会：

- 校验 `GET` 和 `PUT` 请求的路径中是否含有 `item_id`。
- 校验`GET`和`PUT` 请求中的`item_id`是否为  `int`类型。
    - 如果不是，客户端将会收到清晰有用的错误信息。

检查 `GET` 请求中是否有命名为 `q` 的可选查询参数（比如 `http://127.0.0.1:8000/items/foo?q=somequery`）。

- 因为 `q` 被声明为 `= None`，所以它是可选的。
- 如果没有 `None` 它将会是必需的 (如 `PUT` 例子中的请求体)
- 对于访问 `/items/{item_id}` 的 `PUT` 请求，将请求体读取为 JSON 并：
    - 检查是否有必需属性 `name` 并且值为 `str` 类型 。
    - 检查是否有必需属性 `price` 并且值为 `float` 类型。
    - 检查是否有可选属性 `is_offer`， 如果有的话值应该为 `bool` 类型。
    - 以上过程对于多层嵌套的 JSON 对象同样也会执行

- 自动对 JSON 进行转换或转换成 JSON。
- 通过 OpenAPI 文档来记录所有内容，可被用于：

    - 交互式文档系统
    - 许多编程语言的客户端代码自动生成系统
- 直接提供 2 种交互式文档 web 界面。

------

虽然我们才刚刚开始，但其实你已经了解了这一切是如何工作的。

尝试更改下面这行代码：

```python
    return {"item_name": item.name, "item_id": item_id}
```

......从：

```python
        ... "item_name": item.name ...
```

......改为：

```python
        ... "item_price": item.price ...
```

......注意观察编辑器是如何自动补全属性并且还知道它们的类型：

![editor support](https://fastapi.tiangolo.com/img/vscode-completion.png)

[教程 - 用户指南](https://fastapi.tiangolo.com/tutorial/) 中有包含更多特性的更完整示例。

**剧透警告**： 教程 - 用户指南中的内容有：

- 对来自不同地方的参数进行声明，如：**请求头**、**cookies**、**form 表单**以及**上传的文件**。
- 如何设置**校验约束**如 `maximum_length` 或者 `regex`。
- 一个强大并易于使用的 **依赖注入** 系统。
- 安全性和身份验证，包括通过 **JWT 令牌**和 **HTTP 基本身份认证**来支持 **OAuth2**。
- 更进阶（但同样简单）的技巧来声明 **多层嵌套 JSON 模型** （借助 Pydantic）。
- 许多额外功能（归功于 Starlette）比如：
    - **WebSockets**
    - **GraphQL**
    - 基于 `requests` 和 `pytest` 的极其简单的测试
    - **CORS**
    - **Cookie Sessions**
    - ......以及更多

## 性能

独立机构 TechEmpower 所作的基准测试结果显示，基于 Uvicorn 运行的 **FastAPI** 程序是 [最快的 Python web 框架之一](https://www.techempower.com/benchmarks/#section=test&runid=7464e520-0dc2-473d-bd34-dbdfd7e85911&hw=ph&test=query&l=zijzen-7)，仅次于 Starlette 和 Uvicorn 本身（FastAPI 内部使用了它们）。(*)

想了解更多，请查阅 [基准测试](https://fastapi.tiangolo.com/benchmarks/) 章节。

## 可选依赖

用于 Pydantic：

- [`ujson`](https://github.com/esnme/ultrajson) - 更快的 JSON "解析"。
- [`email_validator`](https://github.com/JoshData/python-email-validator) - 用于 email 校验。

用于 Starlette：

- [`requests`](http://docs.python-requests.org/) - 使用 `TestClient` 时安装。
- [`aiofiles`](https://github.com/Tinche/aiofiles) - 使用 `FileResponse` 或 `StaticFiles` 时安装。
- [`jinja2`](http://jinja.pocoo.org/) - 使用默认模板配置时安装。
- [`python-multipart`](https://andrew-d.github.io/python-multipart/) - 需要通过 `request.form()` 对表单进行"解析"时安装。
- [`itsdangerous`](https://pythonhosted.org/itsdangerous/) - 提供 `SessionMiddleware` 支持。
- [`pyyaml`](https://pyyaml.org/wiki/PyYAMLDocumentation) - 使用 Starlette 提供的 `SchemaGenerator` 时安装（有 FastAPI 你可能并不需要它）。
- [`graphene`](https://graphene-python.org/) - 需要 `GraphQLApp` 支持时安装。
- [`ujson`](https://github.com/esnme/ultrajson) - 使用 `UJSONResponse` 时安装。

用于 FastAPI / Starlette：

- [`uvicorn`](http://www.uvicorn.org/) - 用于加载和服务你的应用程序的服务器。
- [`orjson`](https://github.com/ijl/orjson) - 使用 `ORJSONResponse` 时安装。

你可以通过 `pip install fastapi[all]` 命令来安装以上所有依赖。

## 许可协议

该项目遵循 MIT 许可协议。