a.out: parsetest.o y.tab.o lex.yy.o errormsg.o symbol.o absyn.o prabsyn.o table.o util.o
	cc -g parsetest.o y.tab.o lex.yy.o symbol.o absyn.o prabsyn.o table.o errormsg.o util.o

parsetest.o: parsetest.c errormsg.h symbol.h absyn.h util.h
	cc -g -c parsetest.c

prabsyn.o: prabsyn.h prabsyn.c symbol.h absyn.h util.h
	cc -g -c prabsyn.c

symbol.o: symbol.h symbol.c table.h util.h
	cc -g -c symbol.c

table.o: table.h table.c util.h
	cc -g -c table.c

absyn.o: absyn.h absyn.c util.h
	cc -g -c absyn.c

y.tab.o: y.tab.c
	cc -g -c y.tab.c

y.tab.c: tiger.grm
	yacc -dv tiger.grm

y.tab.h: y.tab.c
	echo "y.tab.h was created at the same time as y.tab.c"

errormsg.o: errormsg.c errormsg.h util.h
	cc -g -c errormsg.c

lex.yy.o: lex.yy.c y.tab.h errormsg.h util.h
	cc -g -c lex.yy.c

lex.yy.c: tiger.lex
	lex tiger.lex

util.o: util.c util.h
	cc -g -c util.c

clean: 
	rm -f a.out *.o y.tab.* lex.yy.c y.output

all-tests := $(addsuffix .test, $(notdir $(basename $(wildcard ../testcases/*.tig))))

test: $(all-tests)

test49.test:
	@echo "Skip test49.tig"

%.test: ../testcases/%.tig
	mkdir -p testoutput
	./a.out $< > testoutput/$@
