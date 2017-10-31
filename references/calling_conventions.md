## General Calling Conventions

|      Convention Name       |  Stack Cleanup  |  Parameters                   |
|:---------------------------|:----------------|:------------------------------|
| cdecl                      | caller          | on stack in reverse order     |
| stdcall                    | callee          | on stack in reverse order     |
| fastcall                   | callee          | in registers (ECX, EDX) then on stack in reverse order |
| thiscall                   | callee          | on stack in reverse order; this pointer in ECX |
| Microsoft x64              | caller          | in registers (RCX, RDX, R8, R9) then on stack in reverse order |
| System V AMD64 ABI         | caller          | in registers (RDI, RSI, RDX, RCX, R8, R9) then on stack in reverse order |
| System V AMD64 API Syscall | N/A             | in registers (RDI, RSI, RDX, R10, R8, R9) syscall number in RAX |

## Windows Syscall Calling Conventions
### 32 Bit
#### 32 Bit Modern
The `ntdll` exported function for 32 bit syscalls in modern windows operating
systems looks as follows.

```
mov eax,<syscall_index>
mov edx,0x7ffe0300
call dword [edx]
ret <arg_byte_count>
```

This includes XP -> Windows 7. Notice the hard coded `0x7ffe0300`. This calling
convention bounces off a kernel provided page in memory which points to either
`ntdll.KiFastSystemCall`

```
mov edx, esp
sysenter
ret
```

or ntdll.KiIntSystemCall.

```
lea edx, [esp + 8]
int 0x2e
ret
```

This was done originally to support the introduction of the new "sysenter" instruction which was considerably faster, but not backward compatible with older hardware...

#### 32 Bit Legacy
There was an older syscall convention which used the int 0x2e directly.

### 64 Bit
64 bit platforms have the advantage of not needing to support a legacy hardware-provided syscall interface. So you get the nice simple
```
mov r10, rcx
mov rax, <syscall_index>
syscall
ret
```
### SysWow64
For 32 bit binaries running on a 64bit system, there is a little crazyness... Basically, a special field in the TEB (at offset 0xc0 called Wow32Reserved) is populated (normally it is NULL) with a pointer to special transition code (using a code-segment switching farcall) which prepares a 64bit syscall from the 32bit arguments and carries out the syscall from 64bit mode....
```
mov eax, <syscall_index>
xor ecx,ecx
lea edx, [esp + 4]
call [fs:WOW32RESERVED]
add esp,4
ret <arg_byte_count>
```
Once the syscall is complete, it transitions back into 32 bit mode and returns to the add esp...
