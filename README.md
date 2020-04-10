# distributed-locks java



distributed locks in Spring Integration to ensure exclusive access to a shared resource in a cluster.
https://www.youtube.com/watch?v=firwCHbC7-c

		<!-- <dependency>
			<groupId>org.springframework.integration</groupId>
			<artifactId>spring-integration-core</artifactId>
		</dependency> -->
		<!-- <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-integration</artifactId>
		</dependency> -->
		<!-- <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-jdbc</artifactId>
		</dependency> -->


https://dzone.com/articles/everything-i-know-about-distributed-locks
https://dzone.com/articles/concurrency-and-how-to-avoid-it

https://www.javadevjournal.com/spring-boot/spring-boot-scheduler/
Parallel Scheduling

//	https://docs.spring.io/spring/docs/3.1.x/spring-framework-reference/html/jdbc.html#jdbc-advanced-jdbc

https://stackoverflow.com/questions/42043701/how-can-i-implement-a-pagination-in-spring-jdbctemplate

@EnableAsync
public class ParallelSchedulingExample {
    @Async
    @Scheduled(fixedDelay = 2000)
    public void fixedDelayExample() {
        LOG.info("Hello from our Fixed delay method");
        try {
            TimeUnit.SECONDS.sleep(3);
        } catch (InterruptedException ie) {
            LOG.error("Got Interrupted {}", ie);
        }
    }
}

https://stackoverflow.com/questions/37335351/schedule-a-task-with-cron-which-allows-dynamic-update
http://mbcoder.com/dynamic-task-scheduling-with-spring/


https://stackoverflow.com/questions/14630539/scheduling-a-job-with-spring-programmatically-with-fixedrate-set-dynamically
https://learnwithtaufik.home.blog/2019/03/05/dynamic-scheduling-with-spring-boot/



https://www.geeksforgeeks.org/reentrant-lock-java/
ReadWriteLock vs ReentrantLock  ---  https://www.youtube.com/watch?v=7VqWkc9o7RM






https://github.com/alturkovic/distributed-lock
https://www.veracode.com/blog/secure-development/distributed-synchronization-spring-jpa
Distributed locking means that you need to consider not just multiple threads or processes, but different clients running on separate machines. These separate servers must coordinate in order to ensure that only one of them is using the resource at any given time
https://dzone.com/articles/distributed-java-locks-with-redis


http://javabypatel.blogspot.com/2017/10/quartz-scheduler-spring-boot-example.html

mysql database level schema design so that it will replicate as distibuted lock

testing senarios - we have only one job - i.e purge_job - same datasouce
-----------------------------------------------------------------------------------------
1. two instances ( App-8081 and App-8082) - same tenant ->> valid senario

	->>>> one instance will acquired lock. other skip.

2. two( tenanat1, tenanat2 ) different tenant with same instance ( App-8081)  ->>  valid senario

this senario is valid becz in this case we need to create two different audit client for respetive tenants
and every client has to call their own purge method with tenant specific propeties.

3. two( tenanat1, tenanat2 ) different tenant with same instance ( App-8081 and App-8082 )  ->>  valid senario


testing senarios - we have only one job - i.e purge_job - different datasouce
-----------------------------------------------------------------------------------------
1. two instances ( App-8081 and App-8082) - same tenant ->> valid senario

	->>>> one instance will acquired lock. other skip.

2. two( tenanat1, tenanat2 ) different tenant with same instance ( App-8081)  ->>  valid senario

this senario is valid becz in this case we need to create two different audit client for respetive tenants
and every client has to call their own purge method with tenant specific propeties.

3. two( tenanat1, tenanat2 ) different tenant with same instance ( App-8081 and App-8082 )  ->>  valid senario



----------------------------------------------------------------------------------------------------------------
1. (instanceName = App-8081 , tenantName = tenanat1 , jobName = purge_job) 
   (instanceName = App-8082 , tenantName = tenanat1 , jobName = purge_job)  ->> 
   
2. (instanceName = App-8081 , tenantName = tenanat1 , jobName = purge_job)
	(instanceName = App-8081 , tenantName = tenanat2 , jobName = purge_job)  ->> 
	
3. (instanceName = App-8081 , tenantName = tenanat1 , jobName = purge_job)

  

---------------------------------------------------------------------------------------------------------
multitenant deployment system - multi-tenants same pod / mutiple pods
single deployment system - single tenant/app same pod / mutiple pods



	-->>> this senario is not valid becz each tenant will have separate deployment. 
			As audit is bundled as jar, and with diffrent datasouce - for each tenant.
			
	
	
----------------------------------------------------------------------------------------------------
