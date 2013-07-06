ec2-automation
==============

Scripts for automating Amazon EC2 instance creation / bootstrapping for coursera startup class.

Setup
-----

1. At first add several additional environment variables to your ~/.bash_profile:
```sh
export EC2_AMI=ami-70f96e40 # AMI type used for the startup class
export EC2_TYPE=t1.micro
export EC2_REGION=us-west-2
export DEV_SSH_KEY=/path/to/dev/key
```
$DEV_SSH_KEY should be registered on heroku and github.
For additional AMI types you can check [this link](http://cloud-images.ubuntu.com/releases/precise/release-20130411.1/).

2. Then setup [EC2 API Tools](http://aws.amazon.com/developertools/351) on your local machine as described 
[here](http://www.robertsosinski.com/2008/01/26/starting-amazon-ec2-with-mac-os-x/).

3. Put scripts from this repo to some directory included in $PATH variable, so you can run them from anywhere.

Done. Now creation, starting, bootstrapping and stopping of EC2 instances for [startup class](https://class.coursera.org/startup-001/)
is fully automated [and takes now about 5 minutes].

How To
------
* Start+bootstrap: **ecstart**.
This script creates EC2 instance, starts it and then runs [bootstrap script](https://github.com/mvkvl/startup/blob/master/bootstrap.sh)
 on this instance.

<pre>
$ ecstart
...
...
EC2 instance i-abcdef12 is up and running
connect to it with:
ssh -i ~/.ec2/ec2-keypair ubuntu@w.x.y.z
</pre>

* List running instances: **eclist**

<pre>
$ eclist
i-abc12def  t1.micro  a.b.c.d
i-fed21cba  t1.micro  e.f.g.h
</pre>

* Stop running instance(s): **ecstop**

<pre>
stop defined instance(s)
$ ecstop i-abc12def i-fed21cba

stop all instances
$ ecstop
</pre>

* SSH to running instance: **ecssh**

<pre>
$ ecssh i-12345678
</pre>
