---
layout: docs
标题: 配置.exvim 
---

exVim使用[ex-vimentry](https://github.com/exvim/ex-vimentry)插件来创建和设置一个项目。
ex-vimentry插件会将.exvim结尾的文件里的配置应用在你的项目中。

## .exvim文件的语法
阅读 [ex-vimentry syntax](https://github.com/exvim/ex-vimentry#syntax).

## 默认选项 

### folder_filter_mode (option)

选项:

- include（备注：需要包含的文件夹） 
- exclude（备注：需要排除的文件夹）

`folder_filter_mode` 告诉exvim在 `folder_filter`中使用哪种模式 

### folder_filter (array)

`folder_filter`的值为文件夹。它会按照folder_filter_mode里的设置来读取文件夹，即加载
或者排除哪些文件夹。
示例:

当你将filter设置为：

```
folder_filter_mode = include
folder_filter += foo,bar
```

仅仅叫做foo或者bar的文件夹会在你的ex-project窗口中显示。

当你将filter mode 设置为：

```
folder_filter_mode = exclude
folder_filter += foo,bar
```

叫做foo或bar的文件夹不会在ex-project窗口中显示

这个选项也影响如下插件：

- ex-project 
- NERDTree
- ex-config
  - id-utils ( generate id-lang-autogen.map )
  - ctags

### file_filter (array)

’file_filter'的值是文件类型。它表示你希望在exVim项目中看到的文件类型。

示例:

```
file_filter += c,cpp
```

filter使exVim接受后缀为".c  .cpp"的文件

`file_filter`也接受`__EMPTY__`__的值，它表示文件没有后缀

```
file_filter += __EMPTY__,c,cpp
```

filter也接受没有后缀的文件，比如：
LICENSE, README, Makefile, ...

这个选项影响如下插件：

- ex-project 
- NERDTree
- ex-config
  - id-utils ( generate id-lang-autogen.map )
  - ctags (TODO)

默认情况下，如果这个选项是空的，那么id-lang会使用在 `tools/idutils/`的`id-lang.map`
来创建ID。当这个选项有被设置，ex-config会在`.exvim.project/`文件夹下创建`id-lang-autogen.map
并且会使用它代替'id-lang.map'
### file_ignore_pattern (array)

`file_ignore_pattern`的值为文件名。并且与该值匹配的所有文件将在exVim中被忽略 

示例:

```
file_ignore_pattern += useless.txt,*.min.js,_OLD_*.cpp
```

会使得`useless.txt`、所有以`min.js`结尾的文件、以`_OLD_`开头的cpp文件在exVim中被忽略。__

注意你唯一能使用的通配符是`*`

### enable_restore_bufs (bool)

当开启时，exVim会存储你所有打开过文件的缓存在`.exvim.your.project/restore_info`中。
当你下次打开这个exVim项目时，它会将文件还原到最后一次存储的状态。

## Post Init

当exVim解析完'.exvim'文件后，它会调用'g:exvim_post_init'函数（如果存在的话）。你可以在你的
'____vimrc'文件中自定义这个函数已实现自己的其他配置。

这是一个例子 [reference](https://github.com/exvim/ex-vimentry#get-vimentry-settings)教你如何
在你的脚本中使用这个函数 

## Multiple .exvim files

你可以在一个项目中拥有多个`.exvim`文件，这个选项允许你在一个项目中运用不同的配置。