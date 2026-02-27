# Minecraft-PVP

## 概述

Minecraft地图全职高手所使用的数据包，仅供指令学习使用  
By:ning_mengCC  
未经允许禁止搬运本数据包内指令到其他地图/服务器  
全职高手PVP地图已发布至网易地图资源  
欢迎下载体验！  

![图片](./image/a0e09df8-f1e9-4b78-8845-98062d86198f.png)  
![图片](./image/20260227105912(1).png)  
![图片](./image/20260227110146(1).png)  
![图片](./image/de9272f1-f2e2-4727-92e4-32869e695ea4(1).png)  

## 职业代码格式

如果您想为我们的地图自己编写职业的话，请按照以下格式制作：  

在jnX中（X为技能编号）：
~~~mcfunction
# 设置玩家技能1状态为激活（值为1）
scoreboard players set @s jn1 1
# 重置胡萝卜钓竿计数器
scoreboard players set @s luobo 0

# 中间段落编写技能效果

# 重置技能1冷却时间计数器
scoreboard players set @s jn1time 0
# 向玩家发送技能释放成功的提示信息
tellraw @s [{"text":"技能X<名称>释放成功","color":"yellow"}]
# X秒后执行技能结束函数
schedule function career:您的命名空间/jnXfinish Xs append
~~~

在jnXfinish中：
~~~mcfunction
# 重置技能状态并播放提示音效
execute as @a at @s if \
    score @s zhiye matches <职业id> if \
        score @s jn1time matches 329..361 run \
            scoreboard players set @s jn1 0

# 播放技能冷却完成的音效提示
execute as @a at @s if \
    score @s zhiye matches <职业id> if \
        score @s jn1time matches 329..361 run \
            playsound minecraft:block.note_block.pling master @s ~ ~ ~ 1 1 1

# 向玩家发送技能冷却完成的文字提示
execute as @a at @s if \
    score @s zhiye matches <职业id> if \
        score @s jn1time matches 329..361 run \
            tellraw @s [{"text":"技能X:吸血冷却时间结束","color":"yellow"}]

# 将技能冷却计时器设置为602以防止重复触发
execute as @a at @s if \
    score @s zhiye matches <职业id> if \
        score @s jn1time matches 329..361 run \
            scoreboard players set @s jn1time 362
~~~
其中，**329..361**分别是技能**冷却时间乘20后分别加减1**，重置必须**重置为冷却时间*20+2**
