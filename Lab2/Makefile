CC = gcc
CXX = gcpc
CFLAGS = -Wall -std=gnu99 -openmp -O2 -g -I.
CFLAGS_DEBUG = -Wall -std=gnu99 -openmp -O0 -g -I.
CXXFLAGS = -Wall -openmp -O3 -g
#overkill on the flags, but that doesn't hurt anything
#add current dir to libs for libjsmn.a
LDFLAGS = -lrt -lpthread -L. 
#replace this if you want to change the output name
CTARGET = palindrome
TEX_TARGET = writeup

ASSIGNMENT_NAME = cs472_LAB2_bridgewd_philliry

# LaTeX related constants
HTML=main_html
SRC=

#any headers go here
INCLUDES = 

#any .c or .cpp files go here
SOURCE = lab2_part2/palindrome.c

#default is to compile and pdf
default: compile both
both: pdf html
	
#depends on all of you source and header files
compile: ${SOURCE} ${INCLUDES}
#this assumes you actually are linking all of the source files together
	${CC} ${CFLAGS} ${SOURCE} -o ${CTARGET} ${LDFLAGS}

debug: ${SOURCE} ${INCLUDES}
	${CC} ${CFLAGS_DEBUG} ${SOURCE} -o ${CTARGET} ${LDFLAGS} -DDEBUG

dvi: ${TEX_TARGET}.tex
#	pygmentize the input source file -- THIS NAME SHOULD BE SAFE
#	pygmentize -f latex -o __${SRC}.tex ${SRC}
#	run latex twice to get references correct
	latex ${TEX_TARGET}.tex
#	you can also have a bibtex line here
#	bibtex $(TEX_TARGET).tex
	latex $(TEX_TARGET).tex
#	remove the pygmentized output to avoid cluttering up the directory
#	rm __${SRC}.tex

ps: dvi
	dvips -R -Poutline -t letter ${TEX_TARGET}.dvi -o ${TEX_TARGET}.ps

pdf: ps
	ps2pdf ${TEX_TARGET}.ps


html:
	cp ${TEX_TARGET}.tex ${HTML}.tex
	latex ${HTML}.tex
	latex2html -split 0 -noshow_section_numbers -local_icons -no_navigation -noinfo -noaddress ${HTML}

	sed 's/<BR><HR>//g' < ${HTML}/index.html > ${HTML}/index2.html
	mv ${HTML}/index2.html ${TEX_TARGET}.html
	rm ${HTML}.*
	rm -rf ${HTML}
	
run: 
	$(info ************************RUNNING********************************)
	./$(TARGET) 

tar:
	tar cvf $(ASSIGNMENT_NAME).tar.bz2 $(TEX_TARGET).tex  Makefile \
		$(SOURCE) pygments.tex lab2_part1/*.asm  lab2_part2/*.asm \
		*.pdf


clean:
	rm ${TEX_TARGET}.dvi ${TEX_TARGET}.log ${TEX_TARGET}.out ${TEX_TARGET}.ps ${TEX_TARGET}.aux ${TEX_TARGET}.pdf ${CTARGET}
