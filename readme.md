## 编译流程

![img](https://cdn.nlark.com/yuque/0/2023/png/35745066/1699186776482-54066f84-dc94-439a-8632-40dde9f44f80.png)

在我进行编译成可执行文件的时候，我们需要将源文件编译成`.o`文件来进行使用

## 在同一个目录下进行文件的编译

```makefile
cpp_file := ${shell find src -name "*.cpp"}
cpp_objs := $(patsubst src/%.cpp, obj/%.o, $(cpp_file))

obj/%.o : src/%.cpp
	@mkdir -p $(dir $@)
	@g++ -c $^ -o $@

workspace/exec : $(cpp_objs)
	@mkdir -p workspace
	@g++ $^ -o $@

debug:
	@echo ${cpp_file}

clean:
	@rm -rf workspace obj
run : workspace/exec
	@./$<

.PHONY: debug run clean
```

1. 首先对所有cpp文件进行查找，使用内置的`patsubst`对`.o`文件进行指定
2. 进行正常的编译链接

## 编译在不同目录文件夹下的文件

```makefile
cpp_srcs := $(shell find src -name *.cpp)
cpp_objs := $(patsubst src/%.cpp, objs/%.o, $(cpp_srcs))

include_paths := /home/zyj/makefilelearn/chp2/include
I_flag := $(include_paths:%=-I%)

objs/%.o : src/%.cpp
	@mkdir -p $(dir $@)
	@g++ -c $^ -o $@ $(I_flag)

workspace/exec : $(cpp_objs)
	@mkdir -p $(dir  $@)
	@g++ $^ -o $@

run : workspace/exec
	@./$<

debug:
	@echo $(I_flag)

clean:
	@rm -rf objs

.PHONY: debug run clean
```

1. 面对头文件和源文件在不同文件的夹的情况，我们首先需要指定头文件所在的位置（建议使用绝对路径） 
2. 在进行文件编译的时候使用`-I`参数来带上所有的头文件路径