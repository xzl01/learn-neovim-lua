# 将 Neovim 打造成为自己的 IDE

本项目配置参考[learn-neovim-lua](https://github.com/nshen/learn-neovim-lua)，但大部分快捷键经过重设（因为本人不喜欢快捷键被重度修改，对新手不够友好），由于本人主要做 C++ 开发工作，所以本项目完全适用 C++ 开发场景。

本项目在保持插件原有快捷键配置的同时，尽量进行更加人性化的配置。

## 目录结构说明

.<br>
├── filetype.lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; // 使用lua的文件类型检测，加载速度更快，效率更高<br>
├── init.lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 所有配置的入口<br>
├── LICENSE&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 本项目使用 MIT 协议<br>
├── lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 存放所有配置文件的目录<br>
│  ├── autocmds.lua &emsp;&emsp;&emsp;&emsp;&emsp;// 设置自动命令<br>
│  ├── basic.lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 基础设置<br>
│  ├── colorscheme.lua&emsp;&emsp;&emsp;&emsp;// 主题设置<br>
│  ├── keybindings.lua &emsp;&emsp;&emsp;&emsp;// 快捷键绑定<br>
│  ├── lsp&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// lsp 相关设置<br>
│  │  ├── cmp.lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 智能补全设置<br>
│  │  ├── config&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// lsp 各语言设置<br>
│  │  │  ├── bash.lua<br>
│  │  │  ├── clangd.lua<br>
│  │  │  ├── cmake.lua<br>
│  │  │  ├── css.lua<br>
│  │  │  ├── html.lua<br>
│  │  │  ├── json.lua<br>
│  │  │  ├── lua.lua<br>
│  │  │  ├── markdown.lua<br>
│  │  │  ├── pyright.lua<br>
│  │  │  └── rust.lua<br>
│  │  ├── setup.lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// lsp 安装设置<br>
│  │  └── ui.lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// lsp ui 设置<br>
│  ├── plugin-config&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// nvim 各插件设置<br>
│  │  ├── bufferline.lua<br>
│  │  ├── comment.lua<br>
│  │  ├── dashboard.lua<br>
│  │  ├── fidget.lua<br>
│  │  ├── gitsigns.lua<br>
│  │  ├── indent-blankline.lua<br>
│  │  ├── lualine.lua<br>
│  │  ├── nvim-autopairs.lua<br>
│  │  ├── nvim-notify.lua<br>
│  │  ├── nvim-tree.lua<br>
│  │  ├── nvim-treesitter.lua<br>
│  │  ├── project.lua<br>
│  │  ├── telescope.lua<br>
│  │  ├── todo-comments.lua<br>
│  │  └── toggleterm.lua<br>
│  ├── plugins.lua&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 要安装哪些插件，可以在此设置<br>
│  └── utils&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 通用设置<br>
│     ├── change-colorscheme.lua<br>
│     └── global.lua<br>
└── README.md&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;// 本文件

## 快捷键绑定说明

这里列出一些常用快捷键说明，也可以查看或修改 keybindings.lua 文件

 **分类**     | **快捷键**    | **说明**
------------|------------|---------------------------------------------
 通用         | ;          | leader 键，vim 快捷键的一种方式，加上 leader 键和不加是两种快捷键。
 通用         | qq         | normal 模式，退出
 todo       | ]t         | normal 模式，下一个注释标签
 todo       | [t         | normal 模式，上一个注释标签
 缩进         | <          | visual 模式，左缩进
 缩进         | >          | visual 模式，右缩进
 移动         | Ctrl+Up    | visual 模式， 向上移动选中文本
 移动         | Ctrl+Down  | visual 模式，向下移动选中文本
 通用         | Ctrl+Left  | insert 模式，光标移动到行首
 通用         | Ctrl+Right | insert 模式，光标移动到行尾
 窗口         | sv         | normal 模式，纵向分割
 窗口         | sh         | normal 模式，横向分割
 窗口         | sc         | normal 模式，关闭当前窗口
 窗口         | so         | normal 模式，关闭其他窗口
 窗口         | Alt+Left   | normal 模式，向左跳转窗口
 窗口         | Alt+Right  | normal 模式，向右跳转窗口
 窗口         | Alt+Up     | normal 模式，向上跳转窗口
 窗口         | Alt+Down   | normal 模式，向下跳转窗口
 treesitter | zz         | normal 模式，折叠代码段
 treesitter | Z          | normal 模式，展开代码段
 tree       | Alt+m      | normal 模式，显示文件目录树
 标签         | Ctrl+Left  | normal 模式，向左切换标签页
 标签         | Ctrl+Right | normal 模式，向右切换标签页
 标签         | Ctrl+c     | normal 模式，关闭当前标签页
 空白符        | Ctrl+t     | normal 模式，删除当前文档所有尾部空白符
 telescope  | Ctrl+p     | normal 模式，打开telescope
 注释         | Ctrl+/     | normal visual 模式，注释或取消注释当前行/选中行
 lsp        | ;rn        | normal 模式，重命名所有引用当前变量
 lsp        | gd         | normal 模式，跳转到定义处
 lsp        | gh         | normal 模式，预览定义
 lsp        | gr         | normal 模式，查看所有引用
 lsp        | gp         | normal 模式，显示当前错误信息
 lsp        | gj         | normal 模式，跳转到下一条错误处
 lsp        | gk         | normal 模式，跳转到上一条错误处
 lsp        | gc         | normal 模式，复制当前错误到剪切板
 lsp        | ;f         | normal 模式，格式化当前文档
 cmp        | Tab        | insert 模式，切换到下一条补全条目
 cmp        | Shift+Tab  | insert 模式，切换到上一条补全条目
 terminal   | tt         | normal 模式，以悬浮形式打开终端
 terminal   | tg         | normal 模式，以悬浮形式打开lazygit
 git        | hd         | normal 模式，对比当前文件的修改
 git        | hs         | normal 模式，暂存当前块
 git        | hS         | normal 模式，暂存当前文档
 git        | hr         | normal 模式，取消暂存当前块
 git        | hR         | normal 模式，取消暂存当前文档
 git        | td         | normal 模式，在本文档中显示已删除行
