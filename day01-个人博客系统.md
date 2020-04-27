# 个人博客系统

## 技术结构：

| 技术栈       | 版本        |
| ------------ | ----------- |
| springboot   | 2.2.6       |
| mybatis plus | 3.1.1       |
| redis        | windows版本 |
| shiro        | 1.3+        |
| lucene       | 7.4+        |
| git          | /           |

## **数据库设计**

1.t_blogger:博客表

2.t_blogtype:博客分类表

3.t_blog:博客

4.t_comment:博客评论表

## **搭建项目环境**

使用idea开发工具创建springboot项目

### **项目规范**

项目名称：blog

**包结构**

​	*com.blog.entity：实体类*

​	*com.blog.dao：数据访问层*

​	*com.blog.service：业务层*

​	*com.blog.service.impl：业务层实现类*

​	*com.blog.controller.admin：后台控制器*

​	*com.blog.controller.foreign：前台控制器*

​	*com.blog.config：配置类*

### **pom.xml导入依赖包**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.6.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com</groupId>
    <artifactId>blog</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>war</packaging>
    <name>blog</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <!-- MySQL驱动包 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <!-- 导入thymeleaf依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <!-- shiro与spring整合依赖 -->
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-spring</artifactId>
            <version>1.4.0</version>
        </dependency>
        <!-- MyBatisPlus驱动包 -->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.1.1</version>
        </dependency>


        <!-- 以下是代码生成器的jar依赖 -->
        <!-- 代码生成器核心jar依赖 -->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-generator</artifactId>
            <version>3.1.1</version>
        </dependency>

        <!-- 使用默认的velocity模板 -->
        <dependency>
            <groupId>org.apache.velocity</groupId>
            <artifactId>velocity-engine-core</artifactId>
            <version>2.0</version>
        </dependency>

        <!-- sfl4j -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
        </dependency>

        <!-- fastjson -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.47</version>
        </dependency>

        <!-- 热部署 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
        </dependency>

        <!-- springboot集成redis -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-annotations</artifactId>
        </dependency>

        <!-- jasper -->
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <scope>provided</scope>
        </dependency>
        <!-- 添加百度编辑器ueditor支持 -->
        <dependency>
            <groupId>com.gitee.qdbp.thirdparty</groupId>
            <artifactId>ueditor</artifactId>
            <version>1.4.3.3</version>
        </dependency>

        <!-- 添加lucene相关依赖 -->
        <!-- lucene -->
        <dependency>
            <groupId>org.apache.lucene</groupId>
            <artifactId>lucene-core</artifactId>
            <version>7.4.0</version>
        </dependency>
        <!-- queryparser -->
        <dependency>
            <groupId>org.apache.lucene</groupId>
            <artifactId>lucene-queryparser</artifactId>
            <version>7.4.0</version>
        </dependency>
        <!-- lucene-highlighter 高亮显示 -->
        <dependency>
            <groupId>org.apache.lucene</groupId>
            <artifactId>lucene-highlighter</artifactId>
            <version>7.4.0</version>
        </dependency>
        <!--        热部署-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <version>2.2.2.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```

### **application.yml**

```properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://47.106.191.144:3306/db_blog?useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=123456
mybatis-plus.type-aliases-package=com.blog.entiy
logging.level.com.blog.dao=debug
spring.thymeleaf.cache=false

