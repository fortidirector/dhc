distributed health check 2.0+ superawesomenice
=

Summary
--

Distributed Health Check 2.0+ superawesomenice (DHC further) is a cloud aware, horizontally scalable , redundant and highly available resource monitor. Anything that can be connected or discovered via standard networking protocol can also be monitored via DHC. 

At the current release point DHC probes are limited to ....


Architecture
==

DHC architecture is a spike-hub 

HUB is centrally located or geo distributed (later)

SPIKE is a N work nodes that are hosting workers. Each work node discovers its location members via HUBs service discovery API.
The discovery provides location of work queuee to use. TTL for discovery data is N minutes or failure.

Hub
===
Hub is highly available cloud ready REST interface, built on a top of mongodb (or readis TBD) cluster.

The key features to a hub are
---

1. Authenticate requestor 
2. supply job lists / and DIFFs
3. collect URI's performance data
4. serve as service discovery
5. serve as heart beat and performance monitors for spike members
6. prepare data for dashboard

there could be several geo aware hubs.

SPIKE
===

Spike is a remote data center location, i.e. LONDON. Spike may host N worknodes. 

  Worknode
  ---
  Worknodes can be master or hot standby slaves, the only difference is who's 0MQ is used for decoupling work load.
  
  each worknode consists of :
  
  1. Job agent. 
     - keeps work list for location up to date, by pullig list DIFF from the HUB. Each node has full work list, so it can fail over instantly. Cost of loading large lists is mitigated by loading only diffs from hub
    
  2. Workqueue, job list is thereafter fed every minute
    

