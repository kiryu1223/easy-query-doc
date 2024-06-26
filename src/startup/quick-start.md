---
title: Main函数快速开始🔥🔥🔥
---

## 简介
在使用前您需要知晓目前1.8.0+版本的`easy-query`提供了3中api机制分别是`lambda`、`property`、`entity`其中每个api都有自己的特点,其中`easyEntityQuery`是最新开发的api,使用起来非常顺畅流畅,非常推荐,3种模式可以在一个应用里面共存

如果您希望直接快速体验可以下载对应代码jdk17+springboot3.1.0

[demo地址](https://github.com/xuejmnet/eq-multi-module) https://github.com/xuejmnet/eq-multi-module

## EntityQuery
`EasyEntityQuery`接口为`EntityQuery`暴露给用户的`crud`api接口,我们的主要操作处理都是通过该接口实现的,要实现这个功能有以下两种方式

如果是多模块那么可以再每个需要生成`proxy`的`module`处的`pom.xm`l引入`sql-processor`包或者在项目`maven`插件处进行配置


具体的easy-query包版本可以在文档首页进行查看当前是  最新版本`easy-query` 如果无法看到具体版本可以去github或者gitee源码右侧有对应的release版本
<a target="_blank" href="https://central.sonatype.com/search?q=easy-query">
        <img src="https://img.shields.io/maven-central/v/com.easy-query/easy-query-all?label=Maven%20Central" alt="Maven" />
    </a>



# EntityProxy 推荐🔥🔥🔥
## 安装插件(可选)
可以提高用户体验
<img src="/plugin-search.png">

新建一个`java8`以上的任意项目我们创建maven的空项目即可然后引入对应的包,`sql-core`提供了`property`的api模式,`sql-api-proxy`则是真正的针对`property`的模式增加的强类型`entity`模式的包
## 依赖注入
```xml
    <dependencies>
        <!-- mysql方言 -->
        <dependency>
            <groupId>com.easy-query</groupId>
            <artifactId>sql-mysql</artifactId>
            <version>${easy-query.version}</version>
        </dependency>
        <!-- entity-query的api包 -->
        <dependency>
            <groupId>com.easy-query</groupId>
            <artifactId>sql-api-proxy</artifactId>
            <version>${easy-query.version}</version>
        </dependency>
        <!-- entity-query的apt包 如果你是多模块只需要在生成apt的对象模块处需要引入 -->
        <dependency>
            <groupId>com.easy-query</groupId>
            <artifactId>sql-processor</artifactId>
            <version>${easy-query.version}</version>
        </dependency>
        <!-- mysql驱动 -->
        <!-- 选择自己的合适版本 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.17</version>
        </dependency>
        <!-- 数据源 -->
        <!-- 选择自己的合适版本 -->
        <dependency>
            <groupId>com.zaxxer</groupId>
            <artifactId>HikariCP</artifactId>
            <version>3.3.1</version>
        </dependency>
        <!-- 选择自己的合适版本 -->
        <!-- <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.24</version>
        </dependency> -->
    </dependencies>
```


## 数据库表对象

::: code-tabs
@tab 数据库对象
```java
//import com.easy.query.core.annotation.Table;
//import com.easy.query.core.annotation.Column;
//@Data //如果您有lombok
@Table("t_topic")//注意必须使用easy-query的注解
@EntityProxy
public class Topic{

    @Column(primaryKey = true)//注意必须使用easy-query的注解
    private String id;
    private Integer stars;
    private String title;
    private String name;
    private LocalDateTime createTime;

    //get set方法...
}
```
@tab 数据库脚本
```sql
create table t_topic
(
    id varchar(32) not null comment '主键ID'primary key,
    stars int not null comment '点赞数',
    title varchar(50) null comment '标题',
    create_time datetime not null comment '创建时间'
)comment '主题表';
```
:::

## 生成apt文件

<img src="/startup1.png">

如果存在如下情况无法获取到`TopicProxy`对象那么就将目录标记为生成目录

<img src="/startup2.png">

::: warning 说明!!!
> 如果您还是不行那么建议您点击idea右侧的maven刷新按钮进行刷新即可
:::

<img src="/startup4.png">

::: tip 说明!!!
> 如果您第一步安装了插件那么在你鼠标移出当前entity的编辑区域那么就会自动生成`Proxy类`或者呼出`get set`的界面点击`CompileCurrentFile`
:::


## 添加数据库对象接口


::: warning 说明!!!
> 如果您有洁癖不想实现这个接口也是可以的,就是在使用的时候使用`easyProxyQuery`而不是`easyEntityQuery`
> 只是有些框架是一套试题的情况下那么不需要实现接口也可以用entityQuery的api仅此而已正常使用还是推荐大家实现`ProxyEntityAvailable`接口
> 不是很推荐使用起来会稍微麻烦一点[点击查看两者的区别](/easy-query-doc/startup/diff-proxy)
> 不是很推荐使用起来会稍微麻烦一点[点击查看两者的区别](/easy-query-doc/startup/diff-proxy)
> 不是很推荐使用起来会稍微麻烦一点[点击查看两者的区别](/easy-query-doc/startup/diff-proxy)
```java
//easyEntityQuery.queryable(SysUser.class)
//easyProxyQuery.queryable(SysUserProxy.createTable())
```
:::

实现接口即可


<img src="/startup3.png">

::: tip 说明!!!
> 如果您第一步安装了插件那么可以在呼出`get set`的目录点击`EasyQueryImplements`自动实现接口
:::

::: warning 说明!!!
> 2.0.15+版本框架不需要实现`proxyTableClass`方法，idea-plugin插件在0.0.57后也将不会生成该方法
> 2.0.15+版本框架不需要实现`proxyTableClass`方法，idea-plugin插件在0.0.57后也将不会生成该方法
> 2.0.15+版本框架不需要实现`proxyTableClass`方法，idea-plugin插件在0.0.57后也将不会生成该方法
> 如果您的项目是多模块那么只需要在需要使用@EntityProxy注解的模块下使用`sql-processor`即可
:::

::: warning 说明!!!
> 如果出现no primary key或者not found [id] mapping column name之类的错误请排查lombok是否生效,是否存在get set方法
:::


## 运行
::: danger 说明!!!
> 如果出现无法build或者启动那么请确认是否引入了`sql-processor`包
:::
```java

public class Main {
    public static void main(String[] args) {

        HikariDataSource dataSource = new HikariDataSource();
        dataSource.setJdbcUrl("jdbc:mysql://127.0.0.1:3306/easy-query-test?serverTimezone=GMT%2B8&characterEncoding=utf-8&useSSL=false&allowMultiQueries=true&rewriteBatchedStatements=true");
        dataSource.setUsername("root");
        dataSource.setPassword("root");
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setMaximumPoolSize(20);
        //采用控制台输出打印sql
        LogFactory.useStdOutLogging();
        //property的api
        EasyQueryClient easyQueryClient = EasyQueryBootstrapper.defaultBuilderConfiguration()
                .setDefaultDataSource(dataSource)
                .optionConfigure(op -> {
                    op.setPrintSql(true);
                    op.setKeepNativeStyle(true);
                })
                .useDatabaseConfigure(new MySQLDatabaseConfiguration())
                .build();
                
        EasyEntityQuery easyEntityQuery = new DefaultEasyEntityQuery(easyQueryClient);
        //不需要实现接口但是使用方式有点区别
        EasyProxyQuery easyProxyQuery = new DefaultEasyProxyQuery(easyQueryClient);

        //根据id查询第一条
        Topic topic1 = easyEntityQuery.queryable(Topic.class)
                .whereById("1").firstOrNull();

        //根据id查询并且断言仅一条
        Topic topic2 = easyEntityQuery.queryable(Topic.class)
                .whereById("1").singleOrNull();
        //根据id查询自定义条件返回第一条
        Topic topic3 = easyEntityQuery.queryable(Topic.class)
                .where(o -> {
                    o.id().eq("1");
                })
                .firstOrNull();

        //根据条件返回符合的集合默认ArrayList实现
        List<Topic> list = easyEntityQuery.queryable(Topic.class)
                .where(o -> {
                    o.id().eq("1");
                })
                .toList();
        //判断小明是否存在
       boolean exists= easyEntityQuery.queryable(Topic.class).where(o->o.name().like("小明")).any();
       //断言小明是否存在
       easyEntityQuery.queryable(Topic.class).where(o->o.name().like("小明")).required("未找到小明");

       System.out.println("Hello world!");
    }
}

//打印的sql
==> Preparing: SELECT `id`,`stars`,`title`,`create_time` FROM `t_topic` WHERE `id` = ? LIMIT 1
==> Parameters: 1(String)
<== Time Elapsed: 14(ms)
<== Total: 1
```



::: warning 报错!!!
如果遇到build后报错java:程序包xxxxxxxx.proxy不存在


- 查看是否引入sql-processor包
- 设置idea的注解处理器 Build,Execution,Deployment,Compiler,Annotation Processors 选择Enable annotation processing 并且选择Obtain processors from project classpath

- 如果您之前已经存在`annotationProcessorPaths`那么你可以在里面添加`eq`的`apt`处理，如果未使用过那么还是建议需要apt的模块单独引入`sql-processor`
以下配置那么在各个独立`module`处不需要在引入`sql-processor`
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.8.1</version>
    <configuration>
        <annotationProcessorPaths>
        <!-- 注意顺序 -->
            <path>
            <!-- lombok... -->
            </path>
            <path>
            <!-- mapstruct... -->
            </path>
            <path>
                <groupId>com.easy-query</groupId>
                <artifactId>sql-processor</artifactId>
                <version>${easy-query.version}</version>
            </path>
        </annotationProcessorPaths>
    </configuration>
</plugin>
```
:::



### 单个查询
```java

//根据id查询第一条
Topic topic1 = easyEntityQuery.queryable(Topic.class)
        .whereById("1").firstOrNull();
==> Preparing: SELECT `id`,`stars`,`title`,`create_time` FROM `t_topic` WHERE `id` = ? LIMIT 1
==> Parameters: 1(String)
<== Time Elapsed: 10(ms)
<== Total: 1

//根据id查询返回自定义列
Topic topic1 = easyEntityQuery.queryable(Topic.class)
        .whereById("1").select(t->t.FETCHER.id().stars().fetchProxy()).firstOrNull();
==> Preparing: SELECT `id`,`stars` FROM `t_topic` WHERE `id` = ? LIMIT 1
==> Parameters: 1(String)
<== Time Elapsed: 10(ms)
<== Total: 1


//根据id查询并且断言仅一条
Topic topic2 = easyEntityQuery.queryable(Topic.class)
        .whereById("1").singleOrNull();

==> Preparing: SELECT `id`,`stars`,`title`,`create_time` FROM `t_topic` WHERE `id` = ?
==> Parameters: 1(String)
<== Time Elapsed: 6(ms)
<== Total: 1


//根据id查询自定义条件返回第一条
Topic topic3 = easyEntityQuery.queryable(Topic.class)
        .where(o -> {
            o.id().eq("1");
        })
        .firstOrNull();

==> Preparing: SELECT `id`,`stars`,`title`,`create_time` FROM `t_topic` WHERE `id` = ? LIMIT 1
==> Parameters: 1(String)
<== Time Elapsed: 7(ms)
<== Total: 1


//根据id查询
Topic topic2 = easyEntityQuery.queryable(Topic.class)
        .findOrNull("1");

==> Preparing: SELECT `id`,`stars`,`title`,`create_time` FROM `t_topic` WHERE `id` = ?
==> Parameters: 1(String)
<== Time Elapsed: 6(ms)
<== Total: 1
```

### 返回列表
```java
List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .where(o -> {
            o.id().eq("1");
        })
        .toList();

==> Preparing: SELECT `id`,`stars`,`title`,`create_time` FROM `t_topic` WHERE `id` = ?
==> Parameters: 1(String)
<== Time Elapsed: 10(ms)
<== Total: 1
```

### count查询
```java

long count = easyEntityQuery.queryable(Topic.class)
        .where(o -> {
            o.title().like("11");
            o.createTime().le(LocalDateTime.now());
        }).count();

int intCount = easyEntityQuery.queryable(Topic.class)
        .where(o -> {
            o.title().like("11");
            o.createTime().le(LocalDateTime.now());
        }).intCount();

==> Preparing: SELECT COUNT(*) FROM `t_topic` WHERE `title` LIKE ? AND `create_time` <= ?
==> Parameters: %11%(String),2023-12-16T14:17:04.065(LocalDateTime)
<== Time Elapsed: 2(ms)
<== Total: 1
```

### 返回自定义列
```java

@Data
@EntityProxy
public class TopicVO{
    private String id;
    private String title;
}

List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .where(o->{
            o.title().like("123");
            o.createTime().ge(LocalDateTime.of(2022,2,1,3,4));
        })
        .orderBy(o -> {
            o.id().asc();
            o.createTime().desc();
        })
        .select(o->new TopicVOProxy()
                .id().set(o.id())
                .title().set(o.title())
        )
        .toList();


//上下两种映射都行

List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .where(o->{
            o.title().like("123");
            o.createTime().ge(LocalDateTime.of(2022,2,1,3,4));
        })
        .orderBy(o -> {
            o.id().asc();
            o.createTime().desc();
        })
        .select(TopicVO.class) //自动映射VO有的属性
        .toList();


==> Preparing: SELECT t.`id` as `id`,t.`title` as `title` FROM `t_topic` t WHERE t.`title` LIKE ? AND t.`create_time` >= ? ORDER BY t.`id` ASC,t.`create_time` DESC
==> Parameters: %123%(String),2022-02-01T03:04(LocalDateTime)
<== Time Elapsed: 4(ms)
<== Total: 98


List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .where(o -> {
            o.title().like("123");
            o.createTime().ge(LocalDateTime.of(2022, 2, 1, 3, 4));
        })
        .orderBy(o -> {
            o.id().asc();
            o.createTime().desc();
        })
        .select(o -> new TopicProxy()
                .selectAll(o)
                .selectIgnores(o.id())
        )
        .toList();

//上下两种映射都行

List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .where(o->{
            o.title().like("123");
            o.createTime().ge(LocalDateTime.of(2022,2,1,3,4));
        })
        .orderBy(o -> {
            o.id().asc();
            o.createTime().desc();
        })
        .select(Topic.class,o->Select.of(
                o.FETCHER.allFieldsExclude(o.id())
        ))
        .toList();

==> Preparing: SELECT t.`stars`,t.`title`,t.`create_time` FROM `t_topic` t WHERE t.`title` LIKE ? AND t.`create_time` >= ? ORDER BY t.`id` ASC,t.`create_time` DESC
==> Parameters: %123%(String),2022-02-01T03:04(LocalDateTime)
<== Time Elapsed: 3(ms)
<== Total: 98
```

### 分组
```java
 List<Topic> list = easyEntityQuery.queryable(Topic.class)
                .where(o -> {
                    o.title().like("123");
                    o.createTime().ge(LocalDateTime.of(2022,2,1,3,4));
                })
                //会生成{key1:x,key2:x.... group:{t1:xx,t2:xx}}其中key1...keyn表示key默认支持10个 t1...tn表示前面的表
                //无论join了多少张表group后全部只有一个入参参数其余参数在group属性里面
                .groupBy(o -> GroupKeys.TABLE1.of(o.id()))
                .select(o -> new TopicProxy()
                        .id().set(o.key1())//key1就是id
                        .stars().set(o.intCount())//COUNT(*)返回int 默认返回long类型
                )
                .toList();


 List<Topic> list = easyEntityQuery.queryable(Topic.class)
                .where(o->{
                    o.title().like("123");
                    o.createTime().ge(LocalDateTime.of(2022,2,1,3,4));
                })
                //会生成{key1:x,key2:x.... group:{t1:xx,t2:xx}}其中key1...keyn表示key默认支持10个 t1...tn表示前面的表
                //无论join了多少张表group后全部只有一个入参参数其余参数在group属性里面
                .groupBy(o-> GroupKeys.TABLE1.of(o.id()))
                .select(Topic.class,o->{
                    TopicProxy r = new TopicProxy();
                    r.id().set(o.key1());//key1就是id
                    r.stars().set(o.intCount());//COUNT(*)返回int 默认返回long类型
                    return r;
                })
                .toList();

//上下两种映射都行

List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .where(o->{
            o.title().like("123");
            o.createTime().ge(LocalDateTime.of(2022,2,1,3,4));
        })
        //会生成{key1:x,key2:x.... group:{t1:xx,t2:xx}}其中key1...keyn表示key默认支持10个 t1...tn表示前面的表
        //无论join了多少张表group后全部只有一个入参参数其余参数在group属性里面
        .groupBy(o-> GroupKeys.TABLE1.of(o.id()))
        .select(Topic.class,o->Select.of(
                o.key1(),
                o.intCount().as(Topic::getStars)
        ))
        .toList();

==> Preparing: SELECT t.`id` AS `id`,COUNT(*) AS `stars` FROM `t_topic` t WHERE t.`title` LIKE ? AND t.`create_time` >= ? GROUP BY t.`id`
==> Parameters: %123%(String),2022-02-01T03:04(LocalDateTime)


//草稿模式无需定义返回结果,返回草稿支持1-10 Draft1-Draft10
List<Draft3<String, Integer, Integer>> list = easyEntityQuery.queryable(Topic.class)
        .where(o -> {
            o.title().like("123");
            o.createTime().ge(LocalDateTime.of(2022, 2, 1, 3, 4));
        })
        .groupBy(o -> GroupKeys.TABLE1.of(o.id()))
        .select(o -> new TopicProxy()
                .id().set(o.key1())//key1就是id
                .stars().set(o.intCount())//COUNT(*)返回int 默认返回long类型
        )
        .select(o -> Select.DRAFT.of(
                o.id().nullOrDefault("123"),//如果为空就赋值123
                o.stars(),
                o.stars().abs()//取绝对值
        ))
        .toList();


==> Preparing: SELECT IFNULL(t1.`id`,?) AS `value1`,t1.`stars` AS `value2`,ABS(t1.`stars`) AS `value3` FROM (SELECT t.`id` AS `id`,COUNT(*) AS `stars` FROM `t_topic` t WHERE t.`title` LIKE ? AND t.`create_time` >= ? GROUP BY t.`id`) t1
==> Parameters: 123(String),%123%(String),2022-02-01T03:04(LocalDateTime)
```

### 分页
```java

EasyPageResult<Topic> pageResult = easyEntityQuery.queryable(Topic.class)
        .where(o -> {
            o.title().like("123");
            o.createTime().ge(LocalDateTime.of(2022, 2, 1, 3, 4));
        })
        .orderBy(o -> {
            o.id().asc();
            o.createTime().desc();
        })
        .select(o -> new TopicProxy().selectExpression(o.id(),o.title()))
        //.select(o->new TopicProxy())//全属性映射等于selectAll(o)
        .toPageResult(1, 20);


==> Preparing: SELECT COUNT(*) FROM `t_topic` t WHERE t.`title` LIKE ? AND t.`create_time` >= ?
==> Parameters: %123%(String),2022-02-01T03:04(LocalDateTime)
<== Time Elapsed: 3(ms)
<== Total: 1
==> Preparing: SELECT t.`id`,t.`title` FROM `t_topic` t WHERE t.`title` LIKE ? AND t.`create_time` >= ? ORDER BY t.`id` ASC,t.`create_time` DESC LIMIT 20
==> Parameters: %123%(String),2022-02-01T03:04(LocalDateTime)
<== Time Elapsed: 3(ms)
<== Total: 20
```

### join多表查询

```java

@Data
@EntityProxy
public class TopicVO{
    private String id;
    private String title;
    private Integer stars;
}

List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .leftJoin(Topic.class, (t, t1) -> {//第一个参数t表示第一个表,第二个参数t1表示第二个表
            t.id().eq(t1.id());// ON t.`id` = t1.`id`
        })
        .where((t, t1) -> {
            t.title().like("11");
            t1.createTime().le(LocalDateTime.of(2021, 1, 1, 1, 1));
        })
        .select((t, t1) -> new TopicVOProxy()
                .id().set(t.id())
                .stars().set(t.stars())
                .title().set(t1.id())
        ).toList();


==> Preparing: SELECT t.`id` AS `id`,t.`stars` AS `stars`,t1.`id` AS `title` FROM `t_topic` t LEFT JOIN `t_topic` t1 ON t.`id` = t1.`id` WHERE t.`title` LIKE ? AND t1.`create_time` <= ?
==> Parameters: %11%(String),2021-01-01T01:01(LocalDateTime)
<== Time Elapsed: 12(ms)
<== Total: 0


List<TopicTypeVO> vo = easyEntityQuery.queryable(BlogEntity.class)
        .leftJoin(SysUser.class, (b, s2) -> b.id().eq(s2.id()))
        .select(TopicTypeVO.class, (b1, s2) -> Select.of(
                b1.FETCHER.id().content().createTime().as("createTime"),
                s2.FETCHER.address().idCard()
        )).toList();

==> Preparing: SELECT t.`id`,t.`content`,t.`create_time` AS `create_time`,t1.`address`,t1.`id_card` FROM `t_blog` t LEFT JOIN `easy-query-test`.`t_sys_user` t1 ON t.`id` = t1.`id` WHERE t.`deleted` = ?
==> Parameters: false(Boolean)
```

### 排序

```java

List<Topic> list = easyEntityQuery.queryable(Topic.class)
        .leftJoin(Topic.class, (t, t1) -> {
            t.id().eq(t1.id());
        })
        .orderBy((t, t1) -> {
            t.id().asc();
            t1.createTime().desc();
        })
        //查询t表的所有除了id和title,并且返回t1的title取别名为content
        .select((t,t1) -> new TopicProxy()
                .selectAll(t)
                .selectIgnores(t.id(),t.title())
                .id().set(t1.title())
        )
        .toList();

==> Preparing: SELECT t.`stars`,t.`create_time`,t1.`title` AS `id` FROM `t_topic` t LEFT JOIN `t_topic` t1 ON t.`id` = t1.`id` ORDER BY t.`id` ASC,t1.`create_time` DESC
<== Time Elapsed: 14(ms)
<== Total: 101

//使用草稿无需定义返回结果
List<Draft3<Integer, LocalDateTime, String>> list = easyEntityQuery.queryable(Topic.class)
                .leftJoin(Topic.class, (t, t1) -> {
                    t.id().eq(t1.id());
                })
                .orderBy((t, t1) -> {
                    t.id().asc();
                    t1.createTime().desc();
                })
                .select((t, t1) -> Select.DRAFT.of(
                        t.stars(),
                        t.createTime(),
                        t1.title()
                ))
                .toList();

==> Preparing: SELECT t.`stars` AS `value1`,t.`create_time` AS `value2`,t1.`title` AS `value3` FROM `t_topic` t LEFT JOIN `t_topic` t1 ON t.`id` = t1.`id` ORDER BY t.`id` ASC,t1.`create_time` DESC
```


## 额外配置
如果您之前已经存在`annotationProcessorPaths`那么你可以在里面添加`eq`的`apt`处理，如果未使用过那么还是建议需要apt的模块单独引入`sql-processor`
以下配置那么在各个独立`module`处不需要在引入`sql-processor`
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.8.1</version>
    <configuration>
        <annotationProcessorPaths>
        <!-- 注意顺序 -->
            <path>
            <!-- lombok... -->
            </path>
            <path>
            <!-- mapstruct... -->
            </path>
            <path>
                <groupId>com.easy-query</groupId>
                <artifactId>sql-processor</artifactId>
                <version>${easy-query.version}</version>
            </path>
        </annotationProcessorPaths>
    </configuration>
</plugin>

```