# LKTrack_Android
蓝港统计SDK 安卓版
# 统计SDK
----
### 一、环境配置
游戏或app接入统计SDK，需将压缩包中的jar包放到自己工程的lib目录下，**在压缩包中找对应地区的配置文件放到自己工程对应的assets目录下**（如果不放配置文件默认用中国大陆的服务器），并将Andoridmanifest.txt文件中的权限添加到自己工程Androidmanifest.xml文件中。

### 二、系统生命周期方法
请务必在游戏工程同名系统方法中调用
```java
  public static void onDestroy() {
        LKTrack.onDestroy(this);
    }

    public static void onResume() {
        LKTrack.onResume(this);
    }

    public static void onPause() {
        LKTrack.onPause(this);
    }
```

### 三、接口

1. 激活（必接)  
eventType: LK\_TRACK\_ACTIVE  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 --------|--------|--------|--------
 LKEventParamChannelId | String  | 渠道id | 必传
 LKEventParamGameId | String  | 游戏ID | 必传
 LKEventParamAppId | String  | 应用ID |必传
 LKEventParamAdId | String  | 蓝港广告ID，可传空 | 非必传
 LKEventParamGPUModle | String |显卡型号，不统计显卡信息可不传 | 非必传
 LKEventParamGPUMemorySize | String |显存大小，不统计显卡信息可不传 | 非必传
 LKEventParamGPUVersion | String | 显卡驱动版本，不统计显卡信息可不传 | 非必传

 示例：
```java
   eventValues.put(LKEventParamName.LKEventParamGameId, "1111"); // 游戏必传
   eventValues.put(LKEventParamName.LKEventParamChannelId, "2222"); // 必传
   eventValues.put(LKEventParamName.LKEventParamAppId, "44444"); // 必传
   eventValues.put(LKEventParamName.LKEventParamAdId, "44444"); // 有则传

   LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_ACTIVE, eventValues);
```
 
2. 登录（必接)【成功、失败、取消】  
eventType: LK\_TRACK\_LOGIN\_SUCCESS  、LK\_TRACK\_LOGIN\_FAILURE  、LK\_TRACK_LOGIN\_CANCEL  
eventValue:  

 参数名 | 类型 | 描述 | 是否必传
 ----|------|-----|------
 LKEventParamPassportId | String  | 游戏内的userid | 必传
 LKEventParamPassportName | String  | 游戏内的username | 必传
 LKEventParamPassportType | String  | 账号类型 | 非必传
 LKEventParamPassportBalance | String  | 账号余额 | 非必传
 
 示例：
```java
   eventValues.put(LKEventParamName.LKEventParamPassportId, "11112313213");// 必传
   eventValues.put(LKEventParamName.LKEventParamPassportName, "13254512355");// 必传
   eventValues.put(LKEventParamName.LKEventParamPassportType, "1");//可以不传
   eventValues.put(LKEventParamName.LKEventParamPassportBalance, "1000");// 能获取到就传
   
   LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_LOGIN_SUCCESS, eventValues);
```
 登录失败或取消示例：
```java
   eventValues.put(LKEventParamName.LKEventParamMessage, "msg");
   
   LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_LOGIN_FAILURE, eventValues);
```

3. 创建角色（非必接）  
eventType: LK\_TRACK\_CREATE\_ROLE  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|------
 LKEventParamServerId | String  | 区服id | 必传
 LKEventParamServerName | String  | 区服名称 | 必传
 LKEventParamRoleId | String  | 角色id | 必传
 LKEventParamRoleName | String  | 角色名称 | 必传
 LKEventParamCreateRoleTime | String  | 创建角色时间 | 非必传
 LKEventParamRoleCareer | String  | 角色职业 | 非必传
 LKEventParamRoleGender | String  | 角色性别 | 非必传
 
 示例：
```java
     Map<String, Object> map = new HashMap<String, Object>();
     map.put(LKEventParamName.LKEventParamServerId, "1234");
     map.put(LKEventParamName.LKEventParamServerName, "大合服");
     map.put(LKEventParamName.LKEventParamRoleId, "132132132");
     map.put(LKEventParamName.LKEventParamRoleName, "阿道夫");
     map.put(LKEventParamName.LKEventParamCreateRoleTime, "16031213245");
     map.put(LKEventParamName.LKEventParamRoleCareer, "法师");
     map.put(LKEventParamName.LKEventParamRoleGender, "男");

     LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_CREATE_ROLE, map);
 ```
 
