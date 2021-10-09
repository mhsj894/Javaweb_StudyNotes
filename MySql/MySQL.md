## DDL：操作数据库、表

1. 操作数据库：CRUD
   1. C(Create)：创建
      * 创建数据库：
        * create database 数据库名称;
      * 创建db4数据库，判断不存在，再创建
        * create database if not exists 数据库名称;
      * 创建数据库，并指定字符集
        * create database 数据库名称 character set 字符集名; 
      * 创建db4数据库，判断是否存在，并制定字符集为gbk
        * create database if not exists db4 character set gbk;
   2. R(Retrieve)：查询
      * 查询所有数据库的名称：
         * show databases;
      * 查询某个数据库的字符集：查询某个数据库的创建语句
         * show create database 数据库名称;
   3. U(Update)：修改
      * 修改数据库的字符集
        * alter database 数据库名称 character set 字符集名称;
   4. D(Delete)：删除
      * 删除数据库
        * drop database 数据库名称
      * 判断数据库存在，再删除
        * drop database if exists 数据库名称
   5. 使用数据库
      * 查询当前正在使用的数据库名称
        * select database();
      * 使用数据库
        * use 数据库名称;
2. 操作表
    1. C(Create)：创建

       1. 语法

          * create table 表名(列名1 数据类型1,列名2 数据类型2,...列名n 数据类型n);

          * 最后一列，不需要加逗号

          * 数据类型

            1. int：整数类型
               * age int,
            2. double：小数类型
               * score double(5 小数位数,2 小数点后面位数)
            3. date：日期，只包含年月日，yyyy-MM-dd,
            4. datetime：日期，包含年月日，时分秒，yyyy-MM-dd HH:mm:ss,
            5. timestamp：时间戳类型 包含年月日时分秒 yyyy-MM-dd HH:mm:ss,
               * 如果将来不给这个字段赋值，或赋值为null，则默认使用当前系统时间，来自动赋值
            6. varchar：字符串
               * name varchar(20)：姓名最大20个字符
               * zhangsan 8个字符 张三 2个字符

          * 创建表

            ``` sql
            create table student(
            	id int,
                name varchar(32),
                age int,
                score double(4,1),
                birthday date,
                insert_time timestamp
            );
            ```

          * 复制表
            * create table 表名 like 被复制的表名

          

    2. R(Retrieve)：查询

       * 查询某个数据库中所有的表名称
         * show tables;
       * 查询表结构
         * desc 表名;

    3. U(Update)：修改

       1. 修改表名

          ​	alter table 表名 rename to 新的表名;

       2. 修改表的字符集

          ​	 alter table 表名称 character set 字符集名称;

       3. 添加一列

          ​	alter table 表名 add 列名 数据类型;

       4. 修改列的名称和类型

          ​	 alter table 表名 change 列名 新列名 新数据类型;

          ​	 alter table 表名 modify 列名 新数据类型;

       5. 删除列

          ​	alter table 表名 drop 列名;

    4. D(Delete)：删除

       * drop table 表名;
    * drop table if exists 表名;

## DML：增删表中数据

1. 添加数据：

   * 语法

     * insert into 表名(列名1，列名2，...列名n) values(值1，值2，...值n);

     * 注意：

       1. 列名和值要一一对应。

       2. 如果表名后不定义列名，则默认给所有列添加值。

          ​	insert into 表名 values(值1，值2，...值n);

       3. 除了数字类型，其他类型需要需要使用引号(单双都可以)引起来。

2. 删除数据：

   * 语法：
     * delete from表名 [where 条件];
   * 注意：
     1. 如果不加条件，则删除表中所有数据。
     2. 如果要删除所有记录
        1. delete from 表名; -- 不推荐使用。有多少条记录就会执行多少条删除语句。
        2. TRANCATE TABLE 表名; -- 先删除表，然后再创建一个一模一样的表。

3. 修改数据：

   * 语法
     * update 表名 set 列名1 = 值1，列名2 = 值2，...[where ]
   * 主要：
     1. 如果不加任何条件，则会将表中所有记录全部修改。

## DQL：查询表中的记录

* select * from 表名;

1. 语法：

   ```sql
   select
   	字段列表
   from
   	表名的列表
   where
   	条件列表
   group by
   	分组字段
   having
   	分组之后的条件
   order
   	排序
   limit
   	分页限定
   ```

