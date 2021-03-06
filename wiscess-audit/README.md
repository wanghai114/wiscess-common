# wiscess-audit:

## 版本：v2.0

#####更新时间：2019-01-22

#####更新内容：

1.增加黑名单的处理，根据预设的规则，同一个IP，5分钟内的访问session不同的次数超过10次，即被认定是攻击，加入黑名单；<br/>

2.在审计过滤器中增加黑名单ip的判断，如果判定是黑名单中的ip，直接返回error页面，提示对方不允许访问。


#####更新时间：2018-12-29

#####更新内容：

1.auditFilter的顺序为-9999，排在security之前，登录之前的所有请求也会被记录；排在xssFilter之前，获取到的参数值为原始值，可以记录攻击者的攻击记录；<br/>

2.启动时自动检测当前数据库类型和名称，是否有数据库或表，是否启用审计功能；如果不存在数据库和表，自动执行建库建表语句；

3.记录所有的请求，除了已知的静态资源/css/\**,/js/\**,/images/\**,/webjars/\**,/\**/favicon.ico,/captcha.jpg,可以通过参数增加排除的请求路径；

4.默认所有请求方法都审计，可以通过参数进行配置；

5.指定审计级别，记录请求数据的详细程度。

##参数配置说明：

1.application.yml中添加audit的配置参数：<br/>
<pre>
audit:
  enable: true    #是否启用审计功能，默认为true
  databaseName:   #审计数据库名称，默认为空，与当前项目使用的数据库相同，为将审计记录与项目数据分开，可以指定审计专用的数据库；
  auditMethod:    #审计请求方法，默认为*，全部审计，可以指定请求方法，如GET|POST|PUT|OPTIONS等；
  excludes:       #排除的请求，默认已经排除了常用的静态资源，可以自行添加；
  auditLevel:     #审计级别，默认为0，只记录基本的审计记录
  simples:        #简单记录参数的请求，可以指定请求，不记录参数值的完整数据，只记录参数名称；
  application:    #记录当前应用名称，默认为当前数据库名称
  view:
    username:     #指定查看审计记录的用户名，可以指定多个，用|分隔
    
</pre>  
