# 国际化框架

> 码云地址：[Gitee](https://gitee.com/getActivity/MultiLanguages)

> [点击此处下载Demo](MultiLanguages.apk)

![](MultiLanguages.gif)

#### 集成步骤

```groovy
dependencies {
    implementation 'com.hjq:language:5.0'
}
```

#### 初始化框架

```java
// 在 Application 中初始化
MultiLanguages.init(this);
```

> 重写 Application 的 attachBaseContext 方法

```java
@Override
protected void attachBaseContext(Context base) {
    // 国际化适配（绑定语种）
    super.attachBaseContext(MultiLanguages.attach(base));
}
```

> 重写**基类** BaseActivity 的 attachBaseContext 方法

```java
@Override
protected void attachBaseContext(Context newBase) {
    // 国际化适配（绑定语种）
    super.attachBaseContext(MultiLanguages.attach(newBase));
}
```

> 只要是 Context 的子类都需要重写，Service 也雷同，这里不再赘述

#### 语种设置

```java
// 设置当前的语种（返回 true 需要重启 App）
MultiLanguages.setAppLanguage(Context context, Locale locale);

// 获取当前的语种
MultiLanguages.getAppLanguage(Context context);
```

#### 使用案例

```java
@Override
public void onClick(View v) {
    // 是否需要重启
    boolean restart;
    switch (v.getId()) {
        // 跟随系统
        case R.id.btn_language_auto:
            restart = MultiLanguages.setSystemLanguage(this);
            break;
        // 简体中文
        case R.id.btn_language_cn:
            restart = MultiLanguages.setAppLanguage(this, Locale.CHINA);
            break;
        // 繁体中文
        case R.id.btn_language_tw:
            restart = MultiLanguages.setAppLanguage(this, Locale.TAIWAN);
            break;
        // 英语
        case R.id.btn_language_en:
            restart = MultiLanguages.setAppLanguage(this, Locale.ENGLISH);
            break;
        default:
            restart = false;
            break;
    }

    if (restart) {
        // 我们可以充分运用 Activity 跳转动画，在跳转的时候设置一个渐变的效果
        startActivity(new Intent(this, LanguageActivity.class));
        overridePendingTransition(R.anim.activity_alpha_in, R.anim.activity_alpha_out);
        finish();
    }
}
```

#### 其他 API

```java
// 将 App 语种设置为系统语种（返回 true 需要重启 App）
MultiLanguages.setSystemLanguage(Context context);
// 获取系统的语种
MultiLanguages.getSystemLanguage();

// 对比两个语言是否是同一个语种（比如：中文的简体和繁体，英语的美式和英式）
MultiLanguages.equalsLanguage(Locale locale1, Locale locale2);
// 对比两个语言是否是同一个地方的（比如：中国大陆用的中文简体，中国台湾用的中文繁体）
MultiLanguages.equalsCountry(Locale locale1, Locale locale2);

// 获取某个语种下的 String
MultiLanguages.getLanguageString(Context context, Locale locale, int stringId);
// 获取某个语种下的 Resources 对象
MultiLanguages.getLanguageResources(Context context, Locale locale);
```

#### 作者的其他开源项目

* 安卓架构：[AndroidProject](https://github.com/getActivity/AndroidProject)

* 网络框架：[EasyHttp](https://github.com/getActivity/EasyHttp)

* 日志框架：[Logcat](https://github.com/getActivity/Logcat)

* 权限框架：[XXPermissions](https://github.com/getActivity/XXPermissions)

* 吐司框架：[ToastUtils](https://github.com/getActivity/ToastUtils)

* 标题栏框架：[TitleBar](https://github.com/getActivity/TitleBar)

* 悬浮窗框架：[XToast](https://github.com/getActivity/XToast)

#### Android技术讨论Q群：78797078

#### 如果您觉得我的开源库帮你节省了大量的开发时间，请扫描下方的二维码随意打赏，要是能打赏个 10.24 :monkey_face:就太:thumbsup:了。您的支持将鼓励我继续创作:octocat:

![](https://raw.githubusercontent.com/getActivity/Donate/master/picture/pay_ali.png) ![](https://raw.githubusercontent.com/getActivity/Donate/master/picture/pay_wechat.png)

#### [点击查看捐赠列表](https://github.com/getActivity/Donate)

## License

```text
Copyright 2019 Huang JinQun

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
