# AWS CloudFormation template for a EC2 with Erlang and Ubuntu 18.04

This is an example of cloudFormation template for Amazon EC2 running Ubuntu 18.04 LTS with Erlang OTP23. It implements the following sequence:

 * Create EC2 ubuntu 18.04 with ports 22 and 80 open
 * Install nginx to redirect port 80 <-> 8080;
 * Install Erlang dependencies;
 * Install Rebar3;
 * Install Erlang;
 * Clone erlang example project and make a release;
 * Install init.d file to start the Erlang project automatically when booting;
 * Reboot to conclude all installation

## Connecting nodes

If you want to connect with Erlang node outside the internal network:

```
erl -name test@localhost -setcookie "ebanx_cookie"
```
Now, you should add the node from AWS using the external IP

```erlang
Erlang/OTP 23 [erts-11.0.3] [source] [64-bit] [smp:8:8] [ds:8:8:10] [async-threads:1]

Eshell V11.0.3  (abort with ^G)
(test@localhost)1> nodes().
[]
(test@localhost)2> net_kernel:connect_node('ebanx@X.X.X.X').
true
(test@localhost)3> nodes().
['ebanx@X.X.X.X']
% CTRL+G
(test@localhost)4>
User switch command
 --> h
  c [nn]            - connect to job
  i [nn]            - interrupt job
  k [nn]            - kill job
  j                 - list all jobs
  s [shell]         - start local shell
  r [node [shell]]  - start remote shell
  q                 - quit erlang
  ? | h             - this message
 --> r 'ebanx@X.X.X.X'
 --> j
   1  {shell,start,[init]}
   2* {'ebanx@X.X.X.X',shell,start,[]}
 --> c 2
% Now you are in shell running in the remote node
Eshell V11.1  (abort with ^G)
(ebanx@X.X.X.X)1> whereis(ebanx_sup).
<0.461.0>
(ebanx@X.X.X.X)2>
```

## PS: It is important to write down that Distributed Erlang isn't secure and should not be used outside of trusted local area network

