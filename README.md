## Description

This is a small reproducible issue of a missing hint for Spring boot sleuth

### Steps to reproduce

- Run the following command `./gradlew clean bootBuildImage` 
  - The generated image will be called `sleuth-native-missing-hint:0.0.1-SNAPSHOT`
- Run bot docker-compose files inside `docker` folder
  - Run `mysql.docker-compose.yml` for the database
  - Run `docker-compose.yml` after generating the image
- Then in the logs of the container you should see:

```
2022-07-06 12:07:15.745 DEBUG [,,] 1 --- [           main] t.AbstractTransactionManagerInstrumenter : Exception occurred while trying to create a proxy, falling back to JDK proxy

org.springframework.aop.framework.AopConfigException: Unexpected problem loading and instantiating proxy for target class class org.springframework.r2dbc.connection.R2dbcTransactionManager; nested exception is java.lang.IllegalState
Exception: Class proxy missing at runtime, hint required at build time: @AotProxyHint(targetClass=org.springframework.r2dbc.connection.R2dbcTransactionManager.class, proxyFeatures = ProxyBits.IS_STATIC)
        at org.springframework.aop.framework.BuildTimeAopProxy.getProxy(BuildTimeAopProxy.java:159) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.aop.framework.ProxyFactoryBean.getProxy(ProxyFactoryBean.java:370) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.aop.framework.ProxyFactoryBean.getSingletonInstance(ProxyFactoryBean.java:328) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.aop.framework.ProxyFactoryBean.getObject(ProxyFactoryBean.java:252) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.getObject(AbstractTransactionManagerInstrumenter.java:111) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintAppl
ication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.createProxy(AbstractTransactionManagerInstrumenter.java:120) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintAp
plication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.wrapManager(AbstractTransactionManagerInstrumenter.java:97) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApp
lication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.instrument(AbstractTransactionManagerInstrumenter.java:88) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintAppl
ication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.TraceReactiveTransactionManagerBeanPostProcessor.postProcessAfterInitialization(TraceReactiveTransactionManagerBeanPostProcessor.java:40) ~[com.example.sleuthnativ
emissinghint.SleuthNativeMissingHintApplication:3.1.3]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyBeanPostProcessorsAfterInitialization(AbstractAutowireCapableBeanFactory.java:455) ~[com.example.sleuthnativemissinghint.SleuthNativeMissin
gHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1808) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:620) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:542) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:335) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:333) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:208) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:955) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:918) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:583) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.boot.web.reactive.context.ReactiveWebServerApplicationContext.refresh(ReactiveWebServerApplicationContext.java:66) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:2.7.1]
        at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:734) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:408) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:308) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1306) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1295) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication.main(SleuthNativeMissingHintApplication.java:10) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
Caused by: java.lang.IllegalStateException: Class proxy missing at runtime, hint required at build time: @AotProxyHint(targetClass=org.springframework.r2dbc.connection.R2dbcTransactionManager.class, proxyFeatures = ProxyBits.IS_STAT
IC)
        at org.springframework.aop.framework.BuildTimeAopProxy.getProxy(BuildTimeAopProxy.java:147) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        ... 26 common frames omitted

2022-07-06 12:07:15.745 DEBUG [,,] 1 --- [           main] o.s.aop.framework.ProxyFactoryBean       : Advice has changed; re-caching singleton instance
2022-07-06 12:07:15.745 DEBUG [,,] 1 --- [           main] o.s.aop.framework.ProxyFactoryBean       : Advice has changed; re-caching singleton instance
2022-07-06 12:07:15.745 DEBUG [,,] 1 --- [           main] o.s.aop.framework.ProxyFactoryBean       : Advice has changed; re-caching singleton instance
2022-07-06 12:07:15.745 DEBUG [,,] 1 --- [           main] o.s.aop.framework.ProxyFactoryBean       : Advice has changed; re-caching singleton instance
2022-07-06 12:07:15.745  WARN [,,] 1 --- [           main] .r.c.ReactiveWebServerApplicationContext : Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationEx
ception: Error creating bean with name 'connectionFactoryTransactionManager': Initialization of bean failed; nested exception is com.oracle.svm.core.jdk.UnsupportedFeatureError: Proxy class defined by interfaces [interface org.sprin
gframework.beans.factory.InitializingBean, interface org.springframework.transaction.ReactiveTransactionManager, interface java.io.Serializable, interface org.springframework.aop.SpringProxy, interface org.springframework.aop.framew
ork.Advised, interface org.springframework.core.DecoratingProxy] not found. Generating proxy classes at runtime is not supported. Proxy classes need to be defined at image build time by specifying the list of interfaces that they im
plement. To define proxy classes use -H:DynamicProxyConfigurationFiles=<comma-separated-config-files> and -H:DynamicProxyConfigurationResources=<comma-separated-config-resources> options.
2022-07-06 12:07:15.746 DEBUG [,,] 1 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Shutting down ExecutorService 'applicationTaskExecutor'
2022-07-06 12:07:15.747 DEBUG [,,] 1 --- [           main] reactor.core.publisher.Hooks             : Reset onEachOperator: org.springframework.cloud.sleuth.autoconfig.instrument.reactor.TraceReactorAutoConfiguration$TraceReactorCon
figuration
2022-07-06 12:07:15.747 DEBUG [,,] 1 --- [           main] reactor.core.publisher.Hooks             : Reset onLastOperator: org.springframework.cloud.sleuth.autoconfig.instrument.reactor.TraceReactorAutoConfiguration$TraceReactorCon
figuration
2022-07-06 12:07:15.747 ERROR [,,] 1 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'connectionFactoryTransactionManager': Initialization of bean failed; nested exception is com.oracle.svm.core.jdk.UnsupportedFeatureError: Proxy
class defined by interfaces [interface org.springframework.beans.factory.InitializingBean, interface org.springframework.transaction.ReactiveTransactionManager, interface java.io.Serializable, interface org.springframework.aop.Sprin
gProxy, interface org.springframework.aop.framework.Advised, interface org.springframework.core.DecoratingProxy] not found. Generating proxy classes at runtime is not supported. Proxy classes need to be defined at image build time b
y specifying the list of interfaces that they implement. To define proxy classes use -H:DynamicProxyConfigurationFiles=<comma-separated-config-files> and -H:DynamicProxyConfigurationResources=<comma-separated-config-resources> optio
ns.
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:628) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:542) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:335) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:333) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:208) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:955) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:918) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:583) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.boot.web.reactive.context.ReactiveWebServerApplicationContext.refresh(ReactiveWebServerApplicationContext.java:66) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:2.7.1]
        at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:734) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:408) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:308) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1306) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1295) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication.main(SleuthNativeMissingHintApplication.java:10) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
Caused by: com.oracle.svm.core.jdk.UnsupportedFeatureError: Proxy class defined by interfaces [interface org.springframework.beans.factory.InitializingBean, interface org.springframework.transaction.ReactiveTransactionManager, inter
face java.io.Serializable, interface org.springframework.aop.SpringProxy, interface org.springframework.aop.framework.Advised, interface org.springframework.core.DecoratingProxy] not found. Generating proxy classes at runtime is not
 supported. Proxy classes need to be defined at image build time by specifying the list of interfaces that they implement. To define proxy classes use -H:DynamicProxyConfigurationFiles=<comma-separated-config-files> and -H:DynamicPr
oxyConfigurationResources=<comma-separated-config-resources> options.
        at com.oracle.svm.core.util.VMError.unsupportedFeature(VMError.java:89) ~[na:na]
        at com.oracle.svm.reflect.proxy.DynamicProxySupport.getProxyClass(DynamicProxySupport.java:158) ~[na:na]
        at java.lang.reflect.Proxy.getProxyConstructor(Proxy.java:48) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at java.lang.reflect.Proxy.newProxyInstance(Proxy.java:1037) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:na]
        at org.springframework.aop.framework.JdkDynamicAopProxy.getProxy(JdkDynamicAopProxy.java:126) ~[na:na]
        at org.springframework.aop.framework.ProxyFactoryBean.getProxy(ProxyFactoryBean.java:370) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.aop.framework.ProxyFactoryBean.getSingletonInstance(ProxyFactoryBean.java:328) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.aop.framework.ProxyFactoryBean.getObject(ProxyFactoryBean.java:252) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.getObject(AbstractTransactionManagerInstrumenter.java:111) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintAppl
ication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.createProxy(AbstractTransactionManagerInstrumenter.java:120) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintAp
plication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.wrapManager(AbstractTransactionManagerInstrumenter.java:104) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintAp
plication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.AbstractTransactionManagerInstrumenter.instrument(AbstractTransactionManagerInstrumenter.java:88) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintAppl
ication:3.1.3]
        at org.springframework.cloud.sleuth.autoconfig.instrument.tx.TraceReactiveTransactionManagerBeanPostProcessor.postProcessAfterInitialization(TraceReactiveTransactionManagerBeanPostProcessor.java:40) ~[com.example.sleuthnativ
emissinghint.SleuthNativeMissingHintApplication:3.1.3]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyBeanPostProcessorsAfterInitialization(AbstractAutowireCapableBeanFactory.java:455) ~[com.example.sleuthnativemissinghint.SleuthNativeMissin
gHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1808) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:620) ~[com.example.sleuthnativemissinghint.SleuthNativeMissingHintApplication:5.3.21]
        ... 15 common frames omitted

```