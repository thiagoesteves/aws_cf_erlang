# AWS CloudFormation template for a EC2 with Erlang and Ubuntu 18.04

This is an example of cloudFormation template for Amazon EC2 running Ubuntu 18.04 LTS with Erlang OTP23. It implements the following sequence:

 * Create EC2 ubuntu 18.04 with ports 22 and 80 open
 * Install nginx to redirect port 80 <-> 8080;
 * Install Erlang dependencies;
 * Install Rebar3;
 * Install Erlang;
 * Clone erlang example project and make a release;
 * Install init.d file to start the Erlang project automatically;
 * Reboot to conclude all installation

