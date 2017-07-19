# LKTrack_AOS
蓝港统计SDK 安卓版
# 统计SDK
----
### 一、环境配置
游戏或app接入统计SDK，需将压缩包中的jar包放到自己工程的lib目录下，并将Andoridmanifest.txt文件中的权限添加到自己工程Androidmanifest.xml文件中。

### 二、系统生命周期方法
请务必在游戏工程同名系统方法中调用
```java
  public static void onDestory() {
        LKInAppTrack.onDestory(this);
    }

    public static void onResume() {
        LKInAppTrack.onResume(this);
    }

    public static void onPause() {
        LKInAppTrack.onPause(this);
    }
```

### 四、接口

1. 激活（必接)  
eventType: LK\_TRACK\_ACTIVE  
eventValue:

 参数名 | 类型 | 描述
 -------|---------|-----------
 LKEventParamCompanyId | String  | 公司id
 LKEventParamChannelId | String  | 渠道id
 LKEventParamAdId | String  | 蓝港广告ID
 LKEventParamGameId | String  | 游戏ID
 LKEventParamAppId | String  | 应用ID
 LKEventParamGPUModle | String |显卡型号，不统计显卡信息可不传
 LKEventParamGPUMemorySize | String |显存大小，不统计显卡信息可不传
 LKEventParamGPUVersion | String | 显卡驱动版本，不统计显卡信息可不传
 示例：
```java
   eventValues.put(LKEventParamName.LKEventParamGameId, "1111"); // 游戏必传
   eventValues.put(LKEventParamName.LKEventParamChannelId, "2222"); // 必传
   eventValues.put(LKEventParamName.LKEventParamCompanyId, "3333"); // 可不传
   eventValues.put(LKEventParamName.LKEventParamAppId, "44444"); // 必传
   eventValues.put(LKEventParamName.LKEventParamAdId, "44444"); // 有则传

   LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_ACTIVE, eventValues);
```
 
2. 登录（必接)【成功、失败、取消】  
eventType: LK\_TRACK\_LOGIN\_SUCCESS  、LK\_TRACK\_LOGIN\_FAILURE  、LK\_TRACK_LOGIN\_CANCEL  
eventValue:  

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamPassportId | String  | 游戏内的userid
 LKEventParamPassportName | String  | 游戏内的username
 LKEventParamPassportType | String  | 账号类型
 LKEventParamPassportBalance | String  | 账号余额
 
 示例：
```java
   eventValues.put(LKEventParamName.LKEventParamPassportId, "11112313213");// 必传
   eventValues.put(LKEventParamName.LKEventParamPassportName, "13254512355");// 能获取就传，获取不到可不传
   eventValues.put(LKEventParamName.LKEventParamPassportType, "1");//可以不传
   eventValues.put(LKEventParamName.LKEventParamPassportBalance, "1000");// 能获取到就传
   
   LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_LOGIN_SUCCESS, eventValues);
```
 登录失败或取消示例：
```java
   eventValues.put(LKEventParamName.LKEventParamMessage, "msg");
   
   LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_LOGIN_FAILURE, eventValues);
```

3. 创建角色（必接）  
eventType: LK\_TRACK\_CREATE\_ROLE  
eventValue:

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamServerId | String  | 区服id
 LKEventParamServerName | String  | 区服名称
 LKEventParamRoleId | String  | 角色id
 LKEventParamRoleName | String  | 角色名称
 LKEventParamCreateRoleTime | String  | 创建角色时间
 LKEventParamRoleCareer | String  | 角色职业
 LKEventParamRoleGender | String  | 角色性别
 
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

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamServerId | String  | 区服id
 LKEventParamServerName | String  | 区服名称
 LKEventParamRoleId | String  | 角色id
 LKEventParamRoleName | String  | 角色名称
 LKEvetnParamRoleLevel | String  | 角色等级
 LKEventParamCreateRoleTime | String  | 创建角色时间
 LKEventParamRoleBalance | String  | 角色余额
 LKEventParamRoleCareer | String  | 角色职业
 LKEventParamRoleGender | String  | 角色性别
 LKEventParamRoleFaction | String  | 角色阵营
 LKEventParamRoleUnion | String  | 角色帮会
 
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

 参数名 | 类型 | 描述
 ----|------|----
 LKEvetnParamRoleLevel | String  | 角色等级
 LKEventParamRoleBalance | String  | 角色余额
 LKEventParamRoleFaction | String  | 角色阵营
 LKEventParamRoleUnion | String  | 角色帮会
 
 示例：
