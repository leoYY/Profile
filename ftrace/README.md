# ftrace  
### ftrace介绍
ftrace 自linux2.6.27版本集成到内核中, 相比dtrace, systemtap使用上相对简单, 但是依然很强大  

ftrace继承了linux一切皆文件的传统，相关使用接口均可通过挂在debugfs文件系统，进行操作

    mount -t debugfs nodev /sys/kernel/debug  

ftrace功能开关

    echo 1 > /proc/sys/kernel/ftrace_enabled

### ftrace相关接口文件介绍  

#### ./tracing/current_tracer  
用于设置/展现当前配置的tracer，默认是nop

#### ./tracing/available_tracers  
展示当前内核支持的tracer列表

#### ./tracing/trace  
存储trace结果数据

#### (待补充)
