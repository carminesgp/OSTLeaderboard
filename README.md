# OSTLeaderboard
> Version 1.0.0.2
> CraftlandStudio Version: v1.13.1(3693570)
> Author: carminesgp

# 概要
1. 提供API供写入玩家分数和实时查询
2. 进入游戏后自动拉取服务器数据，本地即时更新，之后适时上传回服务器
3. 自动轮换排行榜（AB榜切换实现清空排行榜）
4. 提供默认UI实体，用于显示排行榜

# 使用说明
1. `Assets\OSTLeaderboard\OSTLeaderboard.fcg`挂载到`Global`脚本列表
2. 检查`Assets\OSTLeaderboard\OSTLeaderboard.fcg`确认`配置常量`部分
3. 在`Data Storage Module`中建立对应的排行榜和数据表并核对名称
4. 检查`Assets\OSTLeaderboard\OSTLeaderboard.ui`将其注册脚本名称为`OSTLeaderboard`
5. 检查`Assets\OSTLeaderboard\OSTLeaderboard.ui`调整布局，并检查本地化文件`Assets\Localization\key.csv`
6. 发布地图，使数据表在服务器上生效
7. 调试运行，确认ui工作正常
8. 从你的ECA或FCG调用API，从`Global`调用`OSTLeaderboard.fcg`中的API
9. 测试API:`test_score_set`为每个玩家生成随机分数
10. 测试API:`player_score_set`
11. 测试API:`player_score_get`

# API 介绍
## 常用 API 列表
1. `player_score_set(player_id object, score_type int, score int)`
   - 功能：设置玩家分数
   - 参数：
     - player_id: 玩家ID
     - score_type: 分数类型（0-4）
     - score: 分数值
   - 用途：记录玩家得分

2. `player_score_get(player_id UUID, score_type int) int`
   - 功能：获取玩家分数
   - 参数：
     - player_id: 玩家ID
     - score_type: 分数类型（0-4）
   - 返回：玩家分数
   - 用途：查询玩家当前分数

3. `player_score_reset(id UUID, score_type int)`
   - 功能：重置玩家分数
   - 参数：
     - id: 玩家ID
     - score_type: 分数类型（0-4）
   - 用途：将玩家分数重置为默认值

4. `player_rank_get(id UUID, score_type int) int`
   - 功能：获取玩家排名
   - 参数：
     - id: 玩家ID
     - score_type: 分数类型（0-4）
   - 返回：玩家排名（从1开始）
   - 用途：查询玩家当前排名

5. `player_upload_data(player entity<Player>)`
   - 功能：立刻上传玩家数据到服务器
   - 参数：
     - player: 玩家实体
   - 用途：立刻将玩家数据同步到服务器，频繁使用可能会失败

6. `handle_leaderboard_switch_visible(id UUID)`
   - 功能：切换排行榜显示状态
   - 参数：
     - id: 玩家ID
   - 用途：显示/隐藏排行榜UI

7. `handle_tab_pressed(id UUID, score_type int)`
   - 功能：切换排行榜标签页
   - 参数：
     - id: 玩家ID
     - score_type: 分数类型（0-4）
   - 用途：切换显示不同类型的排行榜

8. `test_score_set(player_id UUID)`
   - 功能：测试用，设置随机分数
   - 参数：
     - player_id: 玩家ID
   - 用途：测试排行榜功能

9. `test_unit_test_1()`
   - 功能：运行单元测试
   - 测试内容：
     - 测试1：分数格式化功能
     - 测试2：时间相关函数（AB榜索引和周期计算）
     - 测试3：排行榜表配置检查
     - 测试4：排序设置检查
     - 测试5：显示格式检查
   - 用途：验证排行榜核心功能是否正常工作