mybatis-plus.mapper-locations=classpath:com/blog/dao/*.xml
```

使用mybatis generator生成相关包和Java文件

```java
package com.blog;

import org.junit.Test;

import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.annotation.IdType;
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.config.DataSourceConfig;
import com.baomidou.mybatisplus.generator.config.GlobalConfig;
import com.baomidou.mybatisplus.generator.config.PackageConfig;
import com.baomidou.mybatisplus.generator.config.StrategyConfig;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;

public class TestMP {

    private static String author ="YangDongWen";//作者名称
    private static String outputDir ="C:\\";//生成的位置
    private static String driver ="com.mysql.cj.jdbc.Driver";//驱动，注意版本
    //连接路径,注意修改数据库名称
    private static String url ="jdbc:mysql://47.106.191.144:3306/db_blog?useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC";
    private static String username ="root";//数据库用户名
    private static String password ="123456";//数据库密码
    private static String tablePrefix ="t_";//数据库表的前缀，如tbl_user
    private static String [] tables = {"t_blog","t_blogger","t_blogtype","t_comment"};	//生成的表
    private static String parentPackage = "com.blog";//顶级包结构
    private static String dao = "dao";//数据访问层包名称
    private static String service = "service";//业务逻辑层包名称
    private static String entity = "entity";//实体层包名称
    private static String controller = "controller";//控制器层包名称
    private static String mapperxml = "dao";//mapper映射文件包名称


    /**
     * 代码生成    示例代码
     */
    @Test
    public void  testGenerator() {
        //1. 全局配置
        GlobalConfig config = new GlobalConfig();
        config.setAuthor(author) // 作者
                .setOutputDir(outputDir) // 生成路径
                .setFileOverride(true)  // 文件覆盖
                .setIdType(IdType.AUTO) // 主键策略
                .setServiceName("%sService")  // 设置生成的service接口的名字的首字母是否为I，加%s则不生成I
                .setBaseResultMap(true)	//映射文件中是否生成ResultMap配置
                .setBaseColumnList(true);	//生成通用sql字段

        //2. 数据源配置
        DataSourceConfig  dsConfig  = new DataSourceConfig();
        dsConfig.setDbType(DbType.MYSQL)  // 设置数据库类型
                .setDriverName(driver)	//设置驱动
                .setUrl(url)			//设置连接路径
                .setUsername(username)	//设置用户名
                .setPassword(password);	//设置密码

        //3. 策略配置
        StrategyConfig stConfig = new StrategyConfig();
        stConfig.setCapitalMode(true) //全局大写命名
                .setNaming(NamingStrategy.underline_to_camel) // 数据库表映射到实体的命名策略
                .setTablePrefix(tablePrefix) //表前缀
                .setInclude(tables);  // 生成的表

        //4. 包名策略配置
        PackageConfig pkConfig = new PackageConfig();
        pkConfig.setParent(parentPackage)//顶级包结构
                .setMapper(dao)	//数据访问层
                .setService(service)	//业务逻辑层
                .setController(controller)	//控制器
                .setEntity(entity)	//实体类
                .setXml(mapperxml);	//mapper映射文件

        //5. 整合配置
        AutoGenerator  ag = new AutoGenerator();
        ag.setGlobalConfig(config)
                .setDataSource(dsConfig)
                .setStrategy(stConfig)
                .setPackageInfo(pkConfig);
        //6. 执行
        ag.execute();
    }

}

```

### 生成类和接口

**如图，会生成如下类和接口**

<img src="E:\笔记图片\image-20200422085837014.png" alt="image-20200422085837014" style="zoom: 80%;" />

### **设置视图配置类，设置首页**

```java
@Configuration
public class MyMvcConfiguration implements WebMvcConfigurer {
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        // 设置前台首页路径
        registry.addViewController("/").setViewName("/index");
        registry.addViewController("/index").setViewName("/index");
        registry.addViewController("/index.html").setViewName("/index");
    }
}
```

### 抽取页面公共部分

![image-20200422111535729](E:\笔记图片\image-20200422111535729.png)

## 博客首页-按日志类别查询

### xml下写Sql语句

```xml
<!--    查询每个博客分类下的博客数量-->
    <select id="getBlogTypeNameAndBlogCount" resultType="com.blog.entity.Blogtype">
        select typeName, count(tb.typeId) blognum from t_blogtype left join t_blog tb on t_blogtype.id = tb.typeId group by typeName
    </select>
```

### 修改BlogType实体类

```java
//    每个博客分类下的博客数量（数据库中不存在该列名）
// 该属性名应该与mapper文件中的别名一致
	@TableField(exist = false)
    private Integer blognum;

    public Integer getBlognum() {
        return blognum;
    }

    public void setBlognum(Integer blognum) {
        this.blognum = blognum;
    }
```

### pom.xml

```xml
<!-- springboot集成redis -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-annotations</artifactId>
        </dependency>
```

### RedisConfig配置类(直接Copy)

```java
@Configuration
public class RedisConfig {

