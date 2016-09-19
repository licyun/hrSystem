#struts2 spring hibernate 实现的简单员工管理系统
##演示站[简单的员工定时管理系统](http://java.licyun.com/hrSystem/)
    经理帐号：oracle weblogic
    员工帐号：mysql hsql tomcat jetty
    所有密码都和帐号相同
##一.系统功能介绍
    系统分为两个角色：普通员工和经理
    普通员工的功能包括：系统自动完成普通员工每天上下班的考勤记录，员工可以查看工资及3天内的考勤打卡情况，如果发现考勤与实际不符，可以提交申请给经理处理。
    经理继承员工的功能，不同之处在于：能增加员工，审核员工的考勤申请以及查看员工的工资。但经理不能申请考勤修改。
    Quartz配合cron触发器实现系统定时执行任务。
##二.功能模块
###  1.传统表现层:JSP
    本系统使用JSP作为表现层，负责手机用户的请求数据，以及业务数据的展示。
###  2.MVC框架
    本系统使用struts2.2作为mvc框架，本应用中所有的应用请求都必须发给struts的action.由struts控制处理和转发。
###  3.spring框架
    Spring提供的ioc容器是业务逻辑组件和DAO组件的工厂,他负责并管理这些实例。
    本应用的所有DAO都继承hibernateDaoSupport，借助于spring的ioc容器的注入和DAO支持，程序开发者无需管理hibernate的sessionfactory和session对象，直接使用spring提供的hibernateTemp即可完成数据库操作。
###  4.hibernate
    Hibernate作为orm框架，封装了JDBC，以面向对象的方式操作数据库。为底层DAO的实现提供了支持。
##三.系统结构
###  action
    控制系统的url及表现等数据的请求处理。保证系统的安全性。
###  dao 
    封装hibernate持久层，每个DAO都对应包含数据库的逻辑访问，可对一个数据库表完成基本的CRUD操作。
###  domain
    hibernate持久层，完成持久层的建立及对应表的映射规则。
###  exception
    系统异常处理
###  schedule
    quartz定时执行考勤记录和工资发放模块。
###  service
    业务逻辑处理，实现manager和employee两个业务逻辑组件的功能，面向DAO层编程。
###  vo
###  web
    验证码实现