```java
     Map<String, Object> map = new HashMap<String, Object>();
     map.put(LKEventParamName.LKEvetnParamRoleLevel, "29");
     map.put(LKEventParamName.LKEventParamRoleBalance, "1000");
     map.put(LKEventParamName.LKEventParamRoleFaction, "阵营");
     map.put(LKEventParamName.LKEventParamRoleUnion, "青帮");
     
     LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_ROLE_UPGRADE, map);
```

6. 支付【成功、失败、取消】  
eventType: LK\_TRACK\_PURCHASE\_SUCCESS、LK\_TRACK\_PURCHASE\_FAILURE、LK\_TRACK\_PURCHASE\_CANCEL  
eventValue:

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamMoneyAmount | String  | 付费金额
 LKEventParamProductName | String  | 商品名称
 LKEventParamProductId | String  | 商品id
 
 示例：
```java
     Map<String, Object> map = new HashMap<String, Object>();
     map.put(LKEventParamName.LKEventParamProductId, "12132123");
     map.put(LKEventParamName.LKEventParamProductName, "砖石");
     map.put(LKEventParamName.LKEventParamMoneyAmount, "100");
     
     LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_PURCHASE_SUCCESS, map);
 ```

7. 登出（必接）  
eventType: LK\_TRACK\_LOGOUT  
eventValue:

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamMoney1 | String  | 当前下线时的金钱数1
 LKEventParamMoney2 | String  | 当前下线时的金钱数2
 LKEventParamExperience | String  | 当前经验值
 
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

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamCustomInfo | String  | 自定义参数（json字符串）
 
 示例：
 ```java
    Map<String, Object> map = new HashMap<String, Object>();
    map.put(LKEventParamName.LKEventParamCustomInfo, "json格式的字符串");
    
    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_CUSTOM, map);
```

9. 进入关卡（必接）  
eventType: LK\_TRACK\_PASS\_ENTER  
eventValue:

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamEnterTime | String  | 进入关卡时间
 LKEventParamPassId | String  | 关卡ID（如：坐骑副本，装备副本）
 LKEventParamKey1 | String  | 预留字段1
 LKEventParamKey2 | String  | 预留字段2
 LKEventParamKey3 | String  | 预留字段3
 
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
10. 完成关卡（必接）  
eventType: LK\_TRACK\_PASS\_RESULT  
eventValue:

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamResultTime | String  | 完成关卡时间
 LKEventParamPassId | String  | 关卡ID（如：坐骑副本，装备副本）
 LKEventParamKey1 | String  | 预留字段1
 LKEventParamKey2 | String  | 预留字段2
 LKEventParamKey3 | String  | 预留字段3
 LKEventParamResultId | String  | 结果，如：1 - 成功；2 - 失败
 
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
    
11. 固定事件（必接）  
eventType: LK\_TRACK\_FIXED\_EVENT  
eventValue:

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamEventGid | String  | 事件ID
 LKEventParamEventPid | String  | 事件父ID
 LKEventParamEventDesc | String  | 事件描述
 
示例：
```java
    Map<String, Object> map2 = new HashMap<String, Object>();
    map2.put(LKEventParamName.LKEventParamEventPid, "11211");
    map2.put(LKEventParamName.LKEventParamEventGid, "1");
    map2.put(LKEventParamName.LKEventParamEventDesc, "100");
    
    LKTrack.eventTrack(MainActivity.this, LKEventType.LK_TRACK_FIXED_EVENT, map2);
```
 
12. 日常运营活动  
eventType: LK\_TRACK\_SDK\_ACTIVITY  
eventValue:

 参数名 | 类型 | 描述
 ----|------|----
 LKEventParamActivityTime | String  | 参与活动时间，每变动一次记录一次
 LKEventParamActivityId | String  | 活动ID
 LKEventParamActivityType1 | String  | 活动子类型1（如：日常、运营、商业化）
 LKEventParamActivityType2 | String  | 活动子类型2（如：日常充值活动中A活动）
 LKEventParamActivityType3 | String  | 活动子类型3（如：日常充值活动中A活动下的A1项目）
 LKEventParamOperationType | String  | 操作类型（1 - 查看；2 - 参加；3 - 完成）
 LKEventParamKey1 | String  | 预留字段1
 LKEventParamKey2 | String  | 预留字段2
 LKEventParamKey3 | String  | 预留字段3
 
   示例：
```objective-c
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
    
