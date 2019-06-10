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

A. Test on Erlang/OTP 22<br><br>
~/pteracuda/ebin$ erl<br>
Erlang/OTP 22 [erts-10.4.1] [source] [64-bit] [smp:12:12] [ds:12:12:10] [async-threads:1]<br>
Eshell V10.4.1  (abort with ^G)<br>
```erlang
application:start(pteracuda)
pteracuda_demo:start(1000000)
```
Generating test data: 1000000<br>
Measuring performance ..<br>
Erlang: 493.407ms, CUDA: 85.507ms<br>
ok<br>
<br>
B. Test on Elixir 1.8.1<br><br>
~/pteracuda/ebin$ iex<br>
```elixir
Application.start(:pteracuda,:temporary)
# :pteracuda_demo.start(1000000)

list = for _ <- 0..10000000, do: :random.uniform(10000000)
 cudasort = fn x -> 
  {:ok, c} = :pteracuda_context.new()
  {:ok, b} = :pteracuda_buffer.new(:integer)
  :pteracuda_buffer.write(b,x)
  :pteracuda_buffer.sort(c,b)
  :pteracuda_buffer.read(b)|>elem(1) 
 end
 list |> cudasort.() 
 # Benchmark
 fn -> cudasort.(c,b,list) end |> :timer.tc |> elem(0) |> Kernel./(1000)
 # 883.162
 fn -> list |> Enum.sort end |> :timer.tc |> elem(0) |> Kernel./(1000)
 # 4845.561

```

