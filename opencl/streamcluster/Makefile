include ../../common/make.config

#Can be changed by `make TYPE=CPU`
TYPE = GPU

#Library
ifeq ($(TYPE),GPU)
	OPENCL_INC = /usr/local/cuda/include
	OPENCL_LIB = /usr/local/cuda/lib64
else
	OPENCL_INC = $(INTEL_OPENCL_INC)
	OPENCL_LIB = $(INTEL_OPENCL_LIB)
endif


#C compiler
CC = g++


FLAGS = -O3
SRC = streamcluster.cpp ../util/timing.c
EXE = streamcluster.out

release:$(SRC)
	$(CC) $(SRC) -o $(EXE) \
		-I$(OPENCL_INC) -L$(OPENCL_LIB)	$(FLAGS) -lOpenCL \
		-I../util -DTIMING

errmsg:$(SRC)
	$(CC) -lOpenCL $(SRC) -o $(EXE) -I$(OPENCL_INC) -L$(OPENCL_LIB) -D ERRMSG $(FLAGS)
	
ptx:$(SRC)
	$(CC) -lOpenCL $(SRC) -o $(EXE) -I$(OPENCL_INC) -L$(OPENCL_LIB) -D PTX_MSG $(FLAGS)
	
res:$(SRC)
	$(CC) -lOpenCL $(SRC) -o $(EXE) -I$(OPENCL_INC) -L$(OPENCL_LIB) -D RES_MSG $(FLAGS)

run:
	./streamcluster.out 10 20 256 65536 65536 1000 none output.txt 1 -p 0 -d 0
	
clean: $(SRC)
	rm -f $(EXE) $(EXE).linkinfo result*
