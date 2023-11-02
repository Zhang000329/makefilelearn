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