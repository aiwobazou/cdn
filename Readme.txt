//游戏里数值类型结构体
message CurrencyItem {
	double val = 1;//数值
	int32 unit = 2;//数字单位idx 关联的UnitItem
}

//数值单位结构体
message UnitItem {
	double val = 1;//数值
	bytes unit = 2;//单位
}

//怪物分组结构体
message MonsterGroup {
	int32 id = 1;//索引
	int32 bossId = 2;//boos怪物索引
	repeated int32 ids = 3;//怪物数组索引
	repeated double spawnRate = 4;//怪物刷怪数组比例0.5就刷5个
}

//关卡结构体
message StageItem {
	int32 index = 1;
	int32 type = 2;//关联的GlobalConfig.stageType
	int32 stage = 3;//当前关卡
	int32 mapIdx = 4;//地图索引
	int32 monsterGroupId = 5;//怪物分组索引
	int32 killTime = 6;//boos击杀倒计时
	CurrencyItem hpBase = 7;//小怪血量
	CurrencyItem boosHpBase = 8;//boos血量
	CurrencyItem attakDamageBase = 9;//小怪攻击力,boos是10倍
	CurrencyItem gold = 10;//小怪金币奖励
	CurrencyItem boosGold = 11;//boos金币奖励
}
//技能结构体
message SkillsItem {
	int32 id = 1;//索引
	int32 quality = 2;//品质
	bytes icon = 3;//图标
	int32 prefabId = 4;//预设ID
	bytes name = 5;//技能名字
	bytes desc = 6;//技能描述
	int32 levelMax = 7;//技能最大等级
	double cooling = 8;//cd时间
	double continued = 9;//技能持续时间
	repeated double value = 10;//技能基础伤害数组对应描述里伤害类型
	repeated double valueIncrease = 11;//技能数值每级增量
}
//技能等级伤害结构体
message SkillLevelDamage {
	repeated CurrencyItem items = 1;//当前等级品质对应伤害数值数组
}

//英雄属性结构体
message HeroAttrType {
	bytes icon = 1;//属性图标
	bytes desc = 2;//属性描述
	repeated double value = 3;//属性每段对应数值数组
}

//英雄结构体
message HeroItem {
	int32 rarity = 1;//英雄品质
	bytes name = 2;//英雄名字
	int32 prefabId = 3;//预设ID
	bytes icon = 4;//英雄图标
	bytes skillName = 5;//技能名字
	bytes skilldesc = 6;//技能描述
	bytes skillIcon = 7;//技能图标
	int32 skillPrefabId = 8;//技能预设
	repeated double skillValue = 9;//技能伤害数值数组
	repeated int32 bonusKey = 10;//属性对应的类型数组
	repeated int32 bonusVal = 11;//属性对应的数值数组
}

//强化面板等级所需金币
message UpgradePanelLevelItem {
	repeated CurrencyItem damageItems = 1;//攻击力
	repeated CurrencyItem hpItems = 2;//血量
	repeated CurrencyItem hpRecoveryItems = 3;血量恢复
	repeated CurrencyItem attackSpeedItems = 4;//攻击速度
	repeated CurrencyItem critChanceItems = 5;//暴击率
	repeated CurrencyItem critPowerIems = 6;//暴击伤害
	repeated CurrencyItem multishot_1Items = 7;//连射
	repeated CurrencyItem multishot_2Items = 8;//三连射
}

//装备结构体
message EquipmentItem {
	int32 id = 1;
	int32 type = 2;
	bytes name = 3;
	bytes icon = 4;
	int32 rarity = 5;
	CurrencyItem equipValue = 6;
}

//装备强化结构体
message EquipmentReinforce {
	int32 id = 1;
	int32 reqCount = 2;
	CurrencyItem value = 3;
}

//同伴结构体
message CompanionItem {
	int32 id = 1;
	bytes name = 2;
	bytes icon = 3;
	int32 rarity = 4;
	CurrencyItem attackDamageRatio = 5;
	CurrencyItem attackDamageIncrease = 6;
	double attackSpeed = 7;
	repeated int32 companionFlags = 8;
}

//全局数据结构体
message GlobalConfig {
	repeated bytes mapItems = 1;//地图预设数据数组
	repeated MonsterGroup monsterItems = 2;//怪物分组数组
	repeated StageItem stageItems = 3;//关卡数据数组
	repeated UnitItem unitItems = 4;//数值类型数组
	repeated bytes stageType = 5;//关卡标题类型数组
	repeated SkillsItem skillsItems = 6;//技能数组
	repeated SkillLevelDamage skillLevelDamages = 7;//技能等级伤害结数组
	repeated bytes skillQualitys = 8;//技能品质数组
	repeated HeroAttrType heroAttrTypes = 9;//英雄属性数值数组
	repeated HeroItem heroItems = 10;//英雄数组
	repeated bytes heroRaritys = 11;//英雄品质数组
	UpgradePanelLevelItem upgradePanelLevelItem = 12;//面板强化等级对应数值
	UpgradePanelItem upgradePanelItem = 13;//面板强化基础数值
	repeated int32 HeroExpItems = 14;//英雄升级对应经验
	repeated EquipmentItem equipmentItems = 15;//装备基础数据
	repeated EquipmentReinforce equipmentReinforces = 16;//装备强化对应数值
	repeated CurrencyItemList equipmentLevelDamages = 17;//装备品质等级对应数值
	repeated CompanionItem companionItems = 18;//同伴基础数据
	repeated CurrencyItemList companionLevelDamages = 19;//同伴品质等级对应数值
}