4. 进入游戏（必接）  
eventType: LK\_TRACK\_ENTER\_GAME  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|------
 LKEventParamServerId | String  | 区服id | 必传
 LKEventParamServerName | String  | 区服名称 | 必传
 LKEventParamRoleId | String  | 角色id | 必传
 LKEventParamRoleName | String  | 角色名称 | 必传
 LKEvetnParamRoleLevel | String  | 角色等级 | 必传
 LKEventParamCreateRoleTime | String  | 创建角色时间 | 非必传
 LKEventParamRoleBalance | String  | 角色余额 | 非必传
 LKEventParamRoleCareer | String  | 角色职业 | 非必传
 LKEventParamRoleGender | String  | 角色性别 | 非必传
 LKEventParamRoleFaction | String  | 角色阵营 | 非必传
 LKEventParamRoleUnion | String  | 角色帮会 | 非必传
 
 示例：
```java
     Map<String, Object> map = new HashMap<String, Object>();
     map.put(LKEventParamName.LKEventParamServerId, "1234");
     map.put(LKEventParamName.LKEventParamServerName, "大合服");
     map.put(LKEventParamName.LKEventParamRoleId, "132132132");
     map.put(LKEventParamName.LKEventParamRoleName, "阿道夫");
     map.put(LKEventParamName.LKEventParamCreateRoleTime, "16031213245");
     map.put(LKEventParamName.LKEventParamRoleCareer, "法师");
     map.put(LKEventParamName.LKEventParamRoleGender, "男");
     map.put(LKEventParamName.LKEvetnParamRoleLevel, "29");
     map.put(LKEventParamName.LKEventParamRoleBalance, "1000");
     map.put(LKEventParamName.LKEventParamRoleFaction, "阵营");
     map.put(LKEventParamName.LKEventParamRoleUnion, "青帮");
     
     LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_ENTER_GAME, map);
```

5. 角色升级（必接）  
eventType: LK\_TRACK\_ROLE\_UPGRADE  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|-----|------
 LKEvetnParamRoleLevel | String  | 角色等级 | 必传
 LKEventParamRoleBalance | String  | 角色余额 | 非必传
 LKEventParamRoleFaction | String  | 角色阵营 | 非必传
 LKEventParamRoleUnion | String  | 角色帮会 | 非必传
 
 示例：
```java
     Map<String, Object> map = new HashMap<String, Object>();
     map.put(LKEventParamName.LKEvetnParamRoleLevel, "29");
     map.put(LKEventParamName.LKEventParamRoleBalance, "1000");
     map.put(LKEventParamName.LKEventParamRoleFaction, "阵营");
     map.put(LKEventParamName.LKEventParamRoleUnion, "青帮");
     
     LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_ROLE_UPGRADE, map);
```

6. 支付【成功、失败、取消】（非必接）  
eventType: LK\_TRACK\_PURCHASE\_SUCCESS、LK\_TRACK\_PURCHASE\_FAILURE、LK\_TRACK\_PURCHASE\_CANCEL  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|------
 LKEventParamMoneyAmount | String  | 付费金额 | 非必传
 LKEventParamProductName | String  | 商品名称 | 非必传
 LKEventParamProductId | String  | 商品id | 非必传
 
 示例：
```java
     Map<String, Object> map = new HashMap<String, Object>();
     map.put(LKEventParamName.LKEventParamProductId, "12132123");
     map.put(LKEventParamName.LKEventParamProductName, "砖石");
     map.put(LKEventParamName.LKEventParamMoneyAmount, "100");
     
     LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_PURCHASE_SUCCESS, map);
 ```

7. 登出  
eventType: LK\_TRACK\_LOGOUT  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|-----
 LKEventParamMoney1 | String  | 当前下线时的金钱数1 | 非必传
 LKEventParamMoney2 | String  | 当前下线时的金钱数2 | 非必传
 LKEventParamExperience | String  | 当前经验值 | 非必传
 
 示例：
 
```java
    Map<String, Object> map = new HashMap<String, Object>();
    map.put(LKEventParamName.LKEventParamMoney1, "11");
    map.put(LKEventParamName.LKEventParamMoney2, "22");
    map.put(LKEventParamName.LKEventParamExperience, "33");
    
    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_LOGOUT, map);
```

8. 自定义事件  
eventType: LK\_TRACK\_CUSTOM  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|-----|------
 LKEventParamCustomInfo | String  | 自定义参数（json字符串） | 必传
 
 示例：
 ```java
    Map<String, Object> map = new HashMap<String, Object>();
    map.put(LKEventParamName.LKEventParamCustomInfo, "json格式的字符串");
    
    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_CUSTOM, map);
```

9. 进入关卡（非必接）  
eventType: LK\_TRACK\_PASS\_ENTER  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|-----
 LKEventParamEnterTime | String  | 进入关卡时间 | 必传
 LKEventParamPassId | String  | 关卡ID（如：坐骑副本，装备副本） | 必传
 LKEventParamKey1 | String  | 预留字段1 | 非必传
 LKEventParamKey2 | String  | 预留字段2 | 非必传
 LKEventParamKey3 | String  | 预留字段3 | 非必传
 
 示例：
