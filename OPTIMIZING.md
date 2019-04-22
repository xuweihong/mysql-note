# 优化笔记

- hint 操作

  - HIGH_PRIORITY
    
    高优先级操作，主要用户 select 和 insert
    
  - LOW_PRIORITY
  
    低优先级操作,主要用于 select,delete,insert 和 update 操作中,只要访问的该表还有要执行的操作，即使先提交，也会比其他执行语句晚执行。
    
  - DELAYED
    
    只对 insert 和 replace 有效, MYSQL 会将结果立即放回给客户端，并将行数据放入缓冲区，并在表空闲时，将缓冲区数据批量写入。适合密集型 IO 操作,坏处是并不是所有的存储引擎都支持，而且不能返回自增id，会导致 LAST_INSERT_ID 不可用。
    
  - STRAIGHT_JOIN
  
    可以放在 select 语句的 select 关键字之后，也可以放在两个链表的名字之间,第一个用法是让查询中所有的表按照语句中出现的顺序关联，第二个方勇则是固定其前后两个表的关联顺序。
    
  - SQL_BIG_RESULT 和 SQL_SMALL_RESULT
  
    只对 select 语句有效,告诉优化器 group by 和 distinct 如何使用临时表及排序,SQL_BIG_RESULT 告诉优化器结果集很大，使用磁盘临时表进行排序操作，SQL_SMALL_RESULT 告诉优化器结果很小，放在内存中的索引历史表，避免排序操作。
    
  - SQL_BUFFER_RESULT
  
    告诉优化器将查询结果放入一个临时表，然后尽可能快的释放表锁。
    
  - SQL_CACHE 和 SQL_NO_CACHE
  
    告诉优化器是否将结果集混存在查询缓存中。
    
  - USE INDEX、IGNORE INDEX 和 FORCE INDEX
  
    告诉优化器使用或者不使用那些索引来查询记录, FORCE INDEX 和 USE INDEX 基本相同，除了 FORCE INDEX 会告诉优化器全表扫描的成本会远远高于索引扫描，哪怕该索引的用处不大。

- 优化关联查询

  - 确保 ON 或者 USING 子句中的列上有索引，只需要再关联顺序的第二个表上建立索引。
  
  - 确保任何的 group by 和 order by 中的表达式只涉及到一个表中的列，这样优化器才可以使用索引来优化这个过程。
  

- count
  
  统计行数或者某个列值的行数，统计列值要求非空(不为NULL)，指定了列或者列的表达式，则统计这个表达式有值的结果集，指定了*则统计行数，使用count(1)和count( * )一样结果，使用 * 并不会扩展所有的列，而是忽略所有的列而直接统计行数
  
  MYISAM 使用 count 必须没有where条件速度才会很快

- group by 和 distinct
  
  使用 `索引字段`
  
  当无法使用`索引字段`的时候,group by 会使用 `临时表(少量数据)`或者`文件排序(大量数据)`实现,可以使用 `hint(查询优化器提示)`,指定 `SQL_GIG_RESULT` 或者 `SQL_SMALL_RESULT`
  
  
- limit

  使用 `延时关联` 或者 `多列二次索引`
 
  - 延迟关联:通过使用覆盖索引查询返回需要的主键,再根据主键关联原表获得需要的数据。
  - 多列二次索引:通过需要查询的字段建立多个索引(不推荐)
  
