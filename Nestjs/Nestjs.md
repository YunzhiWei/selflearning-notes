
# 疑问

* 

# 重点

* 核心组件

> NestJs 主要有 8 个组件（Controller 控制器、Component 组件、Module 模块、Middlewares 中间件、Exception Filters 异常过滤器、Pipes 管道、Guards 守卫、Interceptors 拦截器）
> Component 是 NestJs Ver 4.5 的称呼，5.0 之后成为 Provider

* 不同角色在请求过程中的执行顺序

> 客户端请求 ---> 中间件 ---> 守卫 ---> 拦截器之前 ---> 管道 ---> 控制器处理并响应 ---> 拦截器之后 ---> 过滤器

* 不同角色的特点

    - 功能
        + 中间件    ：访问 请求（req） 和 响应（res） 对象，并调用下一个 中间件（next）
        + 过滤器    ：处理所有抛出的异常
        + 管道      ：对请求参数做变形（纯函数）
        + 守卫      ：做权限认证
        + 拦截器    ：特殊功能，类似于AOP面向切面编程，

    - 实现方式
        + 中间件    ：由 @Injectable() 装饰的类 | 函数
        + 过滤器    ：
        + 管道      ：用@Injectable()装饰器注释的类
        + 守卫      ：用@Injectable()装饰器注释的类
        + 拦截器    ：用@Injectable()装饰器注释的类

    - 实现为类时，所需实现的接口
        + 中间件    ：NestMiddleware
        + 过滤器    ：ExceptionFilter 
        + 管道      ：PipeTransform
        + 守卫      ：CanActivate
        + 拦截器    ：NestInterceptor 

    - 使用方式
        + 中间件    ：全局注册（app.use）               | 模块注册（config(consumer) { consumer.apply().with().exclude().forRoutes()）
        + 过滤器    ：全局注册（app.useGlobalFilters）  | 装饰器（@UseFilters）装饰控制器   | 装饰器（@UseFilters）装饰路由
        + 管道      ：全局注册（app.useGlobalPipes）    | 作用于当前控制器（@UsePipes)      | 作用于当前路由（@UsePipes)        | 作用于当前的 Body（@Body）
        + 守卫      ：全局注册（app.useGlobalGuards）   | 作用于当前控制器（@UseGuards) 
        + 拦截器    ：全局注册（app.useGlobalInterceptors）   | 作用于当前控制器（@UseInterceptors)  | 作用于当前路由（@UseInterceptors) 

* 不同角色所需实现的接口

# 参考资料

* [让我们用Nestjs来重写一个CNode](https://www.jianshu.com/p/f0a4944e8fb9)

# 备忘

* 全局安装：typescript

> 否则 nest g 命令会报错
