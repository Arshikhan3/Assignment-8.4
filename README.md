# Assignment-8.4
1. Explain the difference between FIFO and Capacity scheduler?
Ans:               FIFO                                                                     Capacity Scheduler 
1)The FIFO Scheduler places applications in a queue and               With the Capacity Scheduler, a separate dedicated queue allows the
runs them in the order of submission (first in, first out).              start as soon as it is submitted.

2) Requests for the first application in the queue are                   This is at the cost of overall cluster utilization since the
allocated first; once its requests have been satisfied,                 queue capacity is reserved for jobs in that queue.
the next application in the queue is served, and so
on.
3)The FIFO Scheduler has the merit of being simple to                 On a shared cluster, it is better to use the Capacity Scheduler or
understand and not needing any configuration, but it’s                 the Fair Scheduler.
not suitable for shared clusters.

4)Large applications will use all the resources in a cluster,          Large job finishes late when compared with using the FIFO 
so each application has to wait its turn.                               Scheduler.
  
2. Explain the difference between FIFO and Fair scheduler?
Ans: Fair scheduling is a method of assigning resources to jobs such that all jobs get, on average, an equal share of resources over time. When there is a single job running, that job uses the entire cluster. When other jobs are submitted, tasks slots that free up are assigned to the new jobs, so that each job gets roughly the same amount of CPU time.

Unlike the default Hadoop scheduler which is FIFO, which forms a queue of jobs, this lets short jobs finish in reasonable time while not starving long jobs. It is also an easy way to share a cluster between multiple of users. Fair sharing can also work with job priorities - the priorities are used as weights to determine the fraction of total compute time that each job gets.

3. Explain the difference between Capacity and Fair scheduler?
Ans:  With the Fair Scheduler, there is no need to reserve a set amount of capacity, since it will dynamically balance resources between all running jobs.Just after the first (large) job starts, it is the only job running, so it gets all the resources in the cluster. When the second (small) job starts, it is allocated half of the cluster resources, so that each job is using its fair share of resources.
After the small job completes and no longer requires resources, the large job goes back to using the full cluster capacity again.
The overall effect is both high cluster utilization and timely small job completion.

With the Capacity Scheduler, a separate dedicated queue allows the small job to start as soon as it is submitted. This is at the cost of overall cluster utilization since the queue capacity isreserved for jobs in that queue. If queues are not designed or used properly, some queues may be overloaded while some may be underutilised.

4. 4. What are the limitations of hadoop 1.x and how they were overcome in hadoop 2.x?
Ans: Limitations of hadoop 1.x are 
1. JobTracker keeps track of resource utilization and job monitoring.

2. Suited for maximum of 4000 nodes and 40000 tasks.

3. TaskTracker is configured with static slots. Moreover, a map tasks can not run on reduce slot. So cluster utilization is low.

4. Supports only MapReduce processing model.

Many changes are there in hadoop 2.x. They are as follows: 
1.Single point of Failure - Each cluster has a single NameNode and if that machine is not available, whole cluster will be not available.It is rectified in hadoop 2.x

2.High Availability - If the NameNode process or machine fails, then the entire cluster will not be available until either the NameNode is rebooted or it is assigned and started on another machine. Any restarted NameNode is not available until it gets heartbeat messages from the data nodes with the block locations for all of the files on the data nodes. This can take hours for large clusters which results in decreased availability when there is an unexpected outage. Hadoop 2 remedied this situation by adding support for HDFS high-availability (HA). In this implementation there is a pair of namenodes in an active-standby configuration. In the event of the failure of the active namenode, the standby takes over its duties to continue servicing client requests without a significant interruption.

3.Nodes Limitation (4000 - to unlimited) 
4.Allows other applications also to integrate with HDFS. 
5.Decentralize JobTracker power to data-nodes. Entire job tracker architecture changed. 
6.Map-reduce slots are changed static to dynamic.
7.Support both Interactive,graph iterative algorithms.
