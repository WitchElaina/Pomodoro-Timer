# Pomodoro Timer

> chatgpt 写的

## Demo

https://pomodoro.mszook.art/

## 产品概述
番茄钟是一种时间管理技巧，将工作时间划分为25分钟的时间块，每个时间块之间休息5分钟，每4个时间块之后休息15分钟。这款番茄钟代码是一个基于Vue框架实现的Web应用，通过简单的UI界面帮助用户管理时间和提高工作效率。

## 产品特点
支持自定义时间段：用户可以根据自己的需要设置工作时间、短休息时间、长休息时间和休息次数。
支持浏览器通知：用户可以选择开启浏览器通知，当时间到达时会有弹窗提醒。
易于使用：用户只需要点击“开始”按钮即可开始使用番茄钟，界面简洁易懂，不需要繁琐的设置。

## 产品界面
番茄钟界面包括以下几个部分：

- 工作时间倒计时：显示当前工作时间还剩下多少时间。
- 工作状态信息：显示当前处于工作状态还是休息状态，以及当前已经完成了多少个时间块。
- 控制按钮：包括“开始/暂停”、“重置”、“下一个”和“选项”按钮。
- 选项窗口：用户可以在这个窗口中自定义番茄钟的时间设置。


## 使用方法
1. 打开网页：用户可以通过浏览器打开该番茄钟网页。
1. 设置选项：用户可以点击“选项”按钮设置番茄钟的时间段和休息次数。
1. 开始使用：用户点击“开始”按钮开始使用番茄钟。
1. 休息：当工作时间到达时，番茄钟会提示用户开始休息，用户可以选择点击“下一个”按钮开始休息或者暂停休息。
1. 工作：当休息时间到达时，番茄钟会提示用户开始工作，用户可以选择点击“下一个”按钮开始工作或者暂停工作。
1. 重置：用户可以点击“重置”按钮重新开始番茄钟。
1. 完成使用：用户可以点击关闭按钮完成使用番茄钟。

## 技术实现

该番茄钟代码使用了Vue框架，主要实现了以下几个功能：

- 计时器功能：通过setInterval方法实现倒计时功能。
- 选项设置功能：通过localStorage实现选项的保存和读取。
- 浏览器通知功能：通过Notification API实现浏览器通知功能。
- UI界面：使用HTML、CSS和Vue实现番茄钟的UI界面。