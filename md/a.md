# 规则注意
snk公式，从20240228号开始都用math_lib:ceil_ext/1,老公式如果要改由策划确认发起。

# buff挂载
1. 确定目标
2. 确认初始等级(公式计算用,去动态层数)-----表现不用
3. 确认层数
4. 是否正常加buff--`add1_is_can_/4` ()-----表现不用判定，一定加上，不免疫、反弹
   1. 否就结束跳出
5. 确认特性的`before_add_eff`配置，执行此字段效果-------表现不处理
6. host触发`HOOK_BEFORE_ADD_BUFF`（可改层数）---------表现不处理
7. 是新加、叠加、跳过 add2_repeat_/5
   1. 分支-只加层数
      1. 指令采集
      2. 记录目标被加此`buff_sid次数`
      3. 触发`HOOK_AFTER_BUFF_ONLY_ADD_LAYER`（buff只加层数后
   2. 分支-跳过破军表现要推送unity
      1. 指令采集
   3. 分支-新增、修改buff
      1. 根据`uninstall`字段配置计算del条件数据----表现不用，
      2. `item_buff:init/8`生成、初始/覆盖buff数据（走公式，算、设置属性）***------表现不用
      3. 修正buff的del检查列表-------------表现不用
      4. 特性`uninstall_r_f_die`注册时机数据------------表现不用
      5. 设置宿主状态（可优化不用都检查`state_type`字段）-----表现不用
      6. 指令采集
      7. 记录目标被加此buff_sid次数-------表现不用
      8. 时机`HOOK_BUFF_add`-------表现不用
      9.  `HOOK_AFTER_GIVE_BUFF`-------表现不用
      10. `HOOK_AFTER_BUFF_ADD`-------表现不用
      11. 飘字效果MA-`fs_add_buff_tips`----------fs_add_buff_tips配置，关联buff_sid,无实际使用(del)
      12. 关联buff和处理时机（只有新加才处理）-------表现不用

add1_is_can_/4
1. 取出`add_condition`字段条件
2. 设置obj
3. 计算1的`add概率`
4. 检查1的条件
   1. 条件不过就直接false返回函数
5. `HOOK_BUFF_add_before`触发确认 是否 免疫、反弹
   1. 反弹--->给sFUid完成加buff 
   2. 是否免疫
      1. 免疫是-->采集指令-->false返回函数
      2. 免疫否-->`{true,反弹结果}`返回函数

# buff删除规则（任一规则满足）
1. 次数删除（触发时机,瞬间attr的get--------（当前规则）时机触发后时机(BuffUid自己生效后),`处理一个,就检查del` *del规则*
      buff_act_times
      buff_get_times
     （手动）eff_add_times---效果器往buff上增加的次数

2. 大回合/小回合删除  （进入本次大回合、进入本次小回合）--------（当前规则）大、小回合后时机（所有这种buffUid）*del规则*
        ~~round_action（小回合、行动后）目标行动后，累计小回合+1 `改配置成big_r_num_big，不要此规则`~~
         big_r_num_big（大回合大于）、
         big_r_num（大回合大于等于）
         big_r_action（大回合有先/后手策略）卸载大回合内目标行动后 或 卸载大回合结束  ---行动前、行动后、大回合后（确保行动次数不够）
                  打标记：行动前（确定此刻上场，轻拳前）、行动中（）、行动后（自身技能用完，包含普功、重拳、必杀；不包含怒气、奥义）、
                  {k,{大回合,小回合,先、后手+前、中、后}}---5个时机点位覆盖式检查（大回合结束后、小回合结束后；前、中、后做了标记就马上检查是否卸载，后手包含先手条件）

3. 宿主死亡    (死亡时卸载 特性，源死del)--------（当前规则）死亡后时机
4. 效果删除------------效果器逻辑
5. buff_misc(`{buff_misc,limit_cure,'<=',0}`,限制回复上限)触发后卸载 -------（当前规则）时机触发后时机-----改成`effect_limit_cure效果扣到0时del表现`
6. 层数卸载buff_lay_num_less--------（当前规则）时机触发后时机------改成 `层数变动效果有3个 马上检查0层卸载，unity不再表现减层数，直接del表现,要检查此值为1`
7. ~~source_item_check   挂载Buff的技能、BuffUid存在--------（当前规则）时机触发后时机----改成`buffUid卸载后有关联卸载流程强del 其他uid1,2,3` *del规则*--需求暂无~~

~~round_action条件 round_action_big条件~~

