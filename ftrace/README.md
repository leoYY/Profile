# ftrace  

ftrace 自linux2.6.27版本集成到内核中, 相比dtrace, systemtap使用上相对简单, 但是依然很强大  

目前2.6.32支持的tracer有 blk kmemtrace function_graph wakeup_rt wakeup function sysprof sched_switch initcall nop(./tracing/available_traces)
