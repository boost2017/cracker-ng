
CXX     = g++
#CXX     = callcatcher g++
#CFLAGS  = -O0 -g
CFLAGS  = -march=native -O3 -mmmx -msse -msse2 -msse3 -m3dnow -ffast-math -mno-ieee-fp -s -D_FILE_OFFSET_BITS=64
CFLAGS += -Wfatal-errors -Werror -Wall -W -pedantic -Wextra -Wunused -Wformat=2 -Weffc++ -Wpadded -fexceptions
LDLIBS  = -lpthread
#LDLIBS += -lcurses
CPTOBJ  = cptfunctions.o rijndael.o tables.o stats.o gui.o cptcracker.o cptmain.o
ZIPOBJ  = zipfunctions.o stats.o zipgui.o read.o puff.o zipcracker.o zipmain.o
NAME    = cracker-ng

all: $(NAME)

clean:
	rm -f *.o

mrproper: clean
	rm -f cptcracker-ng

#$(NAME): $(OBJ)
#	$(CXX) $(CFLAGS) -o $@ $^ $(LDLIBS)

#%.o: %.cc
#	$(CXX) $(CFLAGS) -c $*.cc -DZIP


# Modules availables
cpt: $(CPTOBJ)
	$(CXX) $(CFLAGS) -o $@$(NAME) $^ $(LDLIBS)

zip: $(ZIPOBJ)
	$(CXX) $(CFLAGS) -o $@$(NAME) $^ $(LDLIBS)


# Shared objects
gui.o: shared/gui.cc shared/gui.h
	$(CXX) $(CFLAGS) -c shared/$*.cc

stats.o: shared/stats.cc shared/stats.h
	$(CXX) $(CFLAGS) -c shared/$*.cc


# CPT module objects
cptcracker.o: shared/cracker.cc shared/cracker.h
	$(CXX) $(CFLAGS) -c shared/cracker.cc -o cptcracker.o -DCPT

cptfunctions.o: shared/functions.cc shared/functions.h
	$(CXX) $(CFLAGS) -c shared/functions.cc -o cptfunctions.o -DCPT

cptmain.o: main.cc main.h
	$(CXX) $(CFLAGS) -c main.cc -o cptmain.o -DCPT

rijndael.o: cpt/rijndael.cc cpt/rijndael.h
	$(CXX) $(CFLAGS) -c cpt/$*.cc

tables.o: cpt/tables.cc cpt/tables.h
	$(CXX) $(CFLAGS) -c cpt/$*.cc


# ZIP module objects
puff.o: zip/puff.cc zip/puff.h
	$(CXX) $(CFLAGS) -c zip/$*.cc

read.o: zip/read.cc zip/read.h
	$(CXX) $(CFLAGS) -c zip/$*.cc

zipcracker.o: shared/cracker.cc shared/cracker.h
	$(CXX) $(CFLAGS) -c shared/cracker.cc -o zipcracker.o -DZIP

zipfunctions.o: shared/functions.cc shared/functions.h
	$(CXX) $(CFLAGS) -c shared/functions.cc -o zipfunctions.o -DZIP

zipgui.o: shared/gui.cc shared/gui.h
	$(CXX) $(CFLAGS) -c shared/gui.cc -o zipgui.o -DZIP

zipmain.o: main.cc main.h
	$(CXX) $(CFLAGS) -c main.cc -o zipmain.o -DZIP
