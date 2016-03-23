## Clustering

### Building a cluster (in order of best to worst options):

* You don't need a linux cluster.  Maybe you only need lots of storage.  Maybe you only need high availability.
* Use the one you already have at work or school. 
* Buy one from [Advanced Clustering Technologies](www.advancedclustering.com).  You will still need at least a minimal linux administrator but ACT has great hardware at a great price and delivers great support. 
* Setup a Rocks cluster with existing PC machinery with [Rocks](www.rocksclusters.org).  You will need a medium tier linux administrator but this is a great cluster kit and will come with all of the bells and whistles.  Using Rocks lets them do alot of the work for you.  The main benefit of Rocks is the **easy** thing.
* Setup a custom cluster using PC hardware and a switch.  You will need a good linux administrator.  If you insist on certain attributes (must run Suse, must have lustre, must must must), you might need to build it yourself.  Good linux administrators might prefer the custom built route. 
* Setup a cluster on Google Compute.  These are (circa Spring 2016) not clusterable except at a very long distance.  Each VM is roughly unrelated to other VMs that you start.  Potentially high costs in terms of administrative skills and experience.  Google Compute is nice because its out there on the cloud and is Google's problem.  The performance, flexibility and future is very bright with Google Compute.  
* Setup a cluster on Amazon.  This option is very attractive if you have an AWS expert on hand that won't be leaving soon.  With AWS expertise, extremely flexible clustering and extremely competitive pricing is yours.  You can turn on 900 CPUs for two days, use it, turn it off.  That means you have a giant cluster and you only paid a hundred bucks.  By design, AWS setup is **roughly** self documenting.  Therefore, you get your cluster documented as you build it.  This is the best clustering option available but, because of the rarity of competent AWS administration, you should forget it. 

### Benchmarking

The stuff you already have on your machine are the best tools: top, htop, iotop, bonnie, pv, dd, time, ganglia, nagios, df, dmesg, iostat, 

See [OpenMP programming, compilation, execution, benchmarking in C++ on linux](/software/c) for a benchmarking example you can try yourself. 
