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