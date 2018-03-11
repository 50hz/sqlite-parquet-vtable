PARQUET_CPP=~/src/parquet-cpp

CC = g++
# odd, no -lz -ldl -lpthread needed?
CFLAGS = -I ../sqlite -O3 -std=c++11 -Wall -fPIC -g
PARQUET_LIB = $(PARQUET_CPP)/build/release/libparquet.a
THRIFT_LIB = $(PARQUET_CPP)/thrift_ep/src/thrift_ep-install/lib/libthrift.a
ARROW_LIB = $(PARQUET_CPP)/build/release/libarrow.so
BOOST_LIB = /usr/lib/x86_64-linux-gnu/libboost_regex.so

LDFLAGS = -O3 $(PARQUET_LIB) $(THRIFT_LIB) $(ARROW_LIB) $(BOOST_LIB)
DEPS = hellomake.h
OBJ = parquet.o parquet_filter.o parquet_table.o parquet_cursor.o

libparquet.so: $(OBJ)
	$(CC) -shared -o $@ $^ $(LDFLAGS)

parquet_filter.o: parquet_filter.cc parquet_filter.h
	$(CC) -c -o $@ $< $(CFLAGS)

parquet_cursor.o: parquet_cursor.cc parquet_cursor.h parquet_table.h parquet_filter.h
	$(CC) -c -o $@ $< $(CFLAGS)

parquet_table.o: parquet_table.cc parquet_table.h
	$(CC) -c -o $@ $< $(CFLAGS)

parquet.o: parquet.cc parquet_cursor.h parquet_table.h parquet_filter.h
	$(CC) -c -o $@ $< $(CFLAGS)

.PHONY: clean

clean:
	rm -f *.o *.so