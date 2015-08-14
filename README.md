# Perf_Common_Settings

GC log settings:  
Edit in run.conf file:

> timestamp=$( date +%Y-%m-%d_%H%M%S )  
> …  
> -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:/opt/jboss/server/default/log/gc-$timestamp.log