2. 基础查询

   1. 多个字段的查询

      ```sql
      select
      	字段1，字段2，字段n
      from
      	表名;
      ```

      * 注意：
        * 如果查询所有字段，则可以用*来代替字段列表。

   2. 去除重复：

      * DISTINCT 

   3. 计算列

      * 一般可以使用四则运算计算一些列的值。(一般只会进行数值型的计算)
      * ifnull(表达式1，表达式2)：null参与的运算，计算结果都为null
        * 表达式1：那个字段需要判断是否为null
        * 如果该字段为null后的替换值。

   4. 起列名：

      * as:也可省略
      
        ```sql
        -- 查询姓名和年龄
        SELECT
        	NAME, -- 姓名
        	age -- 年龄
        FROM
        	stu;
        
        SELECT score FROM stu;
        SELECT age FROM stu;
        
        -- 去除重复的结果集
        SELECT DISTINCT age FROM stu;
        SELECT DISTINCT NAME,age FROM stu;
        
        
        -- 计算age和id之和
        
        SELECT age,id,age + id FROM stu;
        -- 如果有null参与的运算，计算结果都为null
        SELECT age,id,age + IFNULL(id,0) FROM stu;
        
        -- 起别名
        
        SELECT age,id,age + IFNULL(id,0) AS 总分 FROM stu;
        
        SELECT age,id,age + IFNULL(id,0) AS 总分 FROM stu;
        SELECT age 年龄,id 编号,age + IFNULL(id,0)  总分 FROM stu;
        ```
      
        

3. 条件查询

   1. where子句后跟条件

   2. 运算符

      * '>  <  =  >=  <=  <>'

      * BETWEEN...AND

      * IN(集合)

      * LIKE：模糊查询

        * 占位符：
          * _：单个任意字符
          * %：多个任意字符

      * IS NULL

      * and或&&

      * or或||

      * not或!

        ```sql
        -- 查询年龄大于20岁
        SELECT * FROM stu WHERE age >= 20;
        
        -- 查询年龄等于20
        SELECT * FROM stu WHERE age = 20;
        
        -- 查询年龄不等于20
        SELECT * FROM stu WHERE age != 20;
        SELECT * FROM stu WHERE age <> 20;
        
        -- 查询年龄大于等于20 小于等于25
        SELECT * FROM stu WHERE age>=20 && age<=25;
        SELECT * FROM stu WHERE age>=20 AND age<=25;
        SELECT * FROM stu WHERE age BETWEEN 20 AND 25;
        
        -- 查询年龄30岁，20岁，25岁的信息
        SELECT * FROM stu WHERE age=30 OR age=20 OR age=25;
        SELECT * FROM stu WHERE age IN (30,20,25);
        
        -- 查询生日为null的
        SELECT * FROM stu WHERE birthday = NULL; -- 不对的。null不能使用=去判断
        SELECT * FROM stu WHERE birthday IS NULL;
        
        -- 查询生日不为null的
        -- 查询生日为null的
        SELECT * FROM stu WHERE birthday IS NOT NULL;
        
        -- 查询姓赵的有哪些？LIKE 
        SELECT * FROM stu WHERE NAME LIKE '赵%';
        
        -- 查询姓名第二个字是刚的人
        SELECT * FROM stu WHERE NAME LIKE '_刚%';
        
        -- 查询姓名是三个字的人
        SELECT * FROM stu WHERE NAME LIKE '___';
        
        -- 查询姓名中包含赵的人
        SELECT * FROM stu WHERE NAME LIKE '%赵%';
        ```

# 今日内容

1. DQL：查询语句
   1. 排序查询
   2. 聚合查询
   3. 分组查询
   4. 分页查询
