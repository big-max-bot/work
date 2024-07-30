# 使用 jsPsych 创建心理学实验的教程

在这个教程中，我们将逐步指导您如何使用 `jsPsych` 创建一个简单的心理学实验。我们假设您对 HTML 和 JavaScript 不太熟悉，因此我们将从基础知识讲起，并提供详细的代码示例。

## 1. 基础知识概述

### HTML（超文本标记语言）

HTML 用于创建网页的结构。它定义了网页上的文本、图片、按钮等内容。每个 HTML 页面都由各种元素（如 `<div>`, `<p>`, `<button>`）组成，它们决定了网页的布局和内容。

### JavaScript

JavaScript 是一种编程语言，用于为网页添加交互功能。它允许您创建动态内容和响应用户操作。

### jsPsych

`jsPsych` 是一个用于心理学实验的 JavaScript 库。它帮助研究人员创建和管理心理学实验的各种任务和测量。

## 2. 实验结构概述

我们将创建一个心理学实验，包含以下几个部分：

1. **欢迎页面**：介绍实验并提供开始按钮。
2. **指导语页面**：解释实验的流程和注意事项。
3. **行为实验页面**：包含主要的实验任务。
4. **结束页面**：感谢参与者并结束实验。

## 3. 编写实验代码

### 3.1 创建 HTML 文件

首先，我们需要一个 HTML 文件来加载 `jsPsych` 和定义实验的结构。

```html
<!DOCTYPE HTML>
<html lang='zh-CN'>
<head>
    <meta charset='utf-8'>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>心理学实验</title>
    <!-- 引用 jsPsych 库 -->
    <script src="https://cdn.jsdelivr.net/npm/jspsych@6.3.1/jspsych.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/jspsych@6.3.1/plugins/jspsych-html-button-response.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/jspsych@6.3.1/plugins/jspsych-html-keyboard-response.js"></script>
    <link href="styles.css" rel="stylesheet" type="text/css">
</head>
<body>
    <div id="jspsych-target"></div>
    <script>
        // 这里是实验的 JavaScript 代码
    </script>
</body>
</html>
3.2 欢迎页面
我们将创建一个欢迎页面，介绍实验并提供开始按钮。

javascript
复制代码
var welcome = {
    type: 'html-button-response',
    stimulus: `
        <h2>欢迎参加我们的实验</h2>
        <p>请仔细阅读以下说明，然后点击“开始实验”按钮以继续。</p>
    `,
    choices: ['开始实验']
};
3.3 指导语页面
这个页面将向参与者解释实验的流程和注意事项。

javascript
复制代码
var instructions = {
    type: 'html-keyboard-response',
    stimulus: `
        <h3>实验指导</h3>
        <p>请阅读以下实验指导：</p>
        <ul>
            <li>实验将包括几个阶段。</li>
            <li>请按照指示完成每个阶段。</li>
            <li>按下任意键继续。</li>
        </ul>
    `
};
3.4 行为实验页面
在这个页面，我们将创建一个简单的任务，例如填写一个问卷。

javascript
复制代码
var survey = {
    type: 'survey-html-form',
    html: `
        <div>
            <h3>问卷调查</h3>
            <label>1. 你的名字: <input type="text" name="name"></label><br>
            <label>2. 你的年龄: <input type="text" name="age"></label><br>
            <label>3. 你的性别: 
                <input type="radio" name="gender" value="male"> 男
                <input type="radio" name="gender" value="female"> 女
            </label><br>
            <input type="submit" value="提交">
        </div>
    `,
    button_label: '提交'
};
3.5 结束页面
实验结束后，显示一个感谢页面。

javascript
复制代码
var ending = {
    type: 'html-keyboard-response',
    stimulus: `
        <h3>实验结束</h3>
        <p>感谢您的参与！请按下任意键结束实验。</p>
    `
};
3.6 整合实验代码
最后，我们将所有部分整合到一个 jsPsych.init 调用中。

javascript
复制代码
jsPsych.init({
    timeline: [welcome, instructions, survey, ending],
    display_element: 'jspsych-target',
    on_finish: function() {
        console.log(jsPsych.data.get().json()); // 打印数据
    }
});
4. CSS 样式
为了使页面更美观，您可以使用外部 CSS 文件进行样式设置。创建一个 styles.css 文件并在 HTML 中引用它。

css
复制代码
/* styles.css */
body {
    font-family: Arial, sans-serif;
    text-align: center;
}

button {
    font-size: 16px;
    padding: 10px 20px;
    margin: 20px;
}
5. 运行和测试实验
将 HTML 文件、JavaScript 代码和 CSS 文件上传到您的 Web 服务器或本地环境中。打开 HTML 文件，您应该能看到您的实验界面并进行测试。

总结
通过本教程，您已经学习了如何创建一个基本的 jsPsych 实验。您可以根据自己的需要修改和扩展实验任务。如果遇到问题，jsPsych 官方文档和社区是很好的资源。

祝您实验顺利！

go
复制代码

将以上内容保存为一个 `.md` 文件，即可在 GitHub 或其他 Markdown 支持的平台上查看和共享。