---
# 普通hurt
1. HOOK_BEFORE_ATTACKING----del
2. 对抗属性---无 延时+持续伤害
3. HOOK_ATTACKING  （direct_damage   ---无 延时+持续伤害
4.  HOOK_BEFORE_CALC_HIT 无视本次攻击-命中 ---无 延时+持续伤害
5.  calc_hurt 计算伤害  ---差异 延时+持续伤害
6.  crit_and_block 暴击、格挡  ---无 延时+持续伤害
7.  HOOK_AFTER_CALC_HURT （direct_damage  ---无 延时+持续伤害
8.  记录伤害 本buff，damage_extend配置的record控制  ---无 延时+持续伤害
9.  （不改伤害量 的特性
    1. 是（设置扣血前血量、是否致死  -----要 延时
    2. 否（fs_hurt:before_de_hp/1
       1. %分摊伤害、免伤、减伤 HOOK_BEFORE_DE_HP  （DIRECT_DAMAGE才有  ----有 持续伤害
    3. HOOK_BEFORE_DE_HP2  强行免死  -------有 延时+持续伤害
10. 扣血 fs_hurt:de_hp/1
    1.  %免伤标记---------有 持续伤害
    2.  无视护盾特性，扣盾，盾事件 -------有 延时+持续伤害
    3.  需扣hp,
        1.  延迟伤害（开关，HOOK_BEFORE_DE_HP3  -------有 持续伤害 
        2.  不延迟扣血 de_hp1
    4.  after_de_hp/1
        1.  输出、承伤统计 （代码开关可控制）-------有 持续伤害，真正扣延伤时没有
        2.  时机触发 HOOK_CRIT  HOOK_BLOCK   ---无 延时+持续伤害
        3.  HOOK_AFTER_DE_HP---------------被延时不触发，真正扣延伤时触发；有 持续伤害
        4.  如果死亡，走死亡流程---------------被延时不触发，真正扣延伤时触发；有 持续伤害
    5.  盾破 HOOK_ATTR_SHIELD_AFTER_DEL -------有 延时+持续伤害
11. 增加生效次数  -------有 延时+持续伤害
12. 是(DIRECT_DAMAGE) -------被延时有，真正扣延伤时无+持续伤害无
    1.  HOOK_AFTER_HURT
    2.  反伤 吸血
    3.  HOOK_AFTER_GIVE_HURT
---
# 暴气
co_team_warth---值，可以放很多，消耗不完
每个卡有cd---根据公共大回合计算，有表现需求,用时算cd

---
触发次数（do效果前+1），生效次数(根据效果写)


de_hp---->时机hook_after_de_hp(条件,damage_mode/=生命移出)---->cure--->de_hp


# 伤害统计
1. 死神有buff转移，分摊伤害


# 信标
引爆数量：必杀技目标身上被引爆数量累计
战火洗礼 和 铁血：战斗中每引爆1个信标（宿主阵营累计整场战斗
火线：技能阵营方施放信标计数(层数)(type=20)


```xml
<start>
<效果器sid=xx生效>
指令<jjsjsjs>、buff变化<sid,buffUid,host,改/删>、属性变化<某人,属性index,值>
<end>
```
# snk被动技
```xml
<start>
<'opportunity', HookTypeId--5>
<p_skill_1,SFUid, SkillSid1, StyleSid, OldOutSeqId>

<start>
<效果器sid=xx生效>
buff变化<sid,buffUid,host,add>
<end>

<end>
```




**计算层的负载是云服务器商根据服务器的cpu负载来选tcp到某node**
# 战斗场次会占用cpu资源,下面战斗策略来避免波动
1. 集群系统配置 node下 "秒打战斗"有几个核可用
2. 代码cfg配置每个核可承载的战斗数量
3. 秒打战斗，随机node,队列控制，node下当时存在的 "秒打战斗数量"  小于  `核数*每核战斗数量`
4. 秒打战斗流程，
   1. 业务调用拉战斗的函数，进入秒打
   2. 超时统一 X秒返回 timeout
   3. 随机一个node，进入秒打队列(阻断并绑定返回的pid,在阻断pid接返回)
   4. 秒打出队（入队即出队|定时10ms出队），出队时检测当前node的  "秒打战斗数量"
   5. 秒打完成，返回战斗结果（根据绑定的pid返回）
5. 玩家拉起的需要网络操作技能的战斗，直接拉起
6. 玩家拉起的 秒打 并自动看录像的全自动战斗，走 "秒打战斗流程"
7. 服务器拉起，玩家没有网络消息同步等待的战斗,走 "秒打战斗流程"

# 后面优化方向 `专门的战斗层`，计算层node不会受战斗影响性能


