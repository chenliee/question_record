---------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------
>targetVersion 34，push notification （无法注册推送）
>
>targetVersion null （会弹通知有推送 但是过不了google player）
>
>targetVersion 33，加了notify插件 (会弹通知 有推送)
>``
>targetVersion 33 （收不到推送 打不开通知）
>
>targetVersion 33，push notification （注册推送，会有推送，但是会有推送丢失）
>
>~/.bash_profile
>
>---
>title: question
>markmap:
>  colorFreezeLevel: 2
>---
>
> ========================
> # 2025.02.
> 
> # 2025.02.07
> 1. flutter跨平台時用了 html等庫需要 判斷是否為web平台 才引入
> 2. 多模塊開發時 如果用了intl，需要使用multiple_localization
> ```
> class _S extends S {
>  static const _SDelegate delegate = _SDelegate();
> }
> class _SDelegate extends LocalizationsDelegate<S> {
>  const _SDelegate();
>  List<Locale> get supportedLocales {
>    return const <Locale>[
>      Locale.fromSubtags(languageCode: 'en'),
>      Locale.fromSubtags(languageCode: 'zh', countryCode: 'TW'),
>    ];
>  }
>  @override
>  bool isSupported(Locale locale) => _isSupported(locale);
>  @override
>  Future<S> load(Locale locale) {
>    return MultipleLocalizations.load(
>        initializeMessages, locale, (l) => S.load(Locale(l)),
>        setDefaultLocale: true);
>  }
>  @override
>  bool shouldReload(LocalizationsDelegate<S> old) {
>    return false;
>  }
>  bool _isSupported(Locale locale) {
>    for (var supportedLocale in supportedLocales) {
>      if (supportedLocale.languageCode == locale.languageCode) {
>        return true;
>      }
>    }
>    return false;
>  }
> }
> ```
>
> # 2025.01.24
> 1. pushReplacementNamed和popAndPushNamed本質執行工作一樣，區別在於動畫，前者是直接替換，後者是彈出當前 
>   進入新頁面
>
> # 2025.01.21
> 1. 如果定義命名路由的時候 不用const修飾路由，比如直接將參數放在類上，會導致textfield可以影響該頁面的重建
>   ```
> 	Path(Path.restaurantBookPage,
>  	(context, match, arguments) => const BookPage())
> 	Path(
>  	Path.restaurantBookPage,
>  	(context, match, arguments) => BookPage(
>        	restaurant: arguments['restaurant'],
>        	restaurantNo: arguments['restaurantNo'],
>      	)),       
> 	```
> 2. 场景： 键盘弹起的时候执行了showBottomSheet会导致 
>    使用ModalRoute.of(context)!.settings.arguments as Map<String, dynamic> 重建
>    用Get.arguments 则不会
>
> # 2025.01.07
> 1. 权限配置ios 需要配置3处
> 2. android如果授权了一次性权限 会导致app在后台，权限会被撤销然后kill
>
> # 2025.01.06
> 1. tabController  addListen会导致一次点击监听2次可以用indexChange判断
>    但滑动不会让indexChange变为false，滑动只是动画 不会影响索引
> 2. 
> 
> # 2024.12.27
> 1. BackdropFilter模糊器需要加到ClipRect里 才可以避免全屏模糊
> 
> # 2024.12.24
> 1. 
> 
> # 2024.12.23
> 1. applink只有外网情况下才可以通过验证
> 2. android启动图 在12之后会默认自带一个logo+背景图的启动图，此时如果要自定义启动图可以使用flutter navite splash
> 
> 
> # 2024.12.20
> 1. android配置applink 實現網頁跳轉app，
>    當時瀏覽器輸入url依舊重載url 無法跳轉 解決方法 >在url放個靜態文件，打開默認加載該url即可實現(暫時解決方法)
>    後面發現就算加了靜態文件也是因為瀏覽器問題 會導致applinks失效 選擇使用 靜態文件+schema的形式 打開app
> 2. 
> 
> # 2024.11.22
> 1. 不展示颜色是因为consul连接写法有区别
> 2. 解决11.21问题 是因为swagger-ui-dist
> 
> # 2024.11.21
> 1. midwayjs query参数因为swagger版本问题，
>   用3.15.1解决,后面出现了filter=[]>  sb这样的参数也是因为版本问题，但是没有找到具体哪个插件版本
> 
> # 2024.9.29
> 1. 如果在不該用的小部件裡面使用了expanded，debug模式只會警告，但是release模式會導致視圖無法渲染
>   ```
>   [+34470 ms] I/flutter (31195): type 'FlexParentData' is not a subtype 
>   of type 'StackParentData' in type >cast
> [   +1 ms] I/flutter (31195): #0     
> Positioned.applyParentData (package:flutter/src/widgets/>basic.dart:4345)
> [        ] I/flutter (31195): #1     
> RenderObjectElement._updateParentData (package:flutter/src/widgets/>framework.dart:6553)
> [        ] I/flutter (31195): #2     
> RenderObjectElement.attachRenderObject (package:flutter/src/widgets/>framework.dart:6594)
> [        ] I/flutter (31195): #3     
> RenderObjectElement.mount (package:flutter/src/widgets/>framework.dart:6458)
> [        ] I/flutter (31195): #4     
> MultiChildRenderObjectElement.mount (package:flutter/src/widgets/>framework.dart:6900)
> [        ] I/flutter (31195): #5      
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #6      
> Element.updateChild (package:flutter/src/widgets/framework.dart:3846)
> 
> [   +1 ms] I/flutter (31195): #7      
> ComponentElement.performRebuild (package:flutter/src/widgets/>framework.dart:5505)
> 
> [        ] I/flutter (31195): #8      
> Element.rebuild (package:flutter/src/widgets/framework.dart:5196)
> [        ] I/flutter (31195): #9      
> ComponentElement._firstBuild (package:flutter/src/widgets/>framework.dart:5462)
> 
> [        ] I/flutter (31195): #10     
> ComponentElement.mount (package:flutter/src/widgets/>framework.dart:5456)
> 
> [        ] I/flutter (31195): #11     
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #12     
> Element.updateChild (package:flutter/src/widgets/framework.dart:3846)
> 
> [        ] I/flutter (31195): #13     
> ComponentElement.performRebuild (package:flutter/src/widgets/>framework.dart:5505)
> 
> [        ] I/flutter (31195): #14     
> Element.rebuild (package:flutter/src/widgets/framework.dart:5196)
> [   +1 ms] I/flutter (31195): #15     
> ComponentElement._firstBuild (package:flutter/src/widgets/>framework.dart:5462)
> 
> [        ] I/flutter (31195): #16     
> ComponentElement.mount (package:flutter/src/widgets/>framework.dart:5456)
> 
> [        ] I/flutter (31195): #17     
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #18     
> MultiChildRenderObjectElement.inflateWidget (package:flutter/src/>widgets/framework.dart:6893)
> 
> [        ] I/flutter (31195): #19     
> MultiChildRenderObjectElement.mount (package:flutter/src/widgets/>framework.dart:6905)
> 
> [        ] I/flutter (31195): #20     
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #21     
> Element.updateChild (package:flutter/src/widgets/framework.dart:3846)
> 
> [        ] I/flutter (31195): #22     
> SingleChildRenderObjectElement.mount (package:flutter/src/widgets/>framework.dart:6758)
> 
> [        ] I/flutter (31195): #23     
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #24     
> Element.updateChild (package:flutter/src/widgets/framework.dart:3846)
> 
> [        ] I/flutter (31195): #25     
> SingleChildRenderObjectElement.mount (package:flutter/src/widgets/>framework.dart:6758)
> 
> [        ] I/flutter (31195): #26     
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #27     
> Element.updateChild (package:flutter/src/widgets/framework.dart:3846)
> 
> [        ] I/flutter (31195): #28     
> ComponentElement.performRebuild (package:flutter/src/widgets/>framework.dart:5505)
> 
> [        ] I/flutter (31195): #29     
> Element.rebuild (package:flutter/src/widgets/framework.dart:5196)
> [        ] I/flutter (31195): #30     
> ComponentElement._firstBuild (package:flutter/src/widgets/>framework.dart:5462)
> 
> [        ] I/flutter (31195): #31     
> ComponentElement.mount (package:flutter/src/widgets/>framework.dart:5456)
> 
> [        ] I/flutter (31195): #32     
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #33     
> Element.updateChild (package:flutter/src/widgets/framework.dart:3846)
> 
> [        ] I/flutter (31195): #34     
> ComponentElement.performRebuild (package:flutter/src/widgets/>framework.dart:5505)
> 
> [        ] I/flutter (31195): #35     
> Element.rebuild (package:flutter/src/widgets/framework.dart:5196)
> [        ] I/flutter (31195): #36     
> ComponentElement._firstBuild (package:flutter/src/widgets/>framework.dart:5462)
> 
> [        ] I/flutter (31195): #37     
> ComponentElement.mount (package:flutter/src/widgets/>framework.dart:5456)
> 
> [        ] I/flutter (31195): #38     
> Element.inflateWidget (package:flutter/src/widgets/>framework.dart:4335)
> 
> [        ] I/flutter (31195): #39     
> Element.updateChild (package:flutter/src/widgets/framework.dart:3840)
> 
> [        ] I/flutter (31195): #40     
> ComponentElement.performRebuild (package:flutter/src/widgets/>framework.dart:5505)
> 
> [        ] I/flutter (31195): #41     
> StatefulElement.performRebuild (package:flutter/src/widgets/>framework.dart:5643)
> 
> [        ] I/flutter (31195): #42     
> Element.rebuild (package:flutter/src/widgets/framework.dart:5196)
> [        ] I/flutter (31195): #43     
> BuildOwner.buildScope (package:flutter/src/widgets/>framework.dart:2904)
> 
> [        ] I/flutter (31195): #44     
> WidgetsBinding.drawFrame (package:flutter/src/widgets/>binding.dart:989)
> 
> [        ] I/flutter (31195): #45     
> RendererBinding._handlePersistentFrameCallback (package:flutter/src/>rendering/binding.dart:448)
> 
> [        ] I/flutter (31195): #46     
> SchedulerBinding._invokeFrameCallback (package:flutter/src/scheduler/>binding.dart:1386)
> 
> [        ] I/flutter (31195): #47     
> SchedulerBinding.handleDrawFrame (package:flutter/src/scheduler/>binding.dart:1311)
> 
> [        ] I/flutter (31195): #48     
> SchedulerBinding._handleDrawFrame (package:flutter/src/scheduler/>binding.dart:1169)
> 
> [        ] I/flutter (31195): #49     
> _invoke (dart:ui/hooks.dart:312)
> [        ] I/flutter (31195): #50     
> PlatformDispatcher._drawFrame (dart:ui/platform_dispatcher.dart:399)
> [        ] I/flutter (31195): #51     
> _drawFrame (dart:ui/hooks.dart:283)
> [        ] I/flutter (31195): Another exception was thrown: Instance of 'DiagnosticsProperty<void>'
>    ```
> 
> # 2024.9.13
> 1. navigator2 如果点击按钮，url没有变化 加上
>    ```
>    Router.neglect(navigatorKey.currentContext!, () {
>         setNewRoutePath(currentConfiguration);
>       });
>    ```
> 
> # 2024.9.6
> 1. collection插件相当于集合扩展类 可以简化函数操作
> 
> # 2024.9.2
> 1. flutter插件 ios swift编写的话 sence的代理是不会走的，需要在项目重写然后调用插件的该方法 （在app delegate的情况下）
> 2.  
> 
> # 2024.8.29
> 1. android kotlin Handler(Looper.getMainLooper()).post可以随时使用
>    launch(Dispatchers.Main)不行 得处于协程未结束
> 2.  特殊空個符號
> 3. git配置代理
>    ```
>    [user]
> 	name = chenliee
> 	email = 1067242400@qq.com
> 	[core]
> 		excludesfile = /Users/admin/.gitignore_global
> 	[difftool "sourcetree"]
> 		cmd = opendiff \"$LOCAL\" \"$REMOTE\"
> 		path = 
> 	[mergetool "sourcetree"]
> 		cmd = /Applications/Sourcetree.app/Contents/Resources/opendiff-w.sh 
> 		\"$LOCAL\" \"$REMOTE\" -ancestor >\"$BASE\" -merge \"$MERGED\"
> 		trustExitCode = true
> 	[commit]
> 		template = /Users/admin/.stCommitMsg
> 	[http]
> 		postBuffer = 20000000
> 		proxy = socks5://127.0.0.1:7890
> 	[init]
> 		defaultBranch = main
> 	[https]
> 		proxy = socks5://127.0.0.1:7890
> 	[merge "ours"]
> 		driver = true
> 	[http "https://github.com"]
> 		proxy = socks5://127.0.0.1:7890
>    ```
> 
> # 2024.8.28
> 1. sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
>    sudo xcodebuild -runFirstLaunch
> 2.    
> 
> # 2024.8.27
> 1. 更换模拟器运行 如果报错 可以尝试创建新的runner
> 2. 
> 
> # 2024.8.22
> 1. expanded_bottom_sheet搭配futureBuilder
> 2. 使用了jerpack compose替代xml布局，要升级项目
> 
> # 2024.8.19
> 1. video player当作为组件的时候 如果放大会导致页面重建
> 
> # 2024.8.16
> 1. textbutton padding移除
>    ```
>     style: TextButton.styleFrom(
>                               padding: EdgeInsets.zero,
>                               minimumSize: Size.zero,
>                               tapTargetSize: MaterialTapTargetSize.shrinkWrap,
>                               alignment: Alignment.centerLeft),
>    ```
> 2. 
> 
> # 2024.8.15
> 1. android14 問題，第一點即可解決
> 
> 
> # 2024.8.11
> 1. 订单创建跟支付时候传得uid好像跟签名有关系
> 2. 导航栏颜色可以通过代码修改
>    ```
>    AnnotatedRegion<SystemUiOverlayStyle>(
>       value: SystemUiOverlayStyle(
>         statusBarColor: Colors.white, // 状态栏颜色
>         systemNavigationBarColor: Colors.white, // 导航栏颜色
>         systemNavigationBarIconBrightness: Brightness.dark, // 导航栏图标颜色
>       ),
>    ```
> 
> # 2024.8.10
> 1. streambuilder里面 放 stateful不会重新执行initastate
> 2. 更改了 action之后 直接热更新 然后会导致这个报错
>    ```
>    Bad state: Stream has already been listened to.
> 	Each child must be laid out exactly once.
>    ```
> 
> # 2024.8.7
> 1. ios icon 需要在setting取消设置 include all app icon assets，以及assset配置
> 2. 
> 
> # 2024.7.31
> 1. navigator2.0 初始化的时候要先添加一个页面进去
> 2. streamBuilder跟 listview一起的时候 需要用listviewBuilder
> 
> # 2024.7.26
> 1. text的height 默認跟字頭大小有關
> 
> # 2024.7.18
> 1. dart里面 单引号有json字符串的表达
> 
> # 2024.7.17
> 1. debug模式 直接拔掉手机 不会退出app 调用课程课堂接口会 出现转圈圈情况，如果列表长度小于8就没问题 大于8就加载不出来
> 2. 
> 
> # 2024.6.22
> 1. 对象相同 判断的是引用地址 而不是内容，对象更新之后 地址会变化 所以要重写操作符
> 2. 不可以在迭代列表的时候修改列表
> 3. 
> 
> # 2024.6.20
> 1. textfield border 只会生效于 无下划线
> 2. 自定义error位置用formfield
> 3. provider如果需要保持状态需要用全局
> 
> # 2024.6.19
> 1. ```
>    A GlobalKey was used multiple times inside one widget's child list.
> 	The offending GlobalKey was: [LabeledGlobalKey<NavigatorState>#8c137]
> 	The parent of the widgets with that key was: Builder
> 	The first child to get instantiated with that key became: Navigator-[LabeledGlobalKey<>NavigatorState>#8c137]
> 	  dependencies: [HeroControllerScope, UnmanagedRestorationScope]
> 	  state: NavigatorState#07679(tickers: tracking 2 tickers)
> 	The second child that was to be instantiated with that key was: Builder
> 	A GlobalKey can only be specified on one widget at a time in the widget tree.
>  ```
>  2. \\　\\\ 一個錯誤的空白號
> 
> # 2024.6.17
> 1. 对象判断是直接用引用 除非更改操作符
> 
> # 2024.6.3
> 1. 美元符号少一条横线 是由于字体原因
> 
> # 2024.6.1
> 1. appbar的text如果填写了 会默认附带height：1.45和letterSpaceing：0.3
> 2. 
> 
> # 2024.5.31
> 1. 高德Android key在android mainfest里面配置的时候会对 release版本生效，debug不会
> 
> # 2024.5.30
> 1. 圖片過大 添加解決，原因是圖片過大
>    ```
>    memCacheHeight: 857,
>    memCacheWidth: 568,
>    ```
> 
> # 2024.5.29
> 1. List涉及到对象的时候需要用 List.form(res.map((e)=>e).toList)来深拷贝，
> .  如果涉及到behavior >subject需要用到encode和decode
> 
> # 2024.5.28
> 1. flutter for web 调get请求报错
>    [28 get current]
> 2. Navigator1.0 在web运行时会导致 刷新之后可以返回
>    Navigator2.0刷新之后不可以返回
> 
> # 2024.5.23
> 1. ```
>    [        ] Error connecting to the service protocol: failed to connect to http://127.0.0.1:59283/
>    [ +207 ms] the Dart compiler exited unexpectedly.
>    ```
> 2. clipBehavior: Clip.none
> 3. android 微信分享返回 白屏 因為添加了WxAPiEntry
> 4. 
> 
> # 2024.5.22
> 1. ```
>  No constructor '' declared in class 'null'.
> 	Receiver: null
> 	Tried calling: new ()
>  ```
> 2.
> 
> # 2024.5.20
> 1. 微信分享 不传图片Android会闪退 用抛出异常解决了,以及图片格式少加了个.
> 
> # 2024.5.18
> 1. 微信分享初步怀疑是 两个微信应用 一个是海外 一个是大陆 导致了内容的变化
> 2. 当添加了apple-app-site-association之后，优品完全分享不了，暂时没找到原因，用网上的插件也同理
> 
> # 2024.5.17
> 1. ```
> [        ] Could not build the precompiled application for the device.
> [   +1 ms] Uncategorized (Xcode):Timed out waiting for all destinations matching the provided 
>           destination >specifier to become available
>            	Ineligible destinations for the "Runner" scheme:
>            		{ platform:iOS, arch:arm64, id:00008020-001149943428003A, name:1, 
>            		error:Device is busy (>Preparing 1) }
>    ```
> 2. apple-app-site-association配置要放在域名或者.well-known下
> 3. universal link依赖iOS系统去官网下载配置的associate文件。这个时间是不可控的
> 4. 国外主体不可以分享文字类
> 5. 两台手机微信分享的配置不一样（在没有在ios handler里面添加）
>    [WXApi.handleOpen(url, delegate: MyWXDelegate(channel:channel));]
> 6. ```
> 	Showing All Messages
> 	Could not find or use auto-linked framework 'CoreAudioTypes': framework 'CoreAudioTypes' not found
> 
> 	Undefined symbol: _CTRadioAccessTechnologyCDMA1x
> 
> 	Undefined symbol: _CTRadioAccessTechnologyCDMAEVDORev0
> 
> 	Undefined symbol: _CTRadioAccessTechnologyCDMAEVDORevA
> 
> 	Undefined symbol: _CTRadioAccessTechnologyCDMAEVDORevB
> 
> 	Undefined symbol: _CTRadioAccessTechnologyEdge
> 
> 	Undefined symbol: _CTRadioAccessTechnologyGPRS
> 
> 	Undefined symbol: _CTRadioAccessTechnologyHSDPA
> 
> 	Undefined symbol: _CTRadioAccessTechnologyHSUPA
> 
> 	Undefined symbol: _CTRadioAccessTechnologyLTE
> 
> 	Undefined symbol: _CTRadioAccessTechnologyWCDMA
> 
> 	Undefined symbol: _CTRadioAccessTechnologyeHRPD
> 
> 	Undefined symbol: _OBJC_CLASS_$_CTTelephonyNetworkInfo
> 
> 	Linker command failed with exit code 1 (use -v to see invocation)
>  ```
>     新项目报错 添加CoreTelePhony.framework
>  7. 
> 
> 
> # 2024.5.16
> 1. List.from可以深拷贝，但是仅适用于基础类型，如果类型是object或者Map之类的 需要调用遍历map然后再调用toList()方法
> 
> # 2024.5.15
> 1. fittedBox可以讓組件縮小且佔用空間也縮小，transform只縮小視角
> 
> # 2024.5.13
> 1. [Cycle inside Runner; building could produce unreliable results.] 
>    移动enable fundation extension到copy >resource上
>    因为更新xcode15，然后携带之前小组件的问题？
> 2. 后面报错找不到Pod Runner 删除ios文件夹重新生成
> 
> # 2024.5.10
> 1. 找到搜索gradle的网址
> 2. 编辑完ios之后 需要clean重新pod
> 3. 
> 
> # 2024.56.8
> 1. 5月6号报错原因是因为 图片没有进行裁剪，以原尺寸放入导致内存爆了
> 2. 
> 
> # 2024.5.6
> 1. 之前的ios錯誤代碼 排查好像是ExtendedNetworkImageProvider的問題
>    [Exception: Could not decompress image.]
>    [Exception: Could not create Impeller texture.]
> 2. 
> 
> 
> # 2024.5.4
> 1. ```
>   [ +404 ms] Updating files.
> 	ERROR - 2024-05-04 10:34:07.966865
> 	PUT /dkNy7gpZIzI=/
> 	Error thrown by handler.
> 	Connection reset by peer
>     package:shelf/shelf_io.dart 138:16  handleRequest
>    ```
> 2. [dart run build_runner build]
> 3. [flutter packages pub run build_runner build --delete-conflicting-outputs]
> 
> # 2024.4.30
> 1. [The backing file has been modified outside of Xcode.]
> 2. ```
>     ERROR - 2024-04-30 09:16:50.613369
>     PUT /3ULHs6rihVU=/
>     Error thrown by handler.
>     Write failed
>     package:shelf/shelf_io.dart 138:16  handleRequest
>     ```
> 3. 另一個項目報 无效的源发行版：17，昨天的項目可以運行，修改了一會，昨天的項目也無法運行了
>    进入android项目修改 可运行但是在flutter项目下无法运行
>    在gradle.properties配置 
>    [org.gradle.java.home=/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home]>解決
> 4. ```
>     [   +1 ms] You are applying Flutter's app_plugin_loader Gradle plugin imperatively u
>     sing the apply >script method, which is deprecated. and will be removed in a future release. 
>     Migrate to applying >
>     Gradle plugins with the declarative plugins block: https://flutter.dev/go/flutter-gradle-plugin-apply
> 	[        ] FAILURE: Build failed with an exception.
> 	[        ] * What went wrong:
> 	[        ] A problem occurred configuring root project 'android'.
> 	[        ] > Could not resolve all dependencies for configuration ':classpath'.
> 	[        ]    > Could not create service of type OutputFilesRepository using 
> 	ExecutionGradleServices.createOutputFilesRepository().
> 	[        ]       > Cannot lock Build Output Cleanup Cache (/Users/admin/Desktop/project/
> 	flutter_member/>android/.gradle/buildOutputCleanup) as it has already been locked by this process.
> 	```
> 	进入/.gradle删除所有.lock文件 => flutter clean => flutter pub get
> 5.
> 
> # ios添加隐私协议 2024.4.29
> 1. fluttertoast
>    flutter_inappwebview
>    flutter_local_notifications
>    package_info
>    path_provider
> 2. flutter for web 不可以直接用platform判断
> 3. 直接下载java 17然后android studio配置
> 4. [io.worker.3 (16): EXC_BAD_ACCESS (code=1, address=0x0)]
> 5. [#0	0x000000010bc62250 in flutter::ImpellerAllocator::allocPixelRef(SkBitmap*) ()]
> 6. 导致ios闪退原因好像是因为extendnetwork插件
> 7. 郵品項目更新了fluttertoast fluttertoast: ^8.0.9 -> 8.2.5
>    package_info_plus: 4.2.0 -> package_info_plus: ^6.0.0
> 
> 
> 
> # 2024.4.26
> 1. ```dart
>    SliverOverlapAbsorber(
>         handle: NestedScrollView.sliverOverlapAbsorberHandleFor(context),
>         sliver: header == null
>             ? null
>             : header!(context, innerBoxIsScrolled, tabs: tabs),
>       ),
>    ```
>    该代码会影响布局
> 2. 高德地圖sdk 需要用本地包 因為3dmap跟location有衝突包
> 	[loacation 更換為implementation 'com.amap.api:3dmap:10.0.600'] 
> 	[map 更換為 implementation 'com.amap.api:3dmap:10.0.600']
> 	[search 更換為 implementation 'com.amap.api:search:9.7.0']
> 
> # 2024.4.25
> 1. device info plus 等插件升级到java17
> 2. 处理当ios返回到后台时超过请求 接收时间而导致的请求超时
> 3. 更新版本後報錯
> 4. pop install報錯：[!] CocoaPods could not find compatible versions for pod "TXIMSDK_Plus_iOS":
>   	In snapshot (Podfile.lock):
>     	TXIMSDK_Plus_iOS (= 7.9.5666, >= 7.9.5666)
> 
>   	In Podfile:
>     	tencent_cloud_chat_sdk (from `.symlinks/plugins/tencent_cloud_chat_sdk/ios`) was resolved to 7.0.0, >which d epends on
>       	TXIMSDK_Plus_iOS (>= 7.9.5680)
> 
> 	You have either:
>  	* out-of-date source repos which you can
>     update with `pod repo update` or with `pod install >--repo-update`.
>  	* changed the constraints of dependency `TXIMSDK_Plus_iOS` 
>  	  inside your development pod `>tencent_cloud_chat_sdk`.
>    You should run `pod update TXIMSDK_Plus_iOS` to apply changes you've made.
> 5. Exception: Could not create Impeller texture.
> 6. io.worker.1 (16): EXC_BAD_ACCESS (code=1, address=0x0)
>    [->  0x10c56a250 <+164>: ldr    x8, [x0]]
> 
> 
> # 2024.4.24
> 1. xcode报错o.worker.2 (19): EXC_BAD_ACCESS (code=1, address=0x0)
>    [->  0x1fa2b9a90 <+136>: mov    x1, x0]
> 
> # 2024.4.23
> 1. 在2月份的时候出现过键盘弹起更改布局的问题,部分原因是MediaQuery,及是否用context
> 2. xcode报错o.worker.5 (19): EXC_BAD_ACCESS (code=1, address=0x0)
> 
> # 2024.4.22
> 1. flutter更新到3.19.6，flutter screen util導致了路由於鍵盤交互的重建
> 2. modalRoute也會導致莫名其妙的重建，自定義modalRoute
> 3. ios默認的為path_provider_ios 需手動更換為path_provider_fundation
> 4. ui會默認變成material3
> 5. material3 appbar elevation属性取消 且滑动会增大 tabBarTheme會自帶下劃線 
> 6. 
> 
> # 2024.4.18
> 1. 我的頁面將streamBuilder拆開之後 首次登陸出現報錯 (暫未研究)
> 	[Failed assertion: line 882 pos 14: '_childElements.containsKey(index)': is not true.]
> 	[Failed assertion: line 257 pos 16: 'child == null || indexOf(child) > index': is not true.]
> 
> 
> ----------------------------------------------------------------------------------------------------------
> ----------------------------------------------------------------------------------------------------------
> # git
> 1. git commit --amend [追加提交]
> 
> 2. git remote set-url --add 仓库名  仓库地址 [追加新仓库]
> 3. git push 仓库名 分支名 [指定仓库提交]
> 4. git remote rm  仓库名 [删除仓库]
> 
> 5. git reflog [得到记录]
> 6. git reset --hard 提交号 [恢复版本号] 
> 
> 7. git push origin --delete branch [删除远程分支]
> 8. git branch -d 分支名字 [删除本地分支]
> 9. git fetch [刷新分枝]   
> 10. git config --global merge.名称.driver true [定义驱动]
> 11. 新建.gitattributes，build.gradle merge=mydrive [合并忽略文件]android/build.gradle merge=pro
> android/app/src/main/AndroidManifest.xml merge=pro
> 12. git config --global --list [查看config]
> 13. git push -f github v2
> 14. git rm -r --cached .
>     git add .
>     git commit -m 'update .gitignore'
> 15. git update-index --assume-unchanged 假定文件从不修改
>     git update-index --no-assume-unchanged 取消假定
>     git ls-files -v | grep ^[[:lower:]] 查看取消跟蹤列表，報錯需setopt no_nomatch
> 
> ----------------------------------------------------------------------------------------------------------
>
> # jks
> 1. keytool -genkey -v -keystore ~/pushTest.jks -keyalg RSA 
>    -keysize 2048 -validity 10000 -alias pushTest storetype jks
> 2. keytool -genkeypair -v -keystore your_keystore_name.keystore 
>    -keyalg RSA -keysize 2048 -validity 3650 alias your_alias_name
> 3. ./gradlew signingReport
> 4. keytool -importkeystore -srckeystore /your-path/demo.jks 
> -srcstoretype JKS -deststoretype PKCS12 destkeystore /your-path/client.p12
> 5. keytool -importkeystore -srckeystore /your-path/client.p12 
> -srcstoretype PKCS12 -destkeystore /your-path>/demo.keystore -deststoretype JKS
> 6. keytool -importkeystore -srckeystore ./pushTest.jks 
> -srcstoretype JKS -deststoretype PKCS12 destkeystore ./client.p12 
> 7. adb shell dumpsys package d 查看android applinks 
> 
> ----------------------------------------------------------------------------------------------------------
>
> # SHA1
> 1. keytool -list -v -keystore 你的keystore文件的绝对路径 
> 
> ----------------------------------------------------------------------------------------------------------
>
>
> # 安装brew
> 1. /bin/bash -c "$(curl -fsSL raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
> 2. brew install jq [安装jq]
> 
> ----------------------------------------------------------------------------------------------------------
>
> 
> 1. org.gradle.jvmargs=-Xmx1536M
> 2. android.useAndroidX=true
> 3. android.enableJetifier=true
> 4. org.gradle.java.home=/Users/chen/Desktop/java/jdk-17.0.12.jdk/Contents/Home
> 5. adb shell pm set-app-links --package com.catchgold.ezfun 0 all
> 6. adb shell pm verify-app-links --re-verify com.catchgold.ezfun2> 
>
>
>
>
>
> 
> 
> 