```java
    Map<String, Object> map = new HashMap<String, Object>();
    map.put(LKEventParamName.LKEventParamEnterTime, "1612222454");
    map.put(LKEventParamName.LKEventParamPassId, "22");
    map.put(LKEventParamName.LKEventParamKey1, "key1");
    map.put(LKEventParamName.LKEventParamKey2, "key2");
    map.put(LKEventParamName.LKEventParamKey3, "key3");
    
    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_PASS_ENTER, map);
```
10. 完成关卡（非必接）  
eventType: LK\_TRACK\_PASS\_RESULT  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|------
 LKEventParamEnterTime | String  | 进入关卡时间 | 必传
 LKEventParamResultTime | String  | 完成关卡时间 | 必传
 LKEventParamPassId | String  | 关卡ID（如：坐骑副本，装备副本） | 必传
 LKEventParamKey1 | String  | 预留字段1 | 非必传
 LKEventParamKey2 | String  | 预留字段2 | 非必传
 LKEventParamKey3 | String  | 预留字段3 | 非必传
 LKEventParamResultId | String  | 结果，如：1 - 成功；2 - 失败 | 非必传
 
 示例：
```java
    Map<String, Object> map1 = new HashMap<String, Object>();
    map.put(LKEventParamName.LKEventParamEnterTime, "11211");
    map.put(LKEventParamName.LKEventParamResultTime, "100");
    map.put(LKEventParamName.LKEventParamPassId, "1");
    map.put(LKEventParamName.LKEventParamResultId, "1");
    map.put(LKEventParamName.LKEventParamKey1, "key1");
    map.put(LKEventParamName.LKEventParamKey2, "key2");
    map.put(LKEventParamName.LKEventParamKey3, "key3");
    
    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_PASS_RESULT, map);
```
    
11. 固定事件 （非必接） 
eventType: LK\_TRACK\_FIXED\_EVENT  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|------
 LKEventParamEventGid | String | 事件ID | 必传
 LKEventParamEventPid | String | 事件父ID | 非必传
 LKEventParamEventDesc | String | 事件描述 | 非必传
 
示例：
```java
    Map<String, Object> map2 = new HashMap<String, Object>();
    map2.put(LKEventParamName.LKEventParamEventPid, "11211");
    map2.put(LKEventParamName.LKEventParamEventGid, "1");
    map2.put(LKEventParamName.LKEventParamEventDesc, "100");
    
    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_FIXED_EVENT, map2);
```
 
12. 日常运营活动（非必接）
eventType: LK\_TRACK\_SDK\_ACTIVITY  
eventValue:

 参数名 | 类型 | 描述 | 是否必传
 ----|------|----|-----
 LKEventParamActivityTime | String | 参与活动时间，每变动一次记录一次 | 必传
 LKEventParamActivityId | String | 活动ID | 必传
 LKEventParamOperationType | String | 操作类型（1 - 查看；2 - 参加；3 - 完成）|必传
 LKEventParamActivityType1 | String | 活动子类型1（如：日常、运营、商业化） | 非必传
 LKEventParamActivityType2 | String | 活动子类型2（如：日常充值活动中A活动） | 非必传
 LKEventParamActivityType3 | String | 活动子类型3（如：日常充值活动中A活动下的A1项目） | 非必传
 LKEventParamKey1 | String | 预留字段1 | 非必传
 LKEventParamKey2 | String | 预留字段2 | 非必传
 LKEventParamKey3 | String | 预留字段3 | 非必传
 
   示例：
