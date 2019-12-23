---
title: Sublime插件推荐
top: false
cover: false
toc: true
mathjax: true
date: 2019-12-22 16:52:00
password:
summary:
tags:
- Sublime
- 工具
categories:
- 软件
---

>推荐一下好用的Sublime插件，打造适合自己的编辑器😁。

# Plain Tasks
---
![效果图](2.png)
- [官方文档](https://github.com/aziz/PlainTasks)

今日事今日毕，使用Plain Tasks可以很方便的规划自己的任务。

## 配置步骤
`Shift+Ctrl+P`调出命令行,输入`Package Control: Install Package`
![](1.png)
输入Plain Tasks直接安装，成功后就能在`Preferences/Package Settings`中看到`PlainTasks`这一选项

## 使用说明
### 创建任务表
`Shift+Ctrl+P`输入`tasks`，选择`New document`
### 任务编辑
- `Ctrl+i`添加一个新任务
- `Ctrl+d`将任务标记为完成，再按一次可将其重置
- `Alt+c`将任务标记为取消，再按一次可将其重置
- `Shift+Ctrl+a`将已完成的任务存档，将其从列表中删除并将它们附加到“存档”项目下文件的底部
- `Shift+Ctrl+u`将在默认浏览器中打开位于光标处的url，但http方案必须包含在<>中，如`<https://baidu.com>`
- `:`行尾带有冒号的任何东西都是项目标题，您也可以通过缩进来嵌套项目。
- `--`,`Tab`会创建 `--- ✄ -----------------------`用来分隔
- 标签：
`c`,`Tab`创建`@critical`标签，代表重要且紧急
`h`,`Tab`创建`@high`标签，代表重要不紧急
`l`,`Tab`创建`@low`标签，代表不重要且不紧急
`s`,`Tab`创建`@stared`标签，再按tab一次，将插入当前日期，当您完成或取消带有此类标记的任务时，您将知道自开始以来已经经过了多少时间；如果更改完成/取消/开始时间，则可以删除时间后，在标签后按tab来重新计算花费在任务上的时间
`d`,`Tab`创建`@due`标签，用来规定任务完成的时间，再按tab一次，将插入当前日期，与`@due(0)`一样
|符号|含义|
|:----------------:|:--------------------------------------------------:|
|`@due(1)`         |下个月的第一天|
|`@due(5)`         |当前月份的第5天（如果当前日期为5日或5日之后，则为下个月）|
|`@due(2-3)`       |本年或下一年的2月3日|
|`@due(20.1.1 1:1)`|2020年1月1日在01:01 @due(20-01-01 01:01)|
|`@due(+)`         |明天以及@due( +1) 或@due( +1d)|
|`@due(+w)`        |自当前日期起一周 @due( +7)|
|`@due(+2:)`       |自当前日期起两个小时|
|`@due(+:555)`     |自当前日期起555分钟|
|`@due(+2 12:)`    |自当前日期起2天12个小时|

### 更改配置
- `Preferences/Package Settings/PlainTasks/Settings-Default`中是默认配置
- `Preferences/Package Settings/PlainTasks/Settings-User`是用户配置

#### 配色更改
在`Preferences/Package Settings/PlainTasks/Settings-User`中加入

```sublime
{"color_scheme": "Packages/PlainTasks/tasks.hidden-tmTheme",}
```
其他配色可以选择：

```sublime
Packages/PlainTasks/tasks-dark.hidden-tmTheme
Packages/PlainTasks/tasks-eighties-colored.hidden-tmTheme
Packages/PlainTasks/tasks-eighties-dark.hidden-tmTheme
Packages/PlainTasks/tasks-gray.hidden-tmTheme
Packages/PlainTasks/tasks-monokai.hidden-tmTheme
Packages/PlainTasks/tasks-solarized-dark.hidden-tmTheme
Packages/PlainTasks/tasks-solarized-light.hidden-tmTheme
```

#### 拼写检测
为了防止sublime拼写检查时报错，可以在`Preferences/Settings/User`中加入
```sublime
{
   “ ignore_words ”：[ “ ☐ ”，“ ✔ ”，“ ✘ ”，“ ✄ ” ]
}
```

### 任务统计
在命令面板中输入`Tasks: Copy Statistics`，可以直接粘贴到文档里

### 进度条设置
更改进度条显示的格式，可以在`Preferences/Settings/User`中加入
```sublime
{
    "bar_full": "■",   // any char
    "bar_empty": "☐", // any char

    // if you want to avoid Unicode when copy stats — you can define replacements
    // e.g. to convert ■■■■■■☐☐☐☐ to [======    ]
    "replace_stats_chars": [[" ■", " [="], ["■", "="], ["☐ ", " ] "], ["☐", " "]]
}
```