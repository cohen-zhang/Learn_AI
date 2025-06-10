# 开发人员 AI 增强指南

## 对 AI 定位
- AI 是开发人员的工具，我 + AI ，这时候 AI 不是开发人员的竞争对手，是对我们的增强，10x 效率的自己；
快速生成代码，能快速试错，但 Recept Or Reject 需要开发人员自己来决定权；
- AI 是开发人员的助手，但像 Copilot 名字的定位一样，你才是机长(pilot)
- AI 是开发人员的结对编程，是橡皮鸭，像 DeepSeek 这种给出思考过程，提供思路链
- AI 是开发人员的老师，但这个


## AI 开发效率提升
- AI 提升开发效率和转型
- AI 生成代码的技巧:
  - VS Code 插件
  - ChatGPT 应用
  - Curson 工具
- AI 生成代码的常见问题:
  - 幻觉(Hallucination)问题

## 技术框架掌握
- 公司组件熟悉:
  - DA 框架
  - DP 框架
  - BOSGW 框架

## 开发技能提升
- 高级开发 Review 代码的判断力
- Java 代码常见问题解决
- 业务领域知识掌握


# AI 开发 10x 提效 -极客时间

定性说明 AI 的阶段： 结对编程 ， Copilot 角色， 

提示词原则 

AI 生成代码质量评判

结构性语言

英文重要性， 中文提示词，回答还是英文

让 AI 学习业务代码风格
1. 让 Cursor 学习 @xx.文件 代码风格
2. 分两步，让 Cursor 学习并输出 @xx.文件或者文件夹下的 代码风格，

单元测试


##  生成完整的代码要求--提示词

生成完整的代码要求：
1、功能完整，不要漏掉任何细节代码，配置文件，sql等关键产物;
2、不要使用省略替代具体的代码实现;
3、生成创建整个工程目录和文件的bash脚本,同时将所生成的代码也写入脚本，脚本内封装一个通用写入方法,每次写入输出一行日志,可以一次性生成完整的项目,确保脚本一定是可以执行的,确保不出现脚本错误;


需要根据下面的要求生成完整代码：
技术栈： JDK21/MyBatis-Plus/SpringBoot/MySQL/

包路径：
- com.archforce.atp.bss.表名模块（下划线命名）； 比如 t_hms_account 表使用 com.archforce.atp.bss.hms_account
复杂查询实现可以使用 Mapper.xml 写 SQL 

管理功能根据表结构生成增删改查代码的提示词：

- Controller/Service/Entity/Mapper/Impl 所有类：都需要添加类注释
- Controller 类中的接口：必须添加方法注释，命名规范：模块管理-功能操作，比如证券账户管理-新增
- 所有接口返回统一响应格式：ResBody<T> ,其中查询接口返回 ResBody<PageResult<T>>
- 接口注解格式： @PostMapping("/hms_account/add", name="BM_01:证券账户管理-新增")
- 入参实体：必须以 Request，出参必须以 Response 后缀命名，并和数据库实体类包路径进行隔离
- 入参字段注释：Request 类和 Response 类的字段必须添加字段级中文注释
- 校验规范：类和接口字段的必填校验需使用 @NotNull 或 @NotBlank 注解进行说明，其它长度、格式校验请使用 JSR-303 校验规范注解补充


Service 层：
- Service 层：com.xx.service
- 方法注解：需要加事务 @Transactional(rollbackFor = Exception.class,transactionManager = "transactionManager"); 需要替换具体事务管理器名称，比如 baseTransactionManager
- HmsAccountServiceImpl extends ServiceImpl<HmsAccountMapper, HmsAccount> implements HmsAccountService
MySQL 表结构如下：

```sql
-- 对冲账户组表
DROP TABLE IF EXISTS `t_hms_account_group`;
CREATE TABLE t_hms_account_group (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    group_id VARCHAR(12) NOT NULL COMMENT '对冲账户组编码',  -- 业务主键为group_id，可根据实际修改
    group_name varchar(64) NOT NULL COMMENT '对冲账户组名称', 
    group_remark  varchar(64) DEFAULT NULL COMMENT '对冲账户组描述', 
    org_code varchar(64) NOT NULL COMMENT '所属组织编码',
    dma_account_type INT(1) NOT NULL COMMENT 'DMA账户类型：“DMA账户”，“非DMA”时拒单',
    short_share_efficiency INT(1) NOT NULL COMMENT '空头股份效率：0-空头开仓次日可平 1-空头开仓当日可平',
    is_allow_recall INT(1)NOT NULL COMMENT '是否允许被召回：0-不允许，1-允许',
    recall_priority INT(2) NOT NULL COMMENT '被召回优先级(数值越小代表优先级越高)',
    long_trading_ems_account_id VARCHAR(20) NOT NULL COMMENT '多头交易绑定柜台账户',
    `data_status` INT(1)DEFAULT 0 COMMENT '数据状态:-2:未更新,-1:删除,0:新增,1:已更新',
    `create_time` datetime DEFAULT CURRENT_TIMESTAMP COMMENT 'create_time',
    `create_user` varchar(64) COLLATE utf8mb4_bin DEFAULT NULL COMMENT 'create_user',
    `update_time` datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'update_time',
    `update_user` varchar(64) COLLATE utf8mb4_bin DEFAULT NULL COMMENT 'update_user',
    UNIQUE KEY unique_group_id (group_id)
    UNIQUE KEY unique_group_name (group_name)
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin COMMENT = '对冲账户组表' ROW_FORMAT = Dynamic;

```




第三方组件提供接口：POST 类型的 http://{ip}:{端口}/sql_execute 接口； 
接口作用：通过调用这个接口，用于把前端增删查改管理功能的  拼接构建为SQL 语句，作为参数传入； 
入参： 由 Controller 层增删查改实体入参拼接出的 sql ; 
入参示例：
{
  "sql":"select * from xxxx where x=param1 and y=param2" // 查询、修改、新增、删除
}
响应体：
{
  "code": "0000",
  "msg": "",
  "data": {
    //请求返回值
  }
}
要求：
封装一个放在 bss-common-framework 模块的 http 客户端接口,供各个 Controller 层做增删查改功能时调用此接口，包含 HTTP客户端配置（单例模式）, SQL构建工具类; 
参考 @HmsAccountController 类中的前端管理功能触发的查询、新增、修改、删除这几个场景示例，每种场景由 Contoller 层入参实体，拼接的 SQL 可能比较长： 
请给出示例代码,生成完整的代码要求：
1、使用中文回复
2、功能完整，不要漏掉任何细节代码，配置文件，sql等关键产物;
3、不要使用省略替代具体的代码实现;
4、生成创建整个工程目录和文件的bash脚本,同时将所生成的代码也写入脚本，脚本内封装一个通用写入方法,每次写入输出一行日志,可以一次性生成完整的项目,确保脚本一定是可以执行的,确保不出现脚本错误;


