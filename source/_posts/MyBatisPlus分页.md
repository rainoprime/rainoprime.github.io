---
title: MyBatisPlus分页
date: 2021-06-05 21:06:30
tags:
- Java
- MyBatisPlus
categories:
- 高级框架
---

> MybatisPlus的IPage分页插件的使用流程，代码示例Controller，Server，ServerImpl，Mapper，Vo，Config

<!--more-->

# 一、创建配置类

首先创建配置类，注入分页插件。

```java
@Configuration//标记该类是一个配置类
@EnableTransactionManagement//开启事务管理
@MapperScan(basePackages = {"com.liujinshui.demo.dao"})//加载mapper接口所在的包
public class MyBatisPlusConfig {
    /**
     * 注入分页插件
     * @return
     */
    @Bean
    public PaginationInterceptor paginationInterceptor(){
        return new PaginationInterceptor();
    }
}
```

# 二、Dao层

```java
@Mapper
public interface UserMapper extends BaseMapper<User> {
    
    @Select("select 字段名 from user where userName = #{user.userName}")
    IPage<User> getAllUser(@Param("page") IPage<User> page, @Param("user") UserVo userVo);
}
```

# 三、Service层

```java
public interface UserService { 
    IPage<User> getAllUser(IPage<User> page, UserVo userVo);
}
```

# 四、ServiceImpl层

```java
public class UserServiceImpl implement UserService{
    @Autowired
    private UserMapper userMapper;
    
    @Override
    public IPage<User> getAllUser(IPage<User> page, UserVo userVo) {
        return userMapper.getAllUser(page, userVo);
    }
}
```

# 五、Vo层

```java
public class UserVo extends User {
    
    private Integer page;//当前页码
    private Integer limit;//每页显示数量

    public Integer getPage() { return page; }

    public void setPage(Integer page) { this.page = page; }

    public Integer getLimit() { return limit; }

    public void setLimit(Integer limit) { this.limit = limit; }
}
```

# 六、Controller层

```java
@Controller
@RequestMapping("/sys")
public class UserController {
    
    @Autowired
    private UserService userService;
    
    @GetMapping("/getAllUser")
    @ResponeBody
    public JSONResult getAllUser(UserVo userVo) {
        IPage<User> page = new Page<>(userVo.getPage(), userVo.getLimit());
        IPage<User> pageUser = userService.getAllUser(page, userVo);
        //向前端传入count, data
        return new JSONResult(pageUser.getTotal(), pageUser.getRecords());
    }
}
```
