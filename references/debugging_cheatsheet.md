# Debugger Cheat Sheet

## Windbg

### Switch context from the kernel to a process
!process -0 0
.process /r /p [PROCESS ID]

### Watch for kernel pool allocations
```
ba e 1 nt!ExAllocatePoolWithTag ".printf \"ExAllocatePoolWithTag(PoolType=%N, NumberOfBytes=%N, Tag=%N)\\n\", poi(esp+4),poi(esp+8),poi(esp+c); g"
ba e 1 nt!ExFreePoolWithTag ".printf \"ExFreePoolWithTag(P=%N, Tag=%N)\\n\", poi(esp+4),poi(esp+8); g"
```

### Show a handle object
```
dt win32k!_handleentry poi(win32k!gSharedInfo+$ptrsize)+@@(sizeof(win32k!_handleentry))*0x1234
```