//用户货币结构体
message UserCurrency {
	CurrencyItem coins = 1;//金币
	int32 diamonds = 2;//钻石
}

//用技能结构体
message UserSkill {
	int32 id = 1;//技能索引
	int32 level = 2;//技能等级
	int32 count = 3;//技能拥有多少个
	bool unlock = 4;//是否解锁
}
//用户英雄结构体
message UserHero {
	int32 id = 1;//英雄索引
	int32 level = 2;//英雄等级
	int32 exp = 3;//英雄经验
	bool unlock = 4;//是否解锁
}

//用户面板相关参数配置
message UserPanel {
	int32 weaponId = 1;//佩戴武器
	int32 armorId = 2;//佩戴防具
	int32 ringId = 3;//佩戴戒指
	repeated int32 skillIds = 4;//佩戴的技能数组
	repeated int32 skillUnlockValue = 5;//技能是否解锁1为解锁
	repeated int32 companionIds = 6;//同伴的技能数组
	repeated int32 companionUnlockValue = 7;/同伴是否解锁1为解锁
	int32 damageLevel = 8;//强化攻击力等级
	int32 hpLevel = 9;//强化体力等级
	int32 hpRecoveryLevel = 10;//强化体力恢复等级
	int32 attackSpeedLevel = 11;//强化攻击速度等级
	int32 critChanceLevel = 12;//强化暴击率等级
	int32 critPowerLevel = 13;//强化暴击伤害等级
	int32 multishot_1Level = 14;//强化连射等级
	int32 multishot_2Level = 15;//强化三连射等级
	int32 taskId = 16;//任务id
	int32 taskVal = 17;//记录当前任务数值
}

//用户装备结构体
message UserEquipment {
	int32 id = 1;
	int32 type = 2;
	int32 level = 3;
	int32 count = 4;
	bool unlock = 5;
}

//用户同伴结构体
message UserCompanion {
	int32 id = 1;
	int32 level = 2;
	int32 count = 3;
	bool unlock = 4;
}

//用户存档
message UserDataResponse {
	int32 code = 1;//服务器返回状态
	bytes accessToken = 2;//服务器返回凭证
	int64 userId = 3;//用户ID
	int32 stageIdx = 4;//当前关卡idx
	UserCurrency userCurrency = 5;//用户货币数组
	repeated UserSkill skills = 6;//用户技能数组
	int32 heroId = 7;//用户当前配备影响的索引
	repeated UserHero userHeros = 8;//用户英雄的数组
	UserPanel userPanel = 9;//用户面板相关参数配置
	repeated UserEquipment equipments = 10;//用户装备数组
	repeated UserCompanion companions = 11;//用户同伴数组
}


预设的描述
StageModeUI=关卡标题血量进度相关
BossRushModeUI=boos冲锋副本 标题 倒计时相关
GoldDungeonModeUI=金币副本标题 倒计时相关
DwarfGrandfatherModeUI=侏儒之王副本 标题 血条 倒计时相关
VillageModeUI=扫荡村庄副本 标题 倒计时相关
HealthBar=英雄 怪物 血条

技能index:
0=魔球[Particles/Skills/MissileTurretProjectile] - ok
1=硬币导弹[Particles/Skills/Projectile_Coin] - ok
2=史莱姆重压[Particles/Skills/PoundSlime] -ok
3=愤怒[sketAnimation/Skills/effect_skill_acheive] - ok
4=扔鸡蛋[Particles/Skills/ThrowEggProjectile] - ok
5=闪电[Particles/Skills/LightningStrikeBlue Variant] -ok
6=死神[sketAnimation/Skills/135_PlayerSkill_ReaperSlime] - ok
7=召唤海德拉[sketAnimation/Skills/10002_slime_skill_hydra][Particles/Skills/Projectile_Hydra] - ok
8=哥布林突击队[sketAnimation/Skills/201_goblin_legion] - ok
9=流星雨[Particles/Skills/MeteorProjectile] - 还原失败
10=炸弹蝙蝠[sketAnimation/Skills/128_PlayerSkill_flying][Particles/Skills/DropBombBatProjectile] -ok
11=炸弹史莱姆[sketAnimation/Skills/200_slime_bomb][Particles/Skills/NukeExplosionFire Variant] - 特效爆炸效果还原失败
12=烈焰[Particles/Skills/Explosion] - 还原失败
13=召唤恶灵[sketAnimation/Skills/skill_demon_spirit][Particles/Skills/Projectile_Devil] - OK
14=威慑[sketAnimation/Skills/203_HorrorSlime][Particles/Skills/HorrorSlime] - ok
15=飞鸟撞击[sketAnimation/Skills/29200_badbird][Particles/Skills/BigBirdProjectile] - ok
16=暴风雪[Particles/Skills/fx_SnowStorm] - ok
17=乌云[Particles/Skills/DarkCloud] - ok
18=闪耀彗星[Particles/Skills/fx_comet_nova] - ok
19=魔王降临[sketAnimation/Skills/NPC_devil][Particles/Skills/fx_fire_pillar] - ok
20=破勇者[Particles/Skills/fx_hyperbeam] - ok
