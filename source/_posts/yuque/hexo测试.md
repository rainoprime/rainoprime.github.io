---
title: hexo测试
urlname: dl2oyz
date: '2021-06-05 12:05:36 +0800'
<br />title: hexo测试
tags:
  - Java
categories:
  - - Spring
    - SpringMvc
---

# 前言

> 介绍针对拦截器怎么使用 232323

```java

package com.newamahb.newamahb.utils;

import com.newamahb.newamahb.entity.DbAdminUserEntity;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;


import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 登录验证
 *
 * @ClassName LoginFilter
 * @Author LiuJinshui
 * @Data 2021/5/24 13:11
 **/
@Configuration
public class LoginFilter implements HandlerInterceptor {
    /**
     * 在请求处理之前进行调用（Controller方法调用之前）
     */
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {
//        System.out.println("执行了TestInterceptor的preHandle方法");
        try {
            //统一拦截（查询当前session是否存在user）(这里user会在每次登陆成功后，写入session)
            DbAdminUserEntity user=(DbAdminUserEntity)request.getSession().getAttribute("user");
            if(user!=null){
                return true;
            }
            response.sendRedirect(request.getContextPath()+"/");
        } catch (IOException e) {
            e.printStackTrace();
        }
        return false;//如果设置为false时，被请求时，拦截器执行到此处将不会继续操作
        //如果设置为true时，请求将会继续执行后面的操作
    }

    /**
     * 请求处理之后进行调用，但是在视图被渲染之前（Controller方法调用之后）
     */
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) {
//         System.out.println("执行了TestInterceptor的postHandle方法");
    }

    /**
     * 在整个请求结束之后被调用，也就是在DispatcherServlet 渲染了对应的视图之后执行（主要是用于进行资源清理工作）
     */
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) {
//        System.out.println("执行了TestInterceptor的afterCompletion方法");
    }
}
```

```java
package com.newamahb.newamahb.utils.config;

import com.newamahb.newamahb.utils.LoginFilter;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

/**
 * @ClassName LoginConfig
 * @Author LiuJinshui
 * @Data 2021/5/24 13:34
 **/
@Configuration
public class LoginConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //注册TestInterceptor拦截器
        InterceptorRegistration registration = registry.addInterceptor(new LoginFilter());
        registration.addPathPatterns("/**");                      //所有路径都被拦截
        registration.excludePathPatterns(               //添加不拦截路径
                "/",                            //首页
                "/amahb/login",            //登录
                "/static/**",            //html静态资源
                "/js/**",              //js静态资源
                "/css/**",             //css静态资源
                "/fonts/**",
                "/img/**",
                "/lib/**",
                "/templates/**"
        );
    }
}
```
