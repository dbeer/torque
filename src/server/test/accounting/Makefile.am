PROG_ROOT = ../..

AM_CFLAGS = -g -DTEST_FUNCTION -I$(PROG_ROOT)/ -I$(PROG_ROOT)/../include/ --coverage 

lib_LTLIBRARIES = libaccounting.la

AM_LDFLAGS = @CHECK_LIBS@ $(lib_LTLIBRARIES)

check_PROGRAMS = test_accounting

libaccounting_la_SOURCES = scaffolding.c $(PROG_ROOT)/accounting.c
libaccounting_la_LDFLAGS = @CHECK_LIBS@ -shared -lgcov  

test_accounting_SOURCES = test_accounting.c

check_SCRIPTS = coverage_run.sh

TESTS = $(check_PROGRAMS) coverage_run.sh

coverage_run.sh:
	echo 'cp -p .libs/accounting.gc* . >/dev/null 2>&1' > $@
	echo 'RESULTS=($$(gcov accounting.gcda))' >> $@
	echo 'PARSED_RESULT="TOTALCOV -- $${RESULTS[1]}: Lines($${RESULTS[5]})- $${RESULTS[3]}"' >> $@
	echo 'echo -e "\033[40m\033[1;33m$$PARSED_RESULT\033[0m"' >> $@
	chmod +x $@

CLEANFILES = coverage_run.sh *.gcno *.gcda *.gcov core *.lo
