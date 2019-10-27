# 用户信息 

## 基类
### DTBaseViewController
#默认显示悬浮按钮showRadioFloat
#默认显示导航showNavigationBar
#- (void)bindInitialization; 初始化方法
#- (void)bindNotification; 注册通知方法
#- (void)bindViewConstraints; 写约束
#- (void)bindViewModel; viewModel 赋值
#- (void)fetchData; 获取网络请求

### DTBaseViewModel
#- (void)viewModelDidLoad; 初始化viewModel 的数据
#- (void)viewModelLoadNotifications; 
#controller 绑定控制器
#- (RACSignal *)requestRemoteDataSignal 重写requestRemoteDataCommand网络请求

### DTBaseView  view用懒加载方式创建，约束建议用masonry
#- (void)setupViews 添加subView
#- (void)setupViewConstraints 设置约束

### DTBaseModel 遵循了copy协议
#id 默认用ID替换

### DTBaseTableViewController 
#tableViewFrame 自定义tableView Frame
#requestHeadRemote 下拉刷新
#requestFootRemote 上拉加载请求

## 登录用户信息 （互联网中心）
#用户的中心编号 ShareManager.userId
#用户是否实名认证 ShareManager.certification 1:已认证 0:未认证
#登录页面相关的
#DSLoginAction 里面包含了跳转登录页面、清除用户信息的方法
#turnToLoginVC: 跳转登录页面
#checkCurrentUserHasLogin检查用户是否登录，没有登录时会跳转登录页面
#logOutClean: 退出登录，清除用户信息,主动退出清除直播间的数据
#clearWindowSubView:清理添加到window 上的视图，根据类名清理，如果有新添加的，需要更新当前方法
#loginSuccessBackgroundOperation 登录成功之后的操作，如请求用户在道上的信息和emoji表情
## 道上中心服务用户信息
#APPUserCenterShare  里面包含了用户在道上的用户信息
## 道上IM用户信息
#AppUserBeanShare 里面包含了用户在道上IM的用户信息，包含用户的token

# 跳转方法
#通知和linkme的跳转和系统消息通过DSControllerActionManager 进行跳转
#内部跳转都通过DSControllerAction 类调用方法
#注意：新模块需给DSControllerAction添加一个分类，将跳转方法都写到当前分类里面，如需要用户信息，在跳转方法里面判断登录


# 常用方法
## 提示
### MBProgressHUD 包含了普通提示，提示默认0.9s消失，如果不传view，默认添加到最后的window上
#showMulTextOnWindow 显示多行提示，需要换行的地方可认为加上\r\n
#showCompleteTitle:toView: 完成的提示
#showFailTitle:toView: 失败的的提示
#showCoinTitle:toView: 积分变动的的提示
#showSuccess 成功的提示，加在window上
#showSuccess:toView: 成功的提示，加在view上
### DSAlertTitleView 弹出框交互 （包含单行输入框，多行输入框）
#链式调用以 instance 方法开始，以makeShow 方法结束
#其他类方法正常使用

## 网络请求
#### baseUrl/url1都在Appmacro 文件里面
#HostCenter：互联网中心交互服务（登录服务）
#HostIM：群聊模块服务
#SystemMessagePath：系统消息服务
#ThirdPartyUrl：三方推广服务
#ActivityUrl：基础服务
#discoverUrl：发现服务
#HostShareWeb：分享服务-H5静态页面
#RadioUrl：电台相关服务
#MoneyUrl：红包服务
#HostGuess：竞猜服务

### DTBaseViewModel+Request  rac请求方式
#需要继承DTBaseViewModel
#rac_PostNetwork:baseUrl:params:loading: 

### 普通请求方式 SqHttpRequest
#postMd5Url1:url2:params:success:fail: 普通请求
#uploadImageUrl1:url2:image:success:fail:上传敏感图片

## 工具类 
###OSS上传图片 DSOSSManager
#封装了阿里的OSSSDK，用于向OSS服务器上传图片和视频，提供了上传图片和视频的公共方法和取消上传任务的方法。
#uploadVideo: success: failure: 上传视频，传递视频文件的沙盒路径
#uploadImage: compressionQuality: success: failure:上传图片，传递UIImage对象和压缩比例（0～1）


### View
#setCircularViewWithRadius: 画圆形图
#setCircularViewWithRadius:layerWidth:layerColor: 画圆形图，线宽和线色
#setCircleRectView:cornerRadii:已知fame画指定方向圆角
#setCircleRectView:cornerRadii:bounds:根据bounds画指定方向圆角
#snapshot 获取屏幕快照
#viewController 获取当前view的控制器
#lottieAnimationUrl:animationName: 加载lottie 动画

### UITextView
#zw_placeHolder： 提示信息
#zw_placeHolderColor: 提示信息颜色
#zw_placeHolderYoffset 提示信息y偏移
#zw_font 提示信息字体
#vertifyLength：rule： 字体长度验证，自动截取

### UIButton
#d_handleControlEvent:eventInterval:withBlock 延迟点击事件

### UILabel
#updateBadgeunreadCount 更新消息未读数 

### UIViewController
#goBack 返回 优先pop
#goBackAnimated： 返回 优先pop
#closeControllerAnimated： 返回优先dismiss

### UITabBarController
#switchToFirstIndexController 切换到发现
#switchToHomeRadioController 切换到电台首页
#switchToHomeTradeController 切换到生意首页
#switchToSquareController 切换到广场首页

### UIImage
#imageForColor: 根据颜色生产1*1的图片
#resizeImage 拉伸图片
#clipImageInRect: 给图片画圆角
#boxblurImage:withBlurNumber: 图片模糊处理

### UIAppliccation
#canOpenUrl 判断是否能打开链接
#openURL 打开其他应用

### UIColor
#colorAlpha: 设置颜色alpha
#color### 颜色

### UIFont
fontPingFangSCRegularWithSize:      pingFang-Regular  字体
fontPingFangSCMediumWithSize：      pingFang-Medium字体
fontSFProDisplayMediuWithSize：      SFProDisplay-Medium 字体
fontDINMediuWithSize：  DIN-Medium字体
fontDINBoldWithSize：    DIN-Bold 字体

### NSFileManager
#cacheSize 缓存文件大小
#claerCacheSize 删除缓存

### NSUserDefault
showTodayStatusOfCurrentUserId:defaultKey: 判断用户今天是否已经显示
updateTodayStatusOfCurrentUserId:defaultKey:记录用户今天已经显示
queryValueOfCurrentUserId:defaultKey: 获取key 对应的是否显示过
updateValue:userId:defaultKey: 更新或者保存已经显示

### NSError
#errorWithDesc:code: 生成错误信息

### String
#截取指定长度 [NSString stringLimitLength:10 text:text]

### NSDictionary
#toJsonString 转json字符串
#readLocalFileWithName: 从本地读取数据
#readLocalFileWithName：type： 从本地读取数据
#dictionaryWithDataObject： 对象转字典




# 场景问题
#新用户登录发生请求失败，原因：创建IM用户时超过限制，需要去融云后台删除一个测试账号

<<<<<<< HEAD
=======
道上沙盒测试账号：
姓名   账号     密码
测试3 daoshang03@126.com    Daoshang01
测试4 daoshang04@126.com    Daoshang01
测试5 daoshang05@126.com    Daoshang01
测试6 daoshang06@126.com    Daoshang01
测试7 daoshang07@126.com    Daoshang01
测试11 daoshang11@126.com    Daoshang01
>>>>>>> develop-2.5.1
