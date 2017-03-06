
SHELL = /bin/bash

MD = ./bin/Markdown.pl
FC = ./bin/find_code.pl
PP = ./bin/preppage.pl
INCF = ./bin/inc_file.pl
TOCGEN = ./bin/pyhat.py 
MC = _metacontent


SOURCES = homepage.txt education.txt research.txt software.txt publications.txt contact.txt personal.txt credits.txt

pagefiles=$(SOURCES:.txt=.html)

default: all giveaccess

all: $(pagefiles)

index.txt: Template.txt
	/bin/cp -rf Template.txt index.txt

footbar.pm: footbar
	@$(MD) footbar > footbar.pm

sidebar.pm: sidebar
	@$(MD) sidebar > sidebar.pm

%.s: %.txt
	@cat $*.txt $(MC) > $*.txt2
	@$(FC) < $*.txt2 > $*.s
	@/bin/rm -f *.txt2
	@/bin/rm -f tmp_code_123 tmp_code_1234

%.w: %.s
	@$(MD) $*.s > $*.w

%.html : %.w template footbar.pm sidebar.pm $(MC)
	@$(PP) template sidebar.pm footbar.pm $*.w | $(INCF) > $*.html
	@grep 'table_of_contents' $*.html && python $(TOCGEN) -d. $*.html 2>&1 > /dev/null || echo ""
	@echo $*.html created
	
clean:
	/bin/rm -f $(pagefiles)
	/bin/rm -f footbar.pm sidebar.pm
	
giveaccess:
	chmod -R a+r *

