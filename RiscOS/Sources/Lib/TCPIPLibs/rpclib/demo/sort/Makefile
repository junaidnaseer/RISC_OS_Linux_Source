# Copyright 1997 Acorn Computers Ltd
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
#
# @(#)Makefile	1.4 87/11/30 3.9 RPCSRC
#

BIN =  rsort sort_svc
GEN = sort_clnt.c sort_svc.c sort_xdr.c sort.h
LIB = -lrpclib
RPCCOM = rpcgen

all: $(BIN)

rsort: rsort.o sort_clnt.o sort_xdr.o
	$(CC) $(LDFLAGS) -o $@ rsort.o sort_clnt.o sort_xdr.o $(LIB)

rsort.o: rsort.c sort.h

sort_clnt.c:
	$(RPCCOM) -l sort.x >$@

sort_svc: sort_proc.o sort_svc.o sort_xdr.o
	$(CC) $(LDFLAGS) -o $@ sort_proc.o sort_svc.o sort_xdr.o $(LIB)

sort_proc.o: sort_proc.c sort.h

sort_svc.c:
	$(RPCCOM) -s udp sort.x >$@

sort_xdr.c:
	$(RPCCOM) -c sort.x >$@

sort.h:
	$(RPCCOM) -h sort.x >$@

clean cleanup:
	rm -f $(GEN) *.o $(BIN)

