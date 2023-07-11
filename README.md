# 应用配置

一个类似「应用变量」的可在宿主应用内完成配置的适用于「LSPatch 便携模式」的模块

## 特色

- 支持修改应用内 DPI（配置时使用「最小宽度」）
- 支持在不允许获取「读取应用列表」权限的设备上模拟「读取应用列表」权限
- 可以按设备生效的自定义配置

## 配置文件说明

自定义配置不提供 GUI 配置界面，请自行使用「MT 管理器」等工具修改模块 apk 内的 [`assets/config.xml`](https://github.com/jiwangyihao/app_config/blob/main/app/src/main/assets/config.xml) 文件进行配置。

示例文件如下（你也可以点击上面的链接查看当前最新版本）：
``` xml
<?xml version="1.0" encoding="utf-8" ?>
<!-- <config> 是整个配置文件的根元素 -->
<!-- 每个配置文件中只能有一个 <config> -->
<!-- author 属性用于标记当前配置的作者 -->
<!-- 既然你已经看到了这段注释，那么，作为修改配置的开始 -->
<!-- 把它改成你的 ID 吧！ -->
<config author="吉王义昊">
    <!-- <device> 标签标记一组设备配置，name 属性用于标记需生效的设备代码 -->
    <!-- 机型代码可使用「设备信息」获取（「设备」选项卡下第一个卡片的「设备」项） -->
    <!-- 当 device.name 为 default 时，该组配置对所有设备生效 -->
    <device name="default">
        <!-- 最小宽度设置（整数型，默认值是 320） -->
        <!-- 该项设置与开发者选项中的最小宽度效果基本相同 -->
        <!-- （部分系统，比如 MIUI 的开发者选项内的最小宽度设置存在问题，可能效果会不同） -->
        <!-- 最小宽度表示屏幕在宽上以 dp 表示的长度 -->
        <!-- 最小宽度越大，屏幕能容纳的独立像素（dp）就越多，能显示的内容就越多 -->
        <!-- 相应的界面元素就越小 -->
        <!-- 最小宽度与 dpi 之间的换算关系为： -->
        <!-- 最小宽度 * dpi / 160 = 屏幕短边物理像素数 -->
        <!-- 注意：尽管使用本模块无需考虑对系统的影响，但过大或者过小的数值可能会不生效 -->
        <item name="minWidth">320</item>
        <!-- 模拟应用列表权限（布尔型，默认值是 true） -->
        <item name="fakeAppList">true</item>
    </device>
    <!-- 单独设备配置，该配置会对机型代码是 example 的设备生效 -->
    <device name="example">
        <!-- 单独设备配置可以只配置部分项目 -->
        <item name="minWidth">268</item>
    </device>
</config>
<!-- 所有符合条件的配置都会被应用（通用设备配置或者与当前设备机型代码相同的配置） -->
<!-- 重复的配置项会互相覆盖，写在后面的配置项优先级更高，会覆盖前面的配置项 -->
<!-- 值得注意的是，单独设备配置并不享有额外的优先级 -->
<!-- 也就是说，如果你把通用设备配置写在最后，所有的单独设备配置都无法生效 -->

<!-- 警告：尽管编写模块时做了容错处理，但错误的配置仍然可能使模块部分甚至整体失效 -->

<!-- 考虑到一份配置文件大概不太可能只有一个作者 -->
<!-- 但是 Toast 本身又不欢迎过长的文字（笑 -->
<!-- config.author 最好只标注这份配置文件的最后修改者 -->
<!-- 配置文件的编辑历史就写在这下面好了 -->
<!-- （这几个字用不了几 kB 的，^.^） -->

<!-- 2023-7-10 创建 by 吉王义昊 -->
<!-- 2023-7-11 修改 by 吉王义昊 -->
```