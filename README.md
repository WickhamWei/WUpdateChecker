# WUpdateChecker
调用 Github API 实现 Java 应用程序检查更新  
请使用 GSON 库包
## 使用方法  
```
new WUpdateChecker(String 软件现在的软件版本号, String Github的API地址);
```
本项目的Github API地址是 https://api.github.com/repos/WickhamWei/WUpdateChecker/releases/latest  
你的项目的地址可能是 https://api.github.com/repos/你的名字/你的项目/releases/latest  
### 方法函数  
isUpToDate()  
- 返回 Boolean  
- 返回 true 时，可能已经是最新版本，可能网络连接失败。
- 返回 false 时，目前版本不是最新的版本。  

isNetworkNormal() （只能在 isUpToDate() 之后使用）
- 返回 Boolean  
- 返回 true 时，连接正常。
- 返回 false 时，连接失败。  

getNewestVersion()  （只能在 isUpToDate() 之后使用）
- 返回 String
- 返回最新版本的版本号  

getNewestVersionPTimeString()  （只能在 isUpToDate() 之后使用）
- 返回 String
- 返回最新版本的推送时间（东八区）  

### 实例代码  
```
WUpdateChecker updateChecker = new WUpdateChecker(WLogin.main.getDescription().getVersion(), WLogin.url);
if (updateChecker.isUpTodate()) {
	if (updateChecker.isNetworkNormal()) {
		WLogin.main.getLogger().info("WLogin 已是最新版本");
	} else {
		WLogin.main.getLogger().warning("WLogin 无法连接到 Github");
		WLogin.main.getLogger().warning("WLogin 无法检查更新");
	}
} else {
	WLogin.main.getLogger().info("WLogin 当前版本为 " + updateChecker.getCurrentVersionString());
	WLogin.main.getLogger().info("WLogin 最新版本为 " + updateChecker.getNewestVersionString() + " 发布于 "
			+ updateChecker.getNewestVersionPTimeString());
	WLogin.main.getLogger().info("请及时更新");
}
```
