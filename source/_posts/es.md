---
title: ES
excerpt: ES的使用，介绍ES的基本概念，安装，搭建，使用，以及一些实践
date: 2021-11-22 11:15:25
tags: 
  - DB
  - ES
categories: [DB,ES]
---

## 安装/部署

##  文档
1. 文档三要素 index，type(虽然type不一样但文档尽量相似)，id(可以自定义或者由es定义)

##  查询
### 基本概念
1. 映射：描述数据在每个字段内如何存储
2. 分析：全文如何处理使之可以被搜索
3. 领域特定查询语句：

*  空搜索    _search
*  多索引  /index1(\*),index2(\*)/type1,type2/_search
*  分页 _search?size=每页数量&from=跳过的位置
* _all 搜索  将所有字段拼到一起成为一个字段（string）

### 分词器
1. _analyze

###  查询语句
1. 基本语法

```
{
	"query":{
		"match":{
			"":""
		}
	}
}
```

2. 全文搜索 match 使用分词器
3. 匹配所有文档 match_all 
4. multi_match 多个字段执行相同的match查询
5.  range 指定区间的数字或者时间 gt，gte，lt，lte
6.  term 精确匹配，数字，时间，boolean或者not_analyzed（不使用分词器）
7. terms 指定多字段匹配
8.  exists 字段中有值
9. missing 字段中无值
10. 短语搜索 match_phrase 匹配短语
11. 高亮搜索

```
{
	"query":{}
	"highlight":{
		"fields":{}
	}
}
```

#### 查询类型
1. 叶子语句：被用于将查询字符串和一个字段对比
2.  复合语句：合并其他查询 

#### 组合查询 bool constant_score
##### 方式
* bool
* constant_score 将不变的常量评分用于所有匹配的文档

##### 查询类型
1. must 必须匹配
2. must_not 必须不匹配
3. should 如果满足增加score
4. filter 必须匹配

### 验证查询语句是否合法
1. 验证查询 _avlidate
2. 理解错误 _explain

## 排序
### 基本语法

1. 单字段排序
```
"sort":{"":{"order":"desc"}}
```

2. 多级排序
```
"sort":[
	{"":{}},
	{"":{}}
]
```

3. 多值排序（字段中含有多个数值），多值变为单值
```
"sort":{
	"":{
		"order":"asc",
		"mode":"min/max/avg/sum"
	}
}
```

## 聚合

### 基本概念
1. 桶(bucks) 满足特定条件的文档集合
2. 指标(metrics) 对桶内的文档进行统计的计算

1. 基本语法

```
{
	"agg":{
		"all_interests":{
			"terms":{
				"field":""
			}
		}
	}
}
```





## 文档的基本操作
#### 创建
1.  put /index/type/

#### 更新
1. 全部更新 post /index/
2. 版本控制：通过版本号，乐观锁的方式，当前版本号与es中版本号一致，或者大于可以更新。
3. 部分更新
4. 使用脚本更新

#### 取回
1. 取回单个 get /index/type/id
2. 取回多个 /_mget

#### 删除
1. delete 

#### bulk
1. /_bulk
```
post /_bulk
{
 {"delete":{}}
 {"create":{}}
}
```