2. 约束
3. 多表之间的关系
4. 范式
5. 数据库的备份和还原
# DQL：查询语句
   1. 排序查询

      * 语法：order by 子句
        * order by 排序字段1 排序方式1，排序字段2 排序方式2...
      * 排序方式
        * ASC：升序，默认的。
        * DESC：降序
      * 注意
        * 如果有多个排序条件，则当前面条件值一样时，才会判断第二条件

   2. 聚合函数：将一列数据作为一个整体，进行纵向的计算。

         1. count：计算个数

                  1. 一般选择非空的列：主键
                  2. count(*)

         2. max：计算最大值

         3. min：计算最小值

         4. sum：计算求和

         5. avg：计算平均值

            

      * 注意：聚合函数的计算，会排除null值

        * 解决方案：

          1. 选择不包含null的列进行计算

          2. IFNULL函数

             ``` sql
             SELECT * FROM stu ORDER BY age ASC; -- 顺序
             SELECT * FROM stu ORDER BY age DESC; -- 逆序
             
             -- 按照age年龄排名，如果年龄一样，则按照分数排名
             SELECT * FROM stu ORDER BY age ASC,score DESC;
             
             
             SELECT COUNT(birthday) FROM stu; -- 计算birthday不为空的个数
             
             SELECT COUNT(IFNULL(birthday,'2000-1-1')) FROM stu; -- 加上ifnull
             SELECT COUNT(id) FROM stu; -- 按照主键计算个数
             SELECT COUNT(*) FROM stu; -- 行里只要有一个子数据不为null就被算作一个数据
             
             SELECT MAX(age) FROM stu; -- 最大值
             SELECT MIN(age) FROM stu; -- 最小值
             
             SELECT SUM(age) FROM stu; -- 计算和
             SELECT AVG(age) FROM stu; -- 计算平均值
             ```

             

   3. 分组查询

         1. 语法：group by 分组字段;

         2. 注意：

               1. 分组之后查询的字段：分组字段、聚合函数

               2. where和having的区别？

                        1. where在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果则不会被查询出来。
                        2. where后不可以跟聚合函数，having可以进行聚合函数的判断。

                  ``` sql
                  -- 按照年龄分组，分别查询20、30岁同学的平均分
                  SELECT age,AVG(score) FROM stu GROUP BY age;
                  
                  -- 按照年龄分组，分别查询20、30岁同学的平均分,人数
                  SELECT age,AVG(score),COUNT(id) FROM stu GROUP BY age;
                  
                  -- 按照年龄分组，分别查询20、30岁同学的平均分 要求：分数高于100分，不参与分组
                  SELECT age,AVG(score),COUNT(id) FROM stu WHERE score<100 GROUP BY age;
                  
                  -- 按照年龄分组，分别查询20、30岁同学的平均分 要求：分数高于100分，不参与分组,分组之后，人数要大于两个人
                  SELECT age,AVG(score),COUNT(id) FROM stu WHERE score<100 GROUP BY age HAVING COUNT(id)>2;
                  
                  SELECT age,AVG(score),COUNT(id) 人数 FROM stu WHERE score<100 GROUP BY age HAVING 人数>2;
                  
                  ```

                  

   4. 分页查询

         1. 语法：limit 开始的索引，每页查询的条数;

         2. 公式：开始的索引 = (当前的页码-1)*每页显示的条数

         3. limit是一个MySQL的"方言"

            ``` sql
            -- 每页显示3条数据
            SELECT * FROM stu LIMIT 0,3; -- 第1页
            
            SELECT * FROM stu LIMIT 3,3; -- 第2页
            
            SELECT * FROM stu LIMIT 6,3; -- 第3页
            ```



## 约束

* 概念对表中的数据进行限定，保证数据的正确性、有效性和完整性。

* 分类

  1. 主键约束：primary key
  2. 非空约束：not null
  3. 唯一约束：unique
  4. 外键约束：foreign key

* 非空约束：not null，某一列的值不能为null

  1. 创建表时添加约束

     ``` sql
     CREATE TABLE stu(
     	id INT,
     	NAME VARCHAR(20) NOT NULL -- name为非空
     
     );
     ```

  2. 创建表完后，添加非空约束

     ``` sql
     -- 创建表完后，添加非空约束
     ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;
     ```

* 唯一约束：unique，某一列的值不能重复

  1. 注意：

     * 唯一约束可以有null值，但是只能由一天记录为null值

  2. 创建表时添加唯一约束

     ``` sql
     -- 创建表时添加唯一约束
     CREATE TABLE stu(
     	id INT,
     	phone_number VARCHAR(20) UNIQUE -- 手机号
     );
     ```

     

  3. 删除唯一约束

     ``` sql
     ALTER TABLE stu DROP INDEX phone_number;
     ```

  4. 创建表后添加唯一约束

     ``` sql
     -- 表创建完后，创建唯一约束
     ALTER TABLE stu MODIFY phone_number VARCHAR(20) UNIQUE;
     ```

* 主键约束：primary key

  1. 注意：

     1. 含义：非空且唯一
     2. 一张表只能有一个字段为主键
     3. 主键就是表中记录的唯一标识

  2. 创建表时，添加主键约束

     ``` sql
     create table stu(
     	id int PRIMARY KEY, -- 给id添加主键约束
         name varchar(20)
     );
     ```

  3. 删除主键约束

     ``` sql
     -- 删除主键
     -- 错误：alter table stu modify id int;
     ALTER TABLE stu DROP PRIMARY KEY;
     ```

  4. 创建完表后添加主键约束

     ``` sql
     -- 创建完表后，添加主键
     ALTER TABLE stu MODIFY id INT PRIMARY KEY;
     ```

     

 