# pteracuda
Framework for using CUDA from Erlang
Forked from Kevin Smith on 6/9/2019

fixed some issues in pcuda_ops.cu

Testing done on Ubuntu 18.04 GTX 1070 i7-3930k 16GB 256SSD
Erlang/OTP 22
Cuda 10.1

Installing:

1. update the rebar.config to your specific GPU architecture and compilation tool kit folders
2. rebar compile, erl make and start application<br>
~/pteracuda/$ rebar compile<br>
~/pteracuda/$ cd src<br>
~/pteracuda/src$ erl -make<br>
~/pteracuda/src$ cd .. && cd ebin<br>
~/pteracuda/ebin$ erl<br>
Erlang/OTP 22 [erts-10.4.1] [source] [64-bit] [smp:12:12] [ds:12:12:10] [async-threads:1]<br>
Eshell V10.4.1  (abort with ^G)<br>
1> application:start(pteracuda).<br>
ok<br>
