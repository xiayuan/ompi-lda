# Copyright 2010 Yi Wang (yi.wang.2005@gmail.com)
#
# This Makefile builds both lda (single-node training program) and
# mpi-lda (multi-node training program) with OpenMP feature.
#
# To invoke this Makefile:
#   > make clean && make
#
# If you do NOT want OpenMP, just remove -fopenmp from the rest part
# of this file.
#
# If you want to use other compilers instead of GCC/G++, just redefine
# CC and CXX in following lines.  You may want to consult
# http://openmp.org/wp/openmp-compilers/ for compilers that support
# OpenMP.

BUILD_TARGETS=lda infer mpi_lda

CC=g++
CXX=g++
MPICXX=mpicxx

CFLAGS=-O3 -Wall -Wextra -Wno-sign-compare -fopenmp -I/Users/wangyi/3rd-party/boost-1.43.0/include
LDFLAGS=-fopenmp
LDLIBS=-L/Users/wangyi/3rd-party/boost-1.43.0/lib -lboost_program_options

all: $(BUILD_TARGETS)

%.o:%.cc
	$(CXX) $(CFLAGS) $(CXXFLAGS) -c $< -o $@

lda: lda.o sampler.o document.o model.o accumulative_model.o cmd_flags.o common.o

infer: infer.o cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o

mpi_lda: mpi_lda.o cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o
	$(MPICXX) $(LDFLAGS) -o $@ $^ $(LDLIBS)

clean :
	rm -rf $(BUILD_TARGETS) *_test *.o *.a *.exe *~ *.stackdump *.core *.dSYM .depend

.depend: depend

depend: *.cc
	rm -f ./.depend
	$(CC) $(CFLAGS) -MM $^>>./.depend;

include .depend
