CC :=aarch64-linux-gnu-gcc
SRC :=$(shell find src -name "*.c")
INC :=./inc \
	./3rd/usr/local/include \
	./3rd/usr/include \
	./3rd/usr/include/python3.10 \
	./3rd/usr/include/aarch64-linux-gnu/python3.10 \
	./3rd/usr/include/aarch64-linux-gnu


#字符串替换函数，将SRC中的src/替换成obj/
OBJ :=$(subst src/,obj/,$(SRC:.c=.o))


TARGET=obj/garbage
#$(foreach VAR,LIST,TEXT)把LIST中的元素依次取出赋值给VAR在执行TEST函数
CFLAGS :=$(foreach item,$(INC),-I$(item)) # -I./inc -I./3rd/usr/local/include
LIBS_PATH := ./3rd/usr/local/lib \
			 ./3rd/lib/aarch64-linux-gnu \
			 ./3rd/usr/lib/aarch64-linux-gnu \
			 ./3rd/usr/lib/python3.10

LDFLAGS := $(foreach item, $(LIBS_PATH),-L$(item)) # -L./3rd/usr/local/libs

LIBS := -lwiringPi -lpython3.10 -pthread -lexpat -lz -lcrypt

obj/%.o:src/%.c
	mkdir -p obj
	$(CC) -o $@ -c $< $(CFLAGS)

$(TARGET) :$(OBJ)
	$(CC) -o $@ $^ $(CFLAGS) $(LDFLAGS) $(LIBS)

compile: $(TARGET)


debug:
	echo $(CC)
	echo $(SRC)
	echo $(INC)
	echo $(OBJ)
	echo $(TARGET)
	echo $(CFLAGS)
	echo $(LDFLAGS)
	echo $(LIBS)

clean: 
	rm $(TARGET) obj $(OBJ) -rf


.PHONY:clean compile debug

