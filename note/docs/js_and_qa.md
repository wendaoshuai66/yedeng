
#JavaScript与QA测试工程师
##单元测试
###目的
单元测试能够让开发者明确知道代码结果
###原则
单一职责 （通俗的理解的话是管好你自己的事）

接口抽象

层次分离

###断言库
保证最小单元式是否正常运行检测方法

###测试风格
都是敏捷开发方法论

测试驱动开发（Test-Driven Development TDD）：关注所有的功能是否被实现（每一个功能都会有相应的测试用例），suite配合test利用assert（tobi == ueser.name）


行为驱动开发（Behavior-Driven Development BDD）：关注整体行为是否否和整体预期，编写每行代码都有目的提供一个全面的测试用例集


###单元测试框架

better-assert（TDD断言库 Github）

should.js(BDD断言库 Github)

expect.js（BDD断言库 Github）

chaai.js（TDD BDD双模 Github）

Jasmine.js（BDD Github）

Node.js 

###单元测试运行流程

每一个测试用例通过describe进行设置

![单元测试流程](https://wendaoshuai66.github.io/study/note/images/ceshiyongli.png)

1.before 单个测试用例开始之前


2.beforeEach 每一个测试用例开始之前

3.it定义测试用例，并利用断言库进行设置chai 如expect(x).to.equal(true);

异步mocha

4.以上术语叫mock

###自动化单元测试

karma自动化runner集成 PhantomJS 无刷新

##性能测试

面向切面编程AOP无侵入式统计

Benchmark基准测试 （样本）

##压力测试

1.对网络接口做压力测试需要检测几个常用指标有 吞吐率 响应时间和并发数

2.PV网站当日访问人数 UV独立访问人数。QPS = PV/t

常用的压力测试工具ab siege http_load

##安全测试

XSS

SQl

CSRF

##功能测试

用户真实性检查
