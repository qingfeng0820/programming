# 协作型过滤 （collaboration filtering）
    1. 搜集偏好
    2. 根据偏好构建计算相似度
      （欧几里德距离Euclidean Distance， 皮尔逊相关度 Pearson Correlation）
    3. 利用相似度做选择
    
## 推荐
应用协作型过滤做推荐

### 基于用户的协作型过滤做推荐
    1. 搜集每个用户偏好数据
    2. 对某个用户A：根据其偏好与他人的偏好，计算他人与该用户的相似度
    3. 为他人的可推荐偏好做评分 （score）
       （可推荐偏好需满足该偏好不是用户A已具有的偏好）
       对某个推荐偏好的评分：
       a. 找出所有有该推荐偏好的其他用户
       b. 利用这些用户对这个偏好的评分和与用户A的相似度计算这个推荐偏好的总评分
          评分 * 相似度
       c. 计算该推荐偏好的评分： 总评分/总相似度
          (用户1(评分 * 相似度) + .. + 用户n(评分 * 相似度))/(用户1相似度 + .. + 用户n相似度)
       d. 计算好每个推荐偏好的评分后，排序做成评分表。
       e. 利用该评分表给用户A做推荐
    
### 基于Item的协作型过滤做推荐
    1. 搜集每个用户偏好数据
    2. 对所有的Item（偏好）做Item相似度表： 利用所有用户对各个偏好的评分，计算每个偏好间的相似度 
      （当收集足够的数据后，这个相似度表趋向稳定， 因为Item种类（比如商品）会趋向稳定，可以不再更新而反复利用）
    3. 对某个用户A：根据其偏好搜索Item相似度表，获取相似的偏好用来做推荐（可推荐偏好需满足该偏好不是用户A已具有的偏好）
    4. 对获取的推荐偏好评分 
       a. 对与该推荐偏好相关的所有用户A的偏好的相似度来做计算总评分
          用户A的偏好的评分 * 相似度
       c. 计算该推荐偏好的评分： 总评分/总相似度
          (用户A偏好1(评分 * 相似度) + .. + 用户A偏好n(评分 * 相似度))/(与用户A偏好1相似度 + .. + 与用户A偏好n相似度)
       d. 计算好每个推荐偏好的评分后，排序做成评分表。
       e. 利用该评分表给用户A做推荐
       
### 两种协作型过滤做选择
    对于基于用户的协作型过滤需要数据密集，也就是每个用户要有较多的偏好，这样才能针对用户相似来做推荐。
    如果每个用户就那么一两个偏好，而且用户间偏好还不一样，那就找不到相似用户做不了推荐了。
    对于基于Item的协作型过滤是对所有Item以及所有用户对这些Item的评分做成Item相似度表，对数据密集不那么敏感。
    但是构建Item相似度表需要花费很长时间（需要积累数据，让Item相似度表趋向于稳定）。
