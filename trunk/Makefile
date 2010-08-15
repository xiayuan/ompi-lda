CC=g++
MPICC=mpicxx

CFLAGS=-O3 -Wall -Wno-sign-compare -fopenmp -I/Users/wangyi/3rd-party/boost-1.43.0/include
LDFLAGS=-L/Users/wangyi/3rd-party/boost-1.43.0/lib -lboost_program_options

BUILD_TARGETS=lda infer mpi_lda


all: $(BUILD_TARGETS)

cmd_flags.o: cmd_flags.cc cmd_flags.hh
	$(CC) -c $(CFLAGS)  cmd_flags.cc -o cmd_flags.o

common.o: common.cc common.hh
	$(CC) -c $(CFLAGS)  common.cc -o common.o

document.o: document.cc document.hh common.o
	$(CC) -c $(CFLAGS)  document.cc -o document.o

model.o: model.cc model.hh common.o
	$(CC) -c $(CFLAGS)  model.cc -o model.o

accumulative_model.o: accumulative_model.cc accumulative_model.hh common.o model.o
	$(CC) -c $(CFLAGS)  accumulative_model.cc -o accumulative_model.o

sampler.o: sampler.cc sampler.hh common.o document.o model.o accumulative_model.o
	$(CC) -c $(CFLAGS)  sampler.cc -o sampler.o

lda: lda.cc cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o
	$(CC) $(CFLAGS) lda.cc cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o -o lda $(LDFLAGS)

infer: infer.cc cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o
	$(CC) $(CFLAGS) infer.cc cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o -o infer $(LDFLAGS)

mpi_lda: mpi_lda.cc cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o
	$(MPICC) $(CFLAGS) mpi_lda.cc cmd_flags.o common.o document.o model.o accumulative_model.o sampler.o -o mpi_lda $(LDFLAGS)

clean :
	rm -rf $(BUILD_TARGETS) *_test *.o *.a *.exe *~ *.stackdump *.core *.dSYM
