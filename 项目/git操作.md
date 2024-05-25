## git基础教程

>[30分钟弄懂所有工作Git必备操作 / Git 入门教程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1pX4y1S7Dq/?spm_id_from=333.337.search-card.all.click&vd_source=81d07727a431bd6b2d07b94e67a294fc)

## vscode基本配置

>[vscode 搭建 C/C++ 编译环境教程（windows） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/643934671)

## launch.jason

```c
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "gcc.exe - 生成和调试活动文件",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\output\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "C:/MinGW/bin",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "E:\\mingw64\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: gcc.exe 生成活动文件"
        }
    ]
}
```

## task.json

```c
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: gcc.exe 生成活动文件",
            "command": "E://mingw64/bin/gcc.exe",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\output\\${fileBasenameNoExtension}.exe",
                "-fexec-charset=GBK"
            ],
            "options": {
                "cwd": "E://mingw64/bin"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ],
    "version": "2.0.0"
}
```

ssh  kumorio@192.168.112.128

## vscode 调试xv6

>[从零开始使用Vscode调试XV6 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/501901665)

### vscode xv6 launch文件

>```json
>// xv6-riscv/.vscode/launch.json
>{
>    "version": "0.2.0",
>    "configurations": [
>        {
>            "name": "xv6debug",
>            "type": "cppdbg",
>            "request": "launch",
>            "program": "${workspaceFolder}/kernel/kernel",
>            "stopAtEntry": true,
>            "cwd": "${workspaceFolder}",
>            "miDebuggerServerAddress": "127.0.0.1:26000", //见.gdbinit 中 target remote xxxx:xx
>            "miDebuggerPath": "/usr/bin/gdb-multiarch", // which gdb-multiarch
>            "MIMode": "gdb",
>            "preLaunchTask": "xv6build"
>        }
>    ]
>}
>```

### vscode xv6 task文件

>```json
>// xv6-riscv/.vscode/tasks.json
>{
>    "version": "2.0.0",
>    "tasks": [
>        {
>            "label": "xv6build",
>            "type": "shell",
>            "isBackground": true,
>            "command": "make qemu-gdb",
>            "problemMatcher": [
>                {
>                    "pattern": [
>                        {
>                            "regexp": ".",
>                            "file": 1,
>                            "location": 2,
>                            "message": 3
>                        }
>                    ],
>                    "background": {
>                        "beginsPattern": ".*Now run 'gdb' in another window.",
>                        // 要对应编译成功后,一句echo的内容. 此处对应 Makefile Line:170
>                        "endsPattern": "."
>                    }
>                }
>            ]
>        }
>    ]
>}
>```
