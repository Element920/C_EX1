CC = gcc
AR = ar
CFLAGS = -Wall -g
LDFLAGS = -lm

SRC_DIR = src
OBJ_DIR = obj
LIB_DIR = lib
BIN_DIR = bin

OBJECTS_MAIN = $(OBJ_DIR)/main.o
OBJECTS_BASIC = $(OBJ_DIR)/basicClassification.o
OBJECTS_ADVANCED_LOOP = $(OBJ_DIR)/advancedClassificationLoop.o
OBJECTS_ADVANCED_REC = $(OBJ_DIR)/advancedClassificationRecursion.o
LIB_D_REC = $(LIB_DIR)/libclassrec.so
LIB_S_REC = $(LIB_DIR)/libclassrec.a
LIB_D_LOOP = $(LIB_DIR)/libclassloops.so
LIB_S_LOOP = $(LIB_DIR)/libclassloops.a
EXECUTABLES = $(BIN_DIR)/mains $(BIN_DIR)/maindloop $(BIN_DIR)/maindrec

.PHONY: all clean

all: $(EXECUTABLES)

$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c $< -o $@

$(LIB_S_REC): $(OBJECTS_BASIC) $(OBJECTS_ADVANCED_REC)
	$(AR) -rcs $@ $^

$(LIB_D_REC): $(OBJECTS_BASIC) $(OBJECTS_ADVANCED_REC)
	$(CC) -shared $^ -o $@

$(LIB_S_LOOP): $(OBJECTS_BASIC) $(OBJECTS_ADVANCED_LOOP)
	$(AR) -rcs $@ $^

$(LIB_D_LOOP): $(OBJECTS_BASIC) $(OBJECTS_ADVANCED_LOOP)
	$(CC) -shared $^ -o $@

$(BIN_DIR)/mains: $(OBJECTS_MAIN) $(OBJECTS_BASIC) $(OBJECTS_ADVANCED_REC) $(LIB_S_REC)
	$(CC) $^ -o $@ $(LDFLAGS)

$(BIN_DIR)/maindloop: $(OBJECTS_MAIN) $(LIB_D_LOOP)
	$(CC) $< -L$(LIB_DIR) -lclassloops -o $@ $(LDFLAGS)

$(BIN_DIR)/maindrec: $(OBJECTS_MAIN) $(LIB_D_REC)
	$(CC) $< -L$(LIB_DIR) -lclassrec -o $@ $(LDFLAGS)

clean:
	rm -rf $(OBJ_DIR) $(LIB_DIR) $(BIN_DIR)

-include $(OBJ_DIR)/*.d