```erlang
FightMaps0 = FightMaps#{
		'src' => Game,
		'fight_type' => 13,%测试用
		'role_uid_l' => [111111],
		'a_role_info' => [{uid, 5020042}, {name, "virtual_role"}, {role_style, 1}, {style, 1}],
		'b_role_info' => [{uid, 5020041}, {name, "virtual_role1"}, {role_style, 2}, {style, 2}],
		'need_video' => none,

		'fight_mode' => 4%秒打
	},
	try
      %FightMaps0中fight_mode=4,如果不传result_ma参数,就会同步阻塞fs_server:api_init到打完出结算maps#{}
		case fs_server:api_init(0, ServerId, FightMaps0) of
			Ret when is_map(Ref) ->
				Ret;
			Err ->
				?wolf_warn("fight_error2", [
                                       {'fight_maps', FightMaps},
                                       {'server_id', ServerId},
                                       {'catch', Err}]),
				error
		end
```
# 离场(吹飞)
1. 效果离场(先手时;后手时;行动外)，同buff
2. 回场时机点
   1. 队友死完时拉回()
   2. 离场时间到期（大回合;小回合）同buff
3. 离场的卡牌buff被动不触发（但大回合，小回合会del到期buff）

（1push前端Y,2bi抛出N,3录像0不记,4当失败，5当没打，6功能数据库,7战前消耗返回）

外网数据备份ftp地址
ftp地址：124.222.122.72
端口：22
用户密码：sftp_user/sftp_use
# 任务
- [x] 1、双try
- [x] 2、秒打返回
- [x] 3、负载策略
    - [x] 排队机制节点随机、
    - [x] 询问call、
    - [x] 强制排队cast，
    - [x] 超载报警log（报警时间延迟递增，注意循环日志问题）
- [ ] 战报记录随机种和玩家操作集

```html
收到日志,eventSid-->确认此eventSid上次落地时间
                        -->阀值内-->skip
                        -->阀值外-->log内容落地-->更新此eventSid落地时间
```
[beam热更](https://blog.csdn.net/ve12345/article/details/84701270)
# 属性公式
```erlang
扩展计算属性，结果是int,calc_ext_attr_val/3（配置匹配差异）
{'attr_layer', Args}
{'attr_layer', SelectId, Args}
{'attr_consume_layer', Args}
{'attr_layer', target, SelectId, Args}
{'attr_layer_self', SelectId, Args}
{'attr_layer_max', SelectId, Args, LayerMax}
{'attr_camp_layer', Target, SelectId, Args}
{'attr_camp_count', CampFlag, SelectId, Args}
{now_buff_or_skill_releaser, AttrK, CfgN}
{target, AttrK, CfgN}
{AttrK, CfgN}
{Camp, Calc, AttrK, CfgN}
{MaxMin, AttrK, N} 
计算属性，结果是kv列表,attr_list/3（配置+公式值的maps组合匹配差异）
{attr_relate, coeff, Key, CfgN}
{attr_relate, Key, CfgN}
{attr_relate, Key, CfgN}
{attr_relate, Key, CfgN, FixValue, Max, DivLayer}
{attr_relate_other, Key, OtherKey, CfgN, FixValue, Max, DivLayer}
{attr_relate_other, Key, OtherKey, CfgN, CfgMax} 
{attr_relate_other, Key, OtherKey, CfgN}
{Key, CfgN, FixValue, Max, DivLayer}
{Key, CfgN}
{max, Key, CfgN, Max}
{attr_relate, Key, CfgN}
{attr_relate_other, Key, OtherKey, CfgN, CfgMax}
{attr_relate_other, Key, OtherKey, CfgN}
{coeff, Key, CfgN}
{round_num_coeff, Key, CfgBaseVal, CfgVal, CfgMaxVal}
{Key, DiffVal, SingVal, NowVal}
{Key, DiffVal, SingVal, NowVal}
```
tt
-----
Revision: 5013
Author: zhengzhichun
Date: 2024年5月15日 14:11:04
Message:
初始时就胜利
----
Revision: 5007
Author: zhengzhichun
Date: 2024年5月14日 18:11:35
Message:
BLEACH-22553 转移效果器逻辑优化
----
Revision: 5004
Author: zhengzhichun
Date: 2024年5月14日 17:50:23
Message:
BLEACH-22596 effect_do_add_layer buff层数改变效果的buff类型字段支持区间填法
----
Revision: 5001
Author: zhengzhichun
Date: 2024年5月13日 17:22:28
Message:
地底修改，修正逻辑匹配
----


`sudo -u apache svn ci -m "ttttttttt" --username snk_server --password "1kQUJ99QDl"`

`robot_port:start(1001).`
`robot_lib:set_val(Logic, UserName, ?ROBOT_Role_Uid, RoleUid),`

死神平衡器svn用tt最新的

跨服\-传奇对决
--------------
(snk@192.168.22.9)2> cross_time:fun_first_open_date(4,1001).
1717707600
(snk@192.168.22.9)3> time_lib:show(1717707600).
"2024-06-07 05:00:00"
(snk@192.168.22.9)4> cross_server_db:get_c_open_time(1001).
1717448400
(snk@192.168.22.9)5> time_lib:show(1717448400).
"2024-06-04 05:00:00"
4号开的服，7号开功能，配置的3天,cross_server_db:get_c_open_time/1算法是4+3=7
