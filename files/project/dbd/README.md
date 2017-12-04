![image](http://cdn.happyjuzi.com/juzi-pc/pc1.6.2/img/new_logo.png)
# MYSQL数据库设计规范及原则
## 规范 
###     1、数据库命名规范
1. 采用26个英文字母(建议采用小写)和0-9的自然数(经常不需要，水平拆分或者备份数据库情况下需要)加上下划线'_'组成;
2. 命名简洁明确(建议长度不超过30个字符);
3. 例如：user, stat, log,也可以wifi_user, wifi_stat, wifi_log给数据库加个前缀;

###     2、数据库表名命名规范
1. 采用26个英文字母(建议采用小写)和0-9的自然数(经常不需要，水平拆分或者备份数据库情况下需要)加上下划线'_'组成;
2. 命名简洁明确,多个单词用下划线'_'分隔;
3. 例如：user_login, user_profile,user_detail,user_role,user_role_relation,user_role_right, user_role_right_relation表前缀'user_'可以有效的把相同关系的表显示在一起;
         
###     3、数据库表字段名命名规范
1. 采用26个英文字母(建议采用小写)和0-9的自然数(经常不需要)加上下划线'_'组成;
2. 命名简洁明确,多个单词用下划线'_'分隔;
3. 例如：user_login表字段 user_id, user_name, pass_word, eamil, tickit, status, mobile, add_time;
4. 表与表之间的相关联字段名称要求相同;

###    4、数据库表字段类型规范
1. 用尽量少的存储空间来存数一个字段的数据;
2.  例如：能使用int就不要使用varchar、char,能用varchar(16)就不要使用varchar(256);
3. IP地址最好使用int类型;
4. 固定长度的类型最好使用char,例如：手机号 char(11);
5. 能使用tinyint就不要使用smallint,int;
6. 最好给每个字段一个默认值,设置字段为not null; 

###     5、数据库表索引规范
1. 命名简洁明确,例如：user_login表user_name字段的索引应为user_name_index唯一索引;
2. 为每个表创建一个主键索引;
3. 为每个表创建合理的索引;

## 原则
### 1、核心原则
1. 不在数据库做运算;
2. cpu计算务必移至业务层;
3. 控制列数量(字段少而精,字段数建议在20以内);
4. 平衡范式与冗余(效率优先；往往牺牲范式)
5. 拒绝3B(拒绝大sql语句：big sql、拒绝大事务：big transaction、拒绝大批量：big batch);
 
### 2、字段类原则
1. 用好数值类型(用合适的字段类型节约空间);
2. 字符转化为数字(能转化的最好转化,同样节约空间、提高查询性能);
3. 避免使用NULL字段(NULL字段很难查询优化、NULL字段的索引需要额外空间、NULL字段的复合索引无效);
4.    少用text类型(尽量使用varchar代替text字段);

### 3、字段类原则
1. 合理使用索引(改善查询,减慢更新,索引一定不是越多越好);
2. 不在索引做列运算;
3. innodb主键推荐使用自增列(主键建立聚簇索引,主键不应该被修改,字符串不应该做主键)(理解Innodb的索引保存结构就知道了);
4. 不用外键(由程序保证约束);

### 4、sql类原则
1. 不用select *(消耗cpu,io,内存,带宽,这种程序不具有扩展性);
2. OR改写为IN(or的时间复杂度是o(n)级别);