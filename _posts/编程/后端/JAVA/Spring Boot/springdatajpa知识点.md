## 基本用法

### 1.导入maven依赖

```java
<dependency>
	<groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 2.创建一个接口继承下面的任何一个接口都可以(注意下面都是接口)

[参考网址]: https://www.cnblogs.com/xiluonanfeng/p/9640490.html

#### Repository

```js
概述：仅仅是一个标识，表明任何继承它的均为仓库接口类，方便Spring自动扫描识别 。这个接口是最基础的接口，只是一个标志性的接口，没有定义任何的方法。
它是最顶层的接口，是一个空接口，目的是为了统一所有的Repository的类型，且能让组件扫描的时候自动识别。
好处：例如，我们有一部分方法是不想对外提供的，比如我们只想提供增加和修改方法，不提供删除方法，那么下面介绍的几个接口都是做不到的，这个时候，我们就可以继承这个接口，然后将CrudRepository接口里面相应的方法拷贝到Repository接口就可以了。
```

#### CrudRepository

```js
提供一下方法:
保存
    <S extends T> S save(S entity);
批量保存
    <S extends T> Iterable<S> save(Iterable<S> entities);
根据id查询一个对象
    T findOne(ID id)
判断对象是否存在
    boolean exists(ID id)
查询所有的对象
    Iterable<T> findAll()
根据id列表查询所有的对象
    Iterable<T> findAll(Iterable<ID> ids)
计算对象的总个数
    long count()
根据id删除
    void delete(ID id)
删除对象
    void delete(T entity);
批量删除
    void delete(Iterable<? extends T> entities);
删除所有
    void deleteAll()
```

#### PagingAndSortingRepository(常用)

```js
CrudRepository的子接口，添加一组分页排序相关的方法 
主要方法:
不带分页的排序
    Iterable<T> findAll(Sort sort)
带分页的排序
    Page<T> findAll(Pageable pageable)
```

#### JpaRepository

```js
PagingAndSortingRepository的子接口，增加一组JPA规范相关的方法 
主要方法:
查询所有对象，不排序
    List<T> findAll()
查询所有对象，并排序
    List<T> findAll(Sort sort)
批量保存
    <S extends T> List<S> save(Iterable<S> entities);
强制缓存与数据库同步
    void flush()
保存并强制同步
    T saveAndFlush(T entity)
批量删除
    void deleteInBatch(Iterable<T> entities)
删除所有
    void deleteAllInBatch();
```

#### JpaSpecificationExecutor

```js
概述：这个比较特殊，不属于Repository体系，它实现一组JPA Criteria查询相关的方法，主要是用来做复杂的查询的接口（辅助接口）。

注意事项：这个接口很特殊，不属于Repository体系，而Spring data JPA不会自动扫描识别，所以会报找不到对应的Bean，我们只需要继承任意一个继承了Repository的子接口或直接继承Repository接口，Spring data JPA就会自动扫描识别，进行统一的管理。
```

### 自定义方法

前提 ：实现上面的任何一个接口

#### @Query创建查询

```java
1.命名参数
@Query("select u from User u where u.name = :name")
User findUserByName(@Param("name") String name);
2.索引参数(推荐)
@Query("select u from User u where u.email = ?1")// 1表示第一个参数
User findUserByEmail(String email);
```

#### 修改查询(加注解@Modifying)

```java
@Modifying
@Query(value="update UserModel o set o.name=:newName where o.name like %:nn")
public int findByUuidOrAge(@Param("nn") String name,@Param("newName") String newName);
```

## 知识点

### mybatis和jpa的区别

```js
优势对比
1.DAO层开发角度来看，JPA更为简单高效，对于简单的操作甚至连sql都不需要编写，直接调用就能完成数据库的操作。
2.JPA的数据库移植性更好，因为其采用JPQL方式，和原生sql根本就没有耦合度。但一般情况下公司选定数据库后再变更的可能性微乎其微，所以这个优点可以忽略。
3.MyBatis更利于编写复杂的sql，擅长多表关联查询、聚合函数等复杂操作。JPA在这方面支持比较弱，我个人感觉JPA能让简单地操作更加简单，但是让复杂的操作也会更麻烦；但话说回来现在越来越微服务化，每个服务的业务比较单一，所以这个对于JPA来说也不是问题。
4.MyBatis上手容易，尤其是有sql经验的，学习成本会比学习JPA更低些。
```

个人更偏向于mp

### JPA 实体类相关注解有哪些？

```js
@Entity：表明当前类是一个实体类。
@Table ：关联实体类和数据库表。
@Column ：关联实体类属性和数据库表中字段。
@Id ：声明当前属性为数据库表主键对应的属性。
@GeneratedValue： 配置主键生成策略。
@OneToMany ：配置一对多关系，mappedBy 属性值为主表实体类在从表实体类中对应的属性名。
@ManyToOne ：配置多对一关系，targetEntity 属性值为主表对应实体类的字节码。
@JoinColumn：配置外键关系，name 属性值为外键名称，referencedColumnName 属性值为主表主键名称。
```
