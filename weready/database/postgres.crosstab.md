---
title: 'postgres 数据库的 “数据透视表”'
author: 'Chris'
contact: '18621569380'
date: '2020-9-19'
keywords: 'postgres, crosstab, pivot, 数据统计'
brief: '利用 crosstab 函数，针对 postgres 数据表 或 查询结果，做 “列” 转 “行” 的 “转置” 操作'
---

# 背景 & 需求

几乎所有系统的`数据表`，可能都会有一些`状态字段`，这些字段的取值是有限个`状态`。无论是运营的需求层面，还是程序运行的业务逻辑判断层面，往往需要对这些`数据表`中的记录，根据不同的状态进行汇总统计，获取不同状态下，所有记录的统计结果。

例如，假设一个 *任务* `数据表`(`t_tasks`)：

|id|project_code|state|
|:-:|:-:|:-:|
|1001|PRJ_1|WORKING|
|1002|PRJ_1|WORKING|
|1003|PRJ_1|DONE|
|1004|PRJ_2|PENDING|
|1005|PRJ_2|WORKING|
|1006|PRJ_2|WORKING|
|1007|PRJ_2|DONE|
|1008|PRJ_3|PENDING|
|1009|PRJ_3|WORKING|

期望得到这样的统计结果：

|project_code|pending|working|done|
|:-:|:-:|:-:|:-:|
|PRJ_1|   | 2 | 1 |
|PRJ_2| 1 | 2 | 1 |
|PRJ_3| 1 | 1 |   |

# 解决方案

```
SELECT *
FROM crosstab(
  'SELECT project_code::text, state, count(id) FROM t_tasks GROUP BY grouping sets((project_code, state)) ORDER BY 1,2',
  $$values('PENDING'::text),('WORKING'::text),('DONE'::text)$$
)
AS (project text, PENDING int, WORKING int, DONE int)
```

> `crosstab` 是 `postgres` 的扩展功能，使用之前，需要安装相关扩展

# 说明

- `$$` 相当于单引号（`crosstab` 的参数是一个 SQL 语句字符串，字符串是由单引号括起来的，因此，在单引号里面，不能再使用单引号，这时候，可以使用 `$$` 代替单引号）
- `crosstab` 有两个`入参`：`数据集`，`状态集`
- `数据集`有三列：`行标识`, `状态`, `取值`
- `状态集`：所有状态的列表

### 中间结果

`SELECT project_code::text, state, count(id) FROM t_tasks GROUP BY grouping sets((project_code, state)) ORDER BY 1,2`

|project_code|state|count|
|:-:|:-:|:-:|
|PRJ_1|WORKING|2|
|PRJ_1|DONE|1|
|PRJ_2|PENDING|1|
|PRJ_2|WORKING|2|
|PRJ_2|DONE|1|
|PRJ_3|PENDING|1|
|PRJ_3|WORKING|1|

# 关键点

- 构造一个 SQL 语句，能够取得中间结果；这个 SQL 语句，就是 `crosstab` 的第一个参数：`数据集`
- 指明一个`状态集`，作为 `crosstab` 的第二个参数

# 补充

## 状态集 的构造方式

### 固定的`状态集`

```
$$values('PENDING'::text),('WORKING'::text),('DONE'::text)$$
```

### 动态的`状态集`，动态构造

```
const stateArray = ['PENDING', 'WORKING', 'DONE']
const cstr = ....
const sql = `
  SELECT 
    distinct qa.serial_code AS id,
    fb.form_serial_code, fb.form_title, form_index, fb.form_id, 
    fb.notice_template_id, fb.notice_template_code,
    fb.notice_serial_code, fb.notice_title, fb.notice_id, 
    fb.employer_path, fb.employer_id, 
    fb.source_path, fb.source_id, 
    fb.created_by,
    fb.created_when,
    fb.updated_by,
    fb.updated_when,
    qa.* 
  FROM crosstab(
    'SELECT serial_code, question_key, answer_value FROM dbt_biz_logs WHERE ${cstr} ORDER BY 1, 2',
    'SELECT * FROM unnest(array[${stateArray}]) as exp'
  )
  AS qa(serial_code text, ${qtuple})
  LEFT JOIN dbt_biz_logs fb ON fb.serial_code=qa.serial_code AND fb.category='FORM_FEEDBACK_QA'
`
````

### 来自数据库的枚举类型

```
'SELECT e.enumlabel FROM pg_type t, pg_enum e WHERE t.oid=e.enumtypid AND t.typname=''dbe_workflow_task_result'' ORDER BY 1'
```
