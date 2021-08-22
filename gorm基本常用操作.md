# gorm 常用基本操作

## 数据库连接
### DSN

### 如何配置隐式密码

### hardcode 密码的破解与保护


[数据库连接池](./gorm中的数据库连接池)

## 断开连接
+ 主动断开连接  
    何时
+ 释放连接  
    释放连接操作


### 因故障断开连接
+ 重试机制  

+ 报错与处理


## Create
### 新建表
例如根据struct User来创建一张表
```
    type User struct{
        gorm.Model
        Name     string
	    Gender   string
	    Age      int
	    Email    string
	    location string
    }
```
+ 判断表是否已经存在
    通过DbConn.HasTable(&User{})方法可以判断数据库中是否已经存在了该结构体所对应的表，如果存在，返回true，否则返回false
  

+ 根据model_name创建表  
    gorm会默认按照

+ 如何制定表的名称，不采用自动生成的表名称  
    在定义struct的时候实现TableName方法
    ```
    func (User) TableName() string{
        return "user_list"
    }
    ```
    此时就会使用user_list作为表名，而不是使用默认的替代

### 新建一条数据
+ 新建数据的语句  
```
    DbConn.Create(&User{})
```
使用Create方法在表中新建数据。
对于表中的ID字段，默认是主键，会自增，同时作为主键索引存在
如果User没有采用默认表名，也没有指定表名，就会报出table doesn't exist错误
如果没有定义TableName方法，也可以使用gorm提供的Table链式操作方法指定表名
```
    DbConn.Table("table_name").Create(&User{})
```
当多张表具有相同的数据组成时，可以不重复定义多个对应的数据结构，用这个方式实现复用


[gorm怎么知道该去哪张表中增/删/改/查数据？](./gorm如何知道寻找哪张表)  

[mysql和golang的数据结构映射](./mysql和golang的数据结构映射)  

[golang和mysql中的默认值与空值](./golang和mysql中的默认值与空值)


CreateTable 和 AutoMigrate的对比
CreateTable 设定建表参数

### 新建多条数据
+ 如何实现批量新增数据（是否支持以切片或数组的形式create）



### 新建column
（处理方式，已有model改造，model改造不及时可能出现的情况等）

## Research
### find方法


### first 方法
+ 如果没有找到？

### 排序与排序的性能问题

### limit的使用，分页的性能问题

### 索引的使用和读入内存处理性能对比

### join

## Update
### gorm如何知道该update哪条数据？

### 如果定位不到具体的某条数据，默认的处理方式是什么？

### 防止误批量操作的良好习惯

### Update方法和Save方法的比较




## Delete