    @Bean
    public RedisTemplate<Object,Object> redisTemplate(RedisConnectionFactory redisConnectionFactory){
        RedisTemplate<Object,Object> redisTemplate = new RedisTemplate<Object,Object>();
        // 设置redis连接
        redisTemplate.setConnectionFactory(redisConnectionFactory);
        // 使用Jackson2JsonRedisSerialize 替换默认序列化
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
        ObjectMapper objectMapper = new ObjectMapper();
        objectMapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        objectMapper.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
        jackson2JsonRedisSerializer.setObjectMapper(objectMapper);

        // 设置value的序列化规则和 key的序列化规则
        redisTemplate.setHashValueSerializer(jackson2JsonRedisSerializer);
        redisTemplate.setValueSerializer(jackson2JsonRedisSerializer);
        // 将redisTemplate的序列化方式更改为StringRedisSerializer
        redisTemplate.setHashKeySerializer(new StringRedisSerializer());
        redisTemplate.setKeySerializer(new StringRedisSerializer());
        redisTemplate.afterPropertiesSet();
        return redisTemplate;
    }
}
```

### BlogTypeServer接口以及实现类

```java
public interface BlogtypeService extends IService<Blogtype> {

    /**
    *  查询每个博客分类下的博客名称及博客数量
    */
    String getBlogTypeNameAndBlogCount() throws Exception;
}
@Service
public class BlogtypeServiceImpl extends ServiceImpl<BlogtypeMapper, Blogtype> implements BlogtypeService {

    @Resource
    private BlogtypeMapper blogtypeMapper;

    // springboot操作redis的对象
    private RedisTemplate<String, String> redisTemplate;
    /**
     * 查询每个博客分类下的博客名称及博客数量
     */
    @Override
    public String getBlogTypeNameAndBlogCount() throws Exception {
        // 从redis缓存中读取博客分类信息
        // 判断： redis缓存中是否存在分类的数据，如果没有数据，此时需要从数据库中查询查询出来的结果放到redis缓存中
        String blogTypeInfo = redisTemplate.opsForValue().get("blog_name_count");
        if (blogTypeInfo == null || blogTypeInfo.equals("") || blogTypeInfo.length() == 0){
             // 如果缓冲区没有数据，需要从数据库中查询，查出来的结果要放到redis缓存中
            List<Blogtype> blogList = blogtypeMapper.getBlogTypeNameAndBlogCount();
            // 将集合转换成json字符串
            blogTypeInfo = JSON.toJSONString(blogList);
            // 将集合中的数据放到缓存中
            redisTemplate.opsForValue().set("blog_name_count", blogTypeInfo);
        }


        return blogTypeInfo;
    }
}
```

### 编写js文件加载日志博客类别

```js
$.get("/blogtype/typelist",function (data) {
        var blogTypeList = $("#blogTypeList");
        //循环遍历json数组
        $(data).each(function () {
            var li = "<li><span><a href='/index.html?typeId="+this.id+"'>"+this.typeName+" ("+this.blognum+")</a></span></li>";
            //将每一个li标签追加到ul标签
            $(blogTypeList).append(li);
        });
    },"json");
```

### 编写控制类获取前端请求

```java
@Slf4j
@Controller
@RequestMapping("/blogtype")
public class BlogtypeController {

    @Resource
    private BlogtypeService typesService;

    /**
     * 查询博客类别
     * @return
     */
    @ResponseBody
    @GetMapping("/typelist")
    public String typeList(){
        try {
            log.info(typesService.getBlogTypeNameAndBlogCount());
            return typesService.getBlogTypeNameAndBlogCount();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }

}

```

运行效果

![image-20200422123125316](E:\笔记图片\image-20200422123125316.png)

## 博客首页-按日志日期查询

### xml下写sql语句

```xml
<select id="getBlogDateNameAndBlogCount" resultType="com.blog.entity.Blog">
        select DATE_FORMAT(releaseDate, '%Y年%m月') releaseDateStr , count(1) blogNum from t_blog group by DATE_FORMAT(releaseDate, '%Y年%m月')
    </select>
```

### 修改Blog实体类， 并添加Get Set方法

```java
 	@TableField(exist = false)
    private Integer blogNum;

    public Integer getBlogNum() {
        return blogNum;
    }
	public String getReleaseDateStr() {
        return releaseDateStr;
    }

    public void setReleaseDateStr(String releaseDateStr) {
        this.releaseDateStr = releaseDateStr;
    }

