## General Calling Conventions

|      Convention Name       |  Stack Cleanup  |  Parameters  |
|:---------------------------|:----------------|:-------------|
| cdecl                      | caller          | on stack in reverse order |
| stdcall                    | callee          | on stack in reverse order |
| fastcall                   | callee          | in registers (ECX, EDX) then on stack in reverse order |
| thiscall                   | callee          | on stack in reverse order; this pointer in ECX |
| Microsoft x64              | caller          | in registers (RCX, RDX, R8, R9) then on stack in reverse order |
| System V AMD64 ABI         | caller          | in registers (RDI, RSI, RDX, RCX, R8, R9) then on stack in reverse order |
| System V AMD64 API Syscall | N/A             | in registers (RDI, RSI, RDX, R10, R8, R9) syscall number in RAX |
