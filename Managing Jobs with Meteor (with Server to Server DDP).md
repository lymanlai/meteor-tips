Managing Jobs with Meteor (with Server to Server DDP)

In the Meteor community there are couple of packages for managing distributed jobs. Let me show you few of them:

Workers - This project is similar to what we've done here. It'll manages workers for you.
Synched Cron - It's a distributed cron like job management system.
Job Collections - It's another attempt to Job Scheduling for Meteor. It has a rich API compared with the simple API provided by Synched Cron.
All of the above solutions are directly coupled with Meteor. But, you can always use dedicated queuing servers and cloud services for Job Management. Let me show you few of them:

RabbitMQ
Kafka
Iron MQ
Google Cloud Pub/Sub
AWS SQS