    @TableField(exist = false)
    private String releaseDateStr;
```

### BlogService接口及实现类

```java 
@Service
public class BlogServiceImpl extends ServiceImpl<BlogMapper, Blog> implements BlogService {

    @Resource
    private BlogMapper blogMapper;
    @Resource
    private RedisTemplate<String, String> redisTemplate;

    @Override
    public String getBlogDateNameAndBlogCount() throws Exception {
        /**
         * 1.先从redis缓存中读取 数据， 如果存在， 直接返回
         * 2.如果缓存中数据不存在 就在数据库中查找
         * 3.将查找到的数据转换成json字符串
         * 4.将该json字符串存入redis缓存中
         * 5.返回
         */
        String blogDateCount = redisTemplate.opsForValue().get("blog_date_count");
        if (blogDateCount == null || blogDateCount.equals("") || blogDateCount.length() == 0){
            List<Blog> blogDateNameAndBlogCount = blogMapper.getBlogDateNameAndBlogCount();
            blogDateCount = JSON.toJSONString(blogDateNameAndBlogCount);
            redisTemplate.opsForValue().set("blog_date_count", blogDateCount);
        }
        return blogDateCount;
    }
}

```

### 编写js文件以添加日期日志分类

```js
//按博客日期查询
    $.get("/blog/blogDateList",function (data) {
        var blogList = $("#dateList");
        //循环遍历json数组
        $(data).each(function () {
            var li = "<li><span><a href='/index.html?releaseDateStr="+this.releaseDateStr+"'>"+this.releaseDateStr+"("+this.blogNum+")</a></span></li>";
            //将每一个li标签追加到ul标签
            $(blogList).append(li);
        });
    },"json");
```



### 编写控制类获取前端请求

```java
@Controller
@RequestMapping("/blog")
public class BlogController {