```java
    Map<String, Object> map = new HashMap<String, Object>();
    map.put(LKEventParamName.LKEventParamActivityTime, "11211");
    map.put(LKEventParamName.LKEventParamActivityId, "1");
    map.put(LKEventParamName.LKEventParamActivityType1, "1");
    map.put(LKEventParamName.LKEventParamActivityType2, "1");
    map.put(LKEventParamName.LKEventParamActivityType3, "1");
    map.put(LKEventParamName.LKEventParamOperationType, "1");
    map.put(LKEventParamName.LKEventParamKey1, "2");
    map.put(LKEventParamName.LKEventParamKey2, "3");
    map.put(LKEventParamName.LKEventParamKey3, "key3");

    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_ACTIVITY, map);
```
### 四、附录：
```java
public abstract interface LKEventType {
    public static final String LK_TRACK_ACTIVE = "lk_sdk_active";
    public static final String LK_TRACK_LOGIN = "lk_sdk_login";
    public static final String LK_TRACK_LOGIN_SUCCESS = "lk_sdk_login_success";
    public static final String LK_TRACK_LOGIN_FAIL = "lk_sdk_login_fail";
    public static final String LK_TRACK_LOGIN_CANCEL = "lk_sdk_login_cancel";
    public static final String LK_TRACK_LOGOUT = "lk_sdk_logout";
    public static final String LK_TRACK_CREATE_ROLE = "lk_sdk_create_role";
    public static final String LK_TRACK_ENTER_GAME = "lk_sdk_enter_game";
    public static final String LK_TRACK_ROLE_UPGRADE = "lk_sdk_role_upgrade";
    public static final String LK_TRACK_PURCHASE = "lk_sdk_purchase";
    public static final String LK_TRACK_PURCHASE_SUCCESS = "lk_sdk_purchase_success";
    public static final String LK_TRACK_PURCHASE_FAIL = "lk_sdk_purchase_fail";
    public static final String LK_TRACK_PURCHASE_CANCEL = "lk_sdk_purchase_cancel";
    public static final String LK_TRACK_USE_ITEM = "lk_sdk_use_item";
    public static final String LK_TRACK_REWARD = "lk_sdk_reward";
    public static final String LK_TRACK_CUSTOM = "lk_sdk_custom";
    public static final String LK_TRACK_PASS_ENTER = "lk_sdk_pass_enter";
    public static final String LK_TRACK_PASS_RESULT = "lk_sdk_pass_result";
    public static final String LK_TRACK_FIXED_EVENT = "lk_sdk_fixed_event";
    public static final String LK_TRACK_ACTIVITY = "lk_sdk_activity";
}

public class LKEventParamName {
    public static final String LKEventParamAdId = "lk_track_ad_id";
    public static final String LKEventParamAppId = "lk_track_app_id";
    public static final String LKEventParamGameId = "lk_track_game_id";
    public static final String LKEventParamChannelId = "lk_track_channel_id";

    public static final String LKEventParamGPUModel = "lk_track_gpu_model";
    public static final String LKEventParamGPUMemorySize = "lk_track_gpu_memory_size";
    public static final String LKEventParamGPUVersion = "lk_track_gpu_version";

    public static final String LKEventParamPassportId = "lk_track_passport_id";
    public static final String LKEventParamPassportName = "lk_track_passport_name";
    public static final String LKEventParamPassportType = "lk_track_passport_type";
    public static final String LKEventParamPassportBalance = "lk_track_passport_balance";

    public static final String LKEventParamServerId = "lk_track_server_id";
    public static final String LKEventParamServerName = "lk_track_server_name";
    public static final String LKEventParamRoleId = "lk_track_role_id";
    public static final String LKEventParamRoleName = "lk_track_role_name";
    public static final String LKEvetnParamRoleLevel = "lk_track_role_level";
    public static final String LKEventParamCreateRoleTime = "lk_track_role_create_time";
    public static final String LKEventParamDelRoleTime = "lk_track_role_del_time";
    public static final String LKEventParamRoleUnion = "lk_track_role_union";
    public static final String LKEventParamRoleBalance = "lk_track_role_balance";
    public static final String LKEventParamRoleCareer = "lk_track_role_career";
    public static final String LKEventParamRoleGender = "lk_track_role_gender";
    public static final String LKEventParamRoleFaction = "lk_track_role_faction";

    public static final String LKEventParamMoneyAmount = "lk_track_money_amount";
    public static final String LKEventParamProductId = "lk_track_product_id";
    public static final String LKEventParamProductName = "lk_track_product_name";

    public static final String LKEventParamMoney1 = "lk_track_money1";
    public static final String LKEventParamMoney2 = "lk_track_money2";
    public static final String LKEventParamExperience = "lk_track_exprience";
    public static final String LKEventParamMessage = "lk_track_message";

    public static final String LKEventParamCustomInfo = "lk_track_customInfo";

    public static final String LKEventParamPassId = "lk_track_pass_id";
    public static final String LKEventParamResultId = "lk_track_result_id";
    public static final String LKEventParamEnterTime = "lk_track_enter_time";
    public static final String LKEventParamResultTime = "lk_track_result_time";
    public static final String LKEventParamKey1 = "lk_track_key1";
    public static final String LKEventParamKey2 = "lk_track_key2";
    public static final String LKEventParamKey3 = "lk_track_key3";

    public static final String LKEventParamEventGid = "lk_track_event_gid";
    public static final String LKEventParamEventPid = "lk_track_event_pid";
    public static final String LKEventParamEventDesc = "lk_track_event_desc";

    public static final String LKEventParamOperationType = "lk_track_operation_type";
    public static final String LKEventParamActivityTime = "lk_track_product_activity_time";
    public static final String LKEventParamActivityId = "lk_track_product_activity_id";
    public static final String LKEventParamActivityType1 = "lk_track_product_activity_type1";
    public static final String LKEventParamActivityType2 = "lk_track_product_activity_type2";
    public static final String LKEventParamActivityType3 = "lk_track_product_activity_type3";
}
```
