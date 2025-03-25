将其他格式的笔记（如 Word、PDF、HTML、纯文本等）转换为 Markdown 格式，可以借助工具和手动调整结合的方式。以下是详细方法和工具推荐：

\---

\### \*\*1. 常见格式转换工具\*\*

\#### \*\*(1) Word 文档 → Markdown\*\*

\- \*\*工具推荐\*\*：

\- \*\*\[Pandoc\](<https://pandoc.org/)\*\*（跨平台命令行工具，支持批量转换）：>

\`\`\`bash

\# 安装 Pandoc

sudo apt install pandoc # Linux

brew install pandoc # macOS

\# 转换命令

pandoc input.docx -o output.md

\`\`\`

\- \*\*\[Word to Markdown Converter\](<https://word2md.com/)\*\*（在线工具，直接粘贴内容或上传文件）。>

\- \*\*VS Code 插件\*\*：\[Office Viewer\](<https://marketplace.visualstudio.com/items?itemName=cweijan.vscode-office>) 可直接预览并导出为 Markdown。

\- \*\*注意事项\*\*：

\- Word 中的复杂表格可能转换后格式错乱，需手动调整。

\- 图片需要单独导出并手动插入（或使用工具自动上传到图床）。

\---

\#### \*\*(2) PDF → Markdown\*\*

\- \*\*工具推荐\*\*：

\- \*\*\[pdf2md\](<https://github.com/jzillmann/pdf-to-markdown)\*\*（基于> Python 的转换工具）：

\`\`\`bash

pip install pdf2md

pdf2md -i input.pdf -o output.md

\`\`\`

\- \*\*\[Noumena\](<https://noumena.ai/pdf-to-markdown)\*\*（在线转换，免费但有文件大小限制）。>

\- \*\*Adobe Acrobat\*\*：导出为 HTML，再用 Pandoc 转 Markdown。

\- \*\*注意事项\*\*：

\- PDF 转换后可能包含大量无用空格和换行，需用正则表达式清理：

\`\`\`text

替换连续空行：\\n{3,} → \\n\\n

删除行尾空格：\\s+$ → 空

\`\`\`

\---

\#### \*\*(3) HTML → Markdown\*\*

\- \*\*工具推荐\*\*：

\- \*\*\[Turndown\](<https://github.com/domchristie/turndown)\*\*（JavaScript> 库，支持在线\[Demo\](<https://domchristie.github.io/turndown/)）：>

\`\`\`javascript

// 示例代码

var turndownService = new TurndownService();

var markdown = turndownService.turndown(htmlContent);

\`\`\`

\- \*\*\[html2text\](<https://github.com/Alir3z4/html2text)\*\*（Python> 工具）：

\`\`\`bash

pip install html2text

html2text input.html > output.md

\`\`\`

\---

\#### \*\*(4) 纯文本 → Markdown\*\*

\- \*\*手动优化\*\*：

\- \*\*标题\*\*：在文本前加 \`#\`，例如 \`# 一级标题\`。

\- \*\*列表\*\*：

\`\`\`markdown

\- 无序列表项

1\. 有序列表项

\`\`\`

\- \*\*代码块\*\*：用反引号包裹（\\\`代码\\\`）或三个反引号（\\\`\`\`语言）标注多行代码。

\- \*\*链接和图片\*\*：

\`\`\`markdown

\[链接文字\](URL)

!\[图片描述\](图片URL)

\`\`\`

\---

\### \*\*2. 格式转换后的手动优化\*\*

\#### \*\*(1) 表格处理\*\*

\- \*\*工具\*\*：使用 \[Tables Generator\](<https://www.tablesgenerator.com/markdown_tables>) 快速生成 Markdown 表格。

\- \*\*示例\*\*：

\`\`\`markdown

| 语法 | 用途 |

|------------|--------------|

| \`#\` | 标题 |

| \`\*\*text\*\*\` | 加粗文本 |

\`\`\`

\#### \*\*(2) 代码块高亮\*\*

\- 在代码块开头指定语言以启用高亮：

\`\`\`markdown

\`\`\`python

def hello():

print("Hello World")

\`\`\`

\`\`\`

\#### \*\*(3) 数学公式\*\*

\- 使用 \`$$\` 包裹 LaTeX 公式：

\`\`\`markdown

$$ E = mc^2 $$

\`\`\`

\---

\### \*\*3. 批量转换与自动化\*\*

\- \*\*脚本示例\*\*（批量转换 \`docx\` 到 \`md\`）：

\`\`\`bash

# !/bin/bash

for file in \*.docx; do

pandoc "$file" -o "${file%.docx}.md"

done

\`\`\`

\- \*\*自动化工具\*\*：

\- \*\*\[Obsidian\](<https://obsidian.md/)\*\*：支持直接粘贴> HTML/Word 内容并自动转 Markdown。

\- \*\*\[Typora\](<https://typora.io/)\*\*：实时预览> Markdown，支持直接拖入图片和表格。

\---

\### \*\*4. 特殊内容处理\*\*

\#### \*\*(1) 图片迁移\*\*

\- 将本地图片上传到图床（如 \[Imgur\](<https://imgur.com/)、\[SM.MS\>](<https://sm.ms/)），并替换链接：>

\`\`\`markdown

!\[描述\](<https://i.imgur.com/xxx.png>)

\`\`\`

\#### \*\*(2) 脚注和引用\*\*

\- Markdown 的脚注语法：

\`\`\`markdown

这是一段文字\[^1\]。

\[^1\]: 这是脚注内容。

\`\`\`

\---

\### \*\*5. 推荐工具清单\*\*

| 工具类型 | 推荐工具 |

|----------------|--------------------------------------------------------------------------|

| \*\*全能转换\*\* | Pandoc、Typora |

| \*\*在线转换\*\* | \[Word to Markdown\](<https://word2md.com/)、\[Noumena\>](<https://noumena.ai/)|>

| \*\*格式优化\*\* | VS Code + Markdown 插件（如 \*\*Markdown All in One\*\*） |

| \*\*批量处理\*\* | 自定义 Shell/Python 脚本 |

\---

\### \*\*示例：转换后的 Markdown 效果\*\*

\*\*原始文本\*\*（HTML）：

\`\`\`html

&lt;h2&gt;Git 常用命令&lt;/h2&gt;

&lt;ul&gt;

&lt;li&gt;&lt;code&gt;git init&lt;/code&gt;: 初始化仓库&lt;/li&gt;

&lt;/ul&gt;

\`\`\`

\*\*转换后 Markdown\*\*：

\`\`\`markdown

\## Git 常用命令

\- \`git init\`: 初始化仓库

\`\`\`

\---

通过上述方法，你可以高效地将各类笔记转换为 Markdown，并结合 GitHub Pages 构建清晰的知识库！