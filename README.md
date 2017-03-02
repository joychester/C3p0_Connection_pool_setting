# Perf_Common_Settings

## GC log settings:  
Edit in run.conf file:

> timestamp=$( date +%Y-%m-%d_%H%M%S )  
> …  
> -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:/opt/jboss/server/default/log/gc-$timestamp.log

## C3p0 common settings:  
> c3p0.acquireIncrement=5  
> c3p0.minPoolSize=15  
> c3p0.maxPoolSize=200  
> c3p0.maxStatementsPerConnection=100  
> c3p0.maxIdleTime=7200  
> c3p0.preferredTestQuery=select 1 from dual  
> c3p0.idleConnectionTestPeriod=30  
> c3p0.testConnectionOnCheckin=true  
> c3p0.unreturnedConnectionTimeout=60  
> c3p0.checkoutTimeout=60000  

## G1 GC Collector Settings(JDK7_55):  
> -server  
> -XX:+UseG1GC  
> -Xms6144m  
> -Xmx6144m  
> -XX:MaxPermSize=256m  
> -XX:InitiatingHeapOccupancyPercent=55  
> -XX:MaxGCPauseMillis=200  
> -XX:+ParallelRefProcEnabled  

> -XX:+UseStringDeduplication after JDK8_20

## CMS GC Collector Settings with Normal heap size(JDK7_55):  
> -server  
> -Xms4096m  
> -Xmx4096m  
> -XX:NewRatio=2  
> -XX:+CMSClassUnloadingEnabled  
> -XX:+DisableExplicitGC  
> -XX:+UseConcMarkSweepGC  
> -XX:+UseParNewGC  
> -XX:MaxPermSize=512m  
> -XX:ReservedCodeCacheSize=96m  
> -XX:CMSInitiatingOccupancyFraction=70  
> -XX:+UseCMSInitiatingOccupancyOnly  
> -XX:+ParallelRefProcEnabled  

## CMS GC Collector Settings with Large heap size and 10 CPU Cores(JDK7_55):   
> -server  
> -Xms24g  
> -Xmx24g  
> -XX:NewRatio=2  
> -XX:+CMSClassUnloadingEnabled  
> -XX:+DisableExplicitGC  
> -XX:+UseConcMarkSweepGC  
> -XX:+UseParNewGC  
> -XX:MaxPermSize=512m  
> -XX:ReservedCodeCacheSize=96m  
> -XX:+UnlockDiagnosticVMOptions  
> -XX:ParGCCardsPerStrideChunk=4096  
> -XX:CMSInitiatingOccupancyFraction=85  
> -XX:+UseCMSInitiatingOccupancyOnly  
> -XX:ParallelGCThreads=16  
> -XX:ConcGCThreads=4 
> -XX:+ParallelRefProcEnabled  

## Check JVM options default value:  
> java -XX:+PrintFlagsFinal  


 > Note: If the weak refs processing is dominate, you might be able to cut that time down by using parallel reference processing (-XX:+ParallelRefProcEnabled).   

## Tomcat JDBC connection pool Config:  
> **Pool sizing properties:** 
  - initialSize  
  - maxActive  
  - maxIdle  
  - minIdle  
  - timeBetweenEvictionRunsMillis  
  - minEvictableIdleTimeMillis  

> **Validate connections properties:**  
  - validationQuery  
  - validationInterval  
  - testOnBorrow  

> **Connection leak prevent properties:**  
  - removeAbandoned  
  - removeAbandonedTimeout  
  - validationQuery  

> **Useful links:**  
[Tomcat CP offical doc](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html#Common_Attributes)  
[A good example for reference](http://www.codingpedia.org/ama/tomcat-jdbc-connection-pool-configuration-for-production-and-development/)
