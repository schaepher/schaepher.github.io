# Spring Boot


## 过滤器

配置过滤器 Filter 来对特定类的方法做是否登录的判断

添加 Filter 的方法：

1. 创建过滤器
   ```java
   public class EncodingFilter implements Filter {
    private static final String CONTENT_TYPE = "text/html;charset=UTF-8";

    public EncodingFilter() {
    }

    public void destroy() {
    }

    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        request.setCharacterEncoding("UTF-8");
        response.setCharacterEncoding("UTF-8");
        response.setContentType("text/html;charset=UTF-8");
        chain.doFilter(request, response);
    }

    public void init(FilterConfig filterConfig) throws ServletException {
    }
   }
   ```
2. 配置类注解 `@Configuration`
3. 配置类方法注解 `@Bean`
4. 配置类方法内容：  
   ```java
    FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean();
    filterRegistrationBean.setOrder(3); // 设置过滤顺序，越小越先执行
    filterRegistrationBean.setFilter(new YourFilter()); // 设置过滤器
    filterRegistrationBean.setName("customFilter"); // 设置过滤器名称
    filterRegistrationBean.addUrlPatterns("*.action"); // 设置使用该过滤器的 Url 特征
    return filterRegistrationBean;
   ```


见：  
[https://www.jianshu.com/p/05c8be17c80a](https://www.jianshu.com/p/05c8be17c80a)


## 问题集

1. 如何验证用户是否已登录？
2. 如何配置过滤器
3. @Configuration
4. 任意类都可以加上 @Configuration 么
5. Spring Boot 扫描的规则是什么
6. @ComponentScan 和 @ServletComponentScan 有什么区别？  
   为什么教程说 @ServletComponentScan ，而实际使用自带的 @SpringBootApplication （包含 @ComponentScan）就可以？  
   > @WebServlet, @WebFilter, and @WebListener annotated classes can be automatically registered with an embedded Servlet container by annotating @ServletComponentScan on a @Configuration class and specifying the packages.

7. 为何例子里面没有 @WebFilter
8. 如何读取配置文件

http://idea.medeming.com/jetbrains/

https://www.cnblogs.com/oucbl/p/11664610.html#_label1

https://github.com/ddd-by-examples/factory

https://stackoverflow.com/questions/52321971/ddd-ports-and-adapters-with-onion-architecture-what-goes-where


概念数据模型 Conceptual Data Models

http://blog.sina.com.cn/s/blog_45eaa01a0102xf3q.html
