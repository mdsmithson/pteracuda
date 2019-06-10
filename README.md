# pteracuda
Framework for using CUDA from Erlang
Forked from Kevin Smith on 6/9/2019

fixed some issues in pcuda_ops.cu

Testing done on an Ubuntu 18.04 machine: <br>
With a Hexacore i7-3930k, GTX 1070, 16GB DDR3 and a 256SSD Harddrive.<br>
Erlang/OTP 22<br>
Cuda 10.1<br>


Installing:<br>
<br>
1. update the rebar.config to your specific GPU architecture and compilation tool kit folders
2. rebar compile, erl make and start application<br>
~/pteracuda/$ rebar compile<br>
~/pteracuda/$ cd src<br>
~/pteracuda/src$ erl -make<br>
~/pteracuda/src$ cd .. && cd ebin<br>

Application:<br>

A. Test on Erlang/OTP 22<br> 
~/pteracuda/ebin$ erl<br>
Erlang/OTP 22 [erts-10.4.1] [source] [64-bit] [smp:12:12] [ds:12:12:10] [async-threads:1]<br>
Eshell V10.4.1  (abort with ^G)<br>
1> application:start(pteracuda).<br>
ok<br>
2> pteracuda_demo:start(1000000).<br>
Generating test data: 1000000<br>
Measuring performance ..<br>
Erlang: 493.407ms, CUDA: 85.507ms<br>
ok<br>
<br>
B. Test on Elixir 1.8.1<br>
~/pteracuda/ebin$ iex<br>
iex(1)> Application.start(:pteracuda,:temporary)<br>
iex(2)> :pteracuda_demo.start(1000000)<br>
Generating test data: 1000000<br>
Measuring performance ..<br>
Erlang: 492.822ms, CUDA: 84.252ms<br>
:ok
