CXXFLAGS=-O3 -g -DDEBUG_LOG
EXE_NAME=TraceGen

SRC = $(wildcard *.cpp)

OBJ = $(subst LibraryStubs.o,,$(addsuffix .o, $(basename $(SRC))))

REBUILDABLES=$(OBJ) $(EXE_NAME)

all: ${EXE_NAME}

#   $@ target name, $^ target deps, $< matched pattern
$(EXE_NAME): $(OBJ)
	$(CXX) $(LINK_FLAGS) -o $@ $^ 
	@echo "Built $@ successfully" 

#include the autogenerated dependency files for each .o file
-include $(OBJ:.o=.dep)

# build dependency list via gcc -M and save to a .dep file
%.dep : %.cpp
	@$(CXX) -M $(CXXFLAGS) $< > $@

# build all .cpp files to .o files
%.o : %.cpp
	g++ $(CXXFLAGS) -o $@ -c $<

clean: 
	-rm -f ${REBUILDABLES} *.dep 