    @Resource
    private BlogService blogService;
    @ResponseBody  //该注解不可少，如果没有就将自动被Thymeleaf引擎解析
    @GetMapping("/blogDateList")
    public String dateList(){
        try {
            return blogService.getBlogDateNameAndBlogCount();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }

}
```

运行效果

![image-20200422164736432](E:\笔记图片\image-20200422164736432.png)

## 首页-最新博客查询

### MP分页配置类

#### 编写MyBatis plus 分页配置类

```java
@Configuration
@MapperScan("com.blog.dao")//加载mapper接口
@EnableTransactionManagement//开启事务管理器
public class PageMPConfig {
    /**
     * 分页插件
     * @return
     */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        return new PaginationInterceptor();
    }
}
```



### BlogMapper接口

```java
/**
     * 分页查询博客信息
     * @param page
     * @param blog
     * @return
     */
    IPage<Blog> findBlogByPage(@Param("page") IPage<Blog> page, @Param("blog") Blog blog);
```



### BlogMapper.xml

```xml
 <select id="findBlogByPage" resultType="com.blog.entity.Blog">
        select b.*,t.id type_id,typename from t_blog b
        inner join t_blogtype t on b.typeId = t.id
        <where>
            <if test="blog.keyWord!=null and blog.keyWord!=''">
                and  b.keyword like concat('%',#{blog.keyWord},'%')
            </if>
            <if test="blog.typeId!=null">
                and b.typeId = #{blog.typeId}
            </if>
            <if test="blog.releaseDateStr!=null and blog.releaseDateStr!=''">
                and date_format(b.releasedate,'%Y年%m月') = #{blog.releaseDateStr}
            </if>
            <if test="blog.title!=null and blog.title!=''">
                and  b.title like concat('%',#{blog.title},'%')
            </if>
        </where>
        order by b.releasedate desc
    </select>
```



### BlogServiceImpl.java

```java
@Override
    public IPage<Blog> findBlogByPage(IPage<Blog> page, Blog blog) {
        return blogMapper.findBlogByPage(page, blog);
    }
```



### IndexController控制器

```java
@Controller
public class IndexController {
    @Resource
    private BlogService blogService;

    /**
     * 首页查询最新博客内容
     */
    @RequestMapping(value = {"/", "/index", "/index.html"})
    public String index(Blog blog, @RequestParam(value = "page", defaultValue = "1")Long current, Model model){
        int size = 5;
        // 创建分页对象， 指定当前页码及每页显示数量
        Page<Blog> page = new Page<Blog>(current, size);
        StringBuffer param = new StringBuffer();
        if (blog != null){
            if (blog.getReleaseDateStr() != null && !"".equals(blog.getReleaseDateStr())){
                param.append("releaseDateStr=" + blog.getReleaseDateStr().equals(""));
            }
            if (blog.getTypeId() != null){
                param.append("typeId=" + blog.getTypeId());
            }
        }
        // 分页查询
        IPage<Blog> blogIPage = blogService.findBlogByPage(page, blog);
        // 获取博客数据列表
        List<Blog> blogList = blogIPage.getRecords();
        model.addAttribute("blogList", blogList);
        model.addAttribute("pageContext", "foreign/main");
        model.addAttribute("pageCode",  PageUtil.genPagination("/index.html",blogIPage.getTotal(),current.intValue(),size,param.toString()));
        return "index";
    }
}
```

### 修改Blog实体类的日期格式

```java
/**
     * 博客发布时间
     * 替换为Date格式,否则报错
     */
    @TableField("releaseDate")
    private Date releaseDate;
```

## 完善博客最新查询信息

### 添加PageUtil工具类

```java
package com.blog.utils;

/**
 * 分页工具类
 * @author Administrator
 *
 */
public class PageUtil {

    /**
     * 生成分页代码
     * @param targetUrl     目录访问路径
     * @param totalNum      总记录数
     * @param currentPage   当前页码
     * @param pageSize      每页显示数量
     * @param param         查询条件参数
     * @return
     */
    public static String genPagination(String targetUrl,long totalNum,int currentPage,int pageSize,String param){
        //计算总页数
        long totalPage=totalNum%pageSize==0?totalNum/pageSize:totalNum/pageSize+1;
        if(totalPage==0){
            return "未查询到数据";
        }else{
            StringBuffer pageCode=new StringBuffer();
            pageCode.append("<ul class=\"pagination pagination-sm\">");
            //如果当前页码大于1
            if(currentPage>1){
                //首页和上一页的可以点击
                pageCode.append("<li><a href='"+targetUrl+"?page=1&"+param+"'>首页</a></li>");
                pageCode.append("<li><a href='"+targetUrl+"?page="+(currentPage-1)+"&"+param+"'>上一页</a></li>");
            }else {
                //如果当前页码是第一页，首页和上一页不能点击
                pageCode.append("<li class='disabled'><a>首页</a></li>");
                pageCode.append("<li class='disabled'><a>上一页</a></li>");
            }
            //动态生成页码按钮（随着当前页码，页码按钮随之改变）
            for(int i=currentPage-2;i<=currentPage+2;i++){
                if(i<1||i>totalPage){
                    continue;
                }
                if(i==currentPage){
                    pageCode.append("<li class='active'><a href='"+targetUrl+"?page="+i+"&"+param+"'>"+i+"</a></li>");
                }else{
                    pageCode.append("<li><a href='"+targetUrl+"?page="+i+"&"+param+"'>"+i+"</a></li>");
                }
            }
            //如果当前页码小于总页数，下一页和尾页可以点击
            if(currentPage<totalPage){
                pageCode.append("<li><a href='"+targetUrl+"?page="+(currentPage+1)+"&"+param+"'>下一页</a></li>");
                pageCode.append("<li><a href='"+targetUrl+"?page="+totalPage+"&"+param+"'>尾页</a></li>");
            }else{
                pageCode.append("<li class='disabled'><a>下一页</a></li>");
                pageCode.append("<li class='disabled'><a>尾页</a></li>");
            }

            pageCode.append("</ul>");
            return pageCode.toString();
        }
    }


}

```

### 修改BlogMapper.xml

由于之前只对类型进行查询，没有查出id，所以要增加查询typeId列

![image-20200422225921302](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200422225921302.png)

由于之前查过，在redis中存在缓存，要先删除缓存才能通过数据库进行查询

![image-20200422230358149](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200422230358149.png)

### 修改IndexController类

![image-20200422230628410](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200422230628410.png)

**leftmenu.js中的url参数typeId属性需要与mapper文件中的字段保持一致**

![image-20200422230952409](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200422230952409.png)



![image-20200422232135491](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200422232135491.png)

否则this.id是**undifine**

## 完善首页-内容模块

### 提起内容模块

将index中的内容模块的提取到main页面

![image-20200423090002657](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200423090002657.png)

根据后台要传入进来的值进行查看首页或博客内容信息

### 根据id查询博客详细信息

### 修改BlogService代码

```java
@Override
    public Blog getBlogById(int id) throws Exception {
        return blogMapper.getBlogById(id);
    }
```

### 修改BlogDao接口以及xml文件

```java
Blog getBlogById(int id);
```

### BlogMapper映射文件

```xml
 <select id="getBlogById" resultType="com.blog.entity.Blog">

    </select>
```

### BlogController.java

```java
 /**
     * 根据博客id查询详细信息
     */
    @GetMapping("/view/{id}")
    public String getBlog(@PathVariable("id") int id){
        blogService.getBlogById();
        return "foreign/blog/view";
    }
```

![image-20200423094112016](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200423094112016.png)

![image-20200423102645940](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200423102645940.png)

### 修改阅读量，再service实现类中进行修改

**1.先根据主键id查询出blog详细信息**

**2.将查询出来的blog中的阅读量+1，每次点击刷新都自动会+1**

**3.读取数据库的更新操作**

```java
 @Override
    public Blog getBlogById(int id) throws Exception {
        Blog blog = blogMapper.getBlogById(id);
        blog.setClickHit(blog.getClickHit() + 1);
        blogMapper.updateById(blog);
        return blog;
    }
```

### 关键字显示

添加**BlogController**

```java
             // 获取关键字
            String keyWordList = blog.getKeyWord();
            if (keyWordList != null){
                // 如果关键字不为空，则进行拆分， 传到model
                String[] str = keyWordList.split(" ");
                model.addAttribute("keyWordList", keyWordList);
            }else{
                // 如果为空， 传入null
                model.addAttribute("keyWordList", null);
            }
```

**因为传入的是keyWordList，所以模板对应的html也应修改属性**

```html
<div class="blog_keyWord">
                <font><strong>关键字：</strong></font>
                <font th:if="${keyWordList==null}">
                    &nbsp;&nbsp;无关键字
                </font>
                <font th:if="${keyWordList!=null}" th:each="word :${keyWordList}">
                    &nbsp;&nbsp;&nbsp;&nbsp;<a th:href="@{/blog/query(keyWord=${word})}" target="_blank" th:text="${word}">Java</a>&nbsp;&nbsp;
                </font>

            </div>
```

## 添加上一页下一页超链接

### BlogMapper.xml增加上下页查询

```xml
   <select id="findNextBlog" resultType="com.blog.entity.Blog">
        select * from t_blog where id &gt; #{nextId} order by id asc limit 1
    </select>
    <select id="findPrevBlog" resultType="com.blog.entity.Blog">
        select * from t_blog where id &lt; #{preId} order by id desc limit 1
    </select>
```

### BlogMapper接口添加方法

```java
    Blog findPrevBlog(int preId);

    Blog findNextBlog(int nextId);
```

### BlogService以及BlogServiceImp实现类

```java
    Blog findPrevBlog(int id) throws Exception;

    Blog findNextBlog(int id) throws Exception;
```

```java
/**
     * 查看上一篇博客
     *
     * @param id
     * @return
     * @throws Exception
     */
    @Override
    public Blog findPrevBlog(int id) throws Exception {
        return blogMapper.findPrevBlog(id);
    }

    /**
     * 查看下一篇博客
     *
     * @param id
     * @return
     * @throws Exception
     */
    @Override
    public Blog findNextBlog(int id) throws Exception {
        return blogMapper.findNextBlog(id);
    }
```

BlogController.java修改getBlog（）方法

```java
 /**
     * 根据博客id查询详细信息
     */
    @GetMapping("view/{id}")
    public String getBlog(@PathVariable("id") int id, Model model){
        try {
            Blog blog = blogService.getBlogById(id);
            // 将博客信息保存到model中
            model.addAttribute("blog", blog);
            // 获取关键字
            String keyWordList = blog.getKeyWord();
            if (keyWordList != null){
                // 如果关键字不为空，则进行拆分， 传到model
                String[] str = keyWordList.split(" ");
                model.addAttribute("keyWordList", keyWordList);
            }else{
                // 如果为空， 传入null
                model.addAttribute("keyWordList", null);
            }
            model.addAttribute("pageCode", getUpAndDownPageCode(blogService.findPrevBlog(id), blogService.findNextBlog(id)));
            model.addAttribute("pageContext", "foreign/blog/view");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return "index";
        /**
     * 获取博客的上一篇和下一篇
     * @param prev  上一篇
     * @param next  下一篇
     * @return
     */
    private String getUpAndDownPageCode(Blog prev,Blog next){
        StringBuffer sb = new StringBuffer();
        //如果上一篇对象为空，表示没有上一篇
        if(prev==null || prev.getId()==null){
            sb.append("<p>上一篇：没有上一篇了~</p>");
        }else{
            sb.append("<p>上一篇：<a href='/blog/view/"+prev.getId()+"'>"+prev.getTitle()+"</a></p>");
        }

        //如果下一篇对象为空，表示没有下一篇
        if(next==null || next.getId()==null){
            sb.append("<p>下一篇：没有下一篇了~</p>");
        }else{
            sb.append("<p>下一篇：<a href='/blog/view/"+next.getId()+"'>"+next.getTitle()+"</a></p>");
        }
        return sb.toString();
    }
```



### view.html

```html
<div class="blog_lastAndNextPage" th:utext="${pageCode}"></div>
```



## 博客评论页-查询与添加

### index.html给评论按钮添加点击事件

给点击事件中添加ajax方法，提交用户评论信息

```js
$(function () {
            //当点击评论按钮
            $("#commentBtn").click(function () {
                //获取输入的内容
                var content = $("#comment").val().trim();
                //获取当前的博客id
                var blogId = $("#blogId").val().trim();
                //判断评论内容是否为空
                if(content==null || content.length==0){
                    alert("评论内容不能为空！");
                    return;
                }
                $.post("/comment/addComment",{"content":content,"blogId":blogId},function (data) {
                    if(data.success){
                        alert("博客评论成功！待审核通过后显示！");
                        $("#comment").val("");//清空评论输入框信息
                    }else {
                        alert("博客评论失败！");
                    }
                },"json");
            });
        })
```

### 修改Comment实体类

将原本的MP自动生成的时间类修改为java.util.Date时间类

![image-20200423220108355](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200423220108355.png)



### 添加CommentService接口和其实现类

```java
public interface CommentService extends IService<Comment> {
    /**
     * 根据博客id查询该博客下的评论列表
     * @param id
     * @param state
     * @return
     * @throws Exception
     */
    List<Comment> findCommentByBlogId(int id, int state) throws Exception;
}
@Service
public class CommentServiceImpl extends ServiceImpl<CommentMapper, Comment> implements CommentService {

    @Resource
    private CommentMapper commentMapper;

    /**
     * 根据博客id删除评论
     *
     * @param id
     * @return
     * @throws Exception
     */
    public List<Comment> findCommentByBlogId(int id, int state) throws Exception {
        QueryWrapper<Comment> queryWrapper = new QueryWrapper<Comment>();
        queryWrapper.eq("blogId",id);//博客id
        queryWrapper.eq("state",state);//审核状态
        return commentMapper.selectList(queryWrapper);

    }
}
```

### 添加SysConstant接口

定义两个静态变量（1表示未审核， 2表示已审核）

```java
public interface SysConstant {
    int STATUS_NO = 1;  // 未审核状态
    int STATUS_OK = 2;  // 审核状态
}
```

### 添加CommonComtroller.java

```java
@Controller
@RequestMapping("/comment")
public class CommentController {

    @Resource
    private CommentService commentService;


    @ResponseBody
    @PostMapping("/addComment")
    public String addComment(Comment comment) throws UnknownHostException {
        Map<String,Object> map = new HashMap<String, Object>();
        //设置评论信息
        try {
            comment.setCommentDate(new Date());//评论时间就是当前系统时间
            comment.setState(SysConstant.STATUS_NO);//未审核
            comment.setUserIp(InetAddress.getLocalHost().getHostAddress());//获取当前ip地址
            //调用添加评论的方法
            //该save()方法是MyBatisPlus自带的方法
            boolean flag = commentService.save(comment);
            if(flag){
                map.put("success",true);//成功
            }else{
                map.put("success",false);//失败
            }
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
        return JSON.toJSONString(map);
    }

}

```

### view.html

![image-20200423222747107](C:\Users\DW\AppData\Roaming\Typora\typora-user-images\image-20200423222747107.png)



