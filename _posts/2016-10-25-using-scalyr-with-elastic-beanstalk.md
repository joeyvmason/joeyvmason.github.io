--- 
title: Using Scalyr with Elastic Beanstalk
date: 2016-10-25 12:00:00 Z
layout: post
---

# What is Scalyr?

Scalyr provides the ability to aggregate logs from multiple servers and clients into one place. From there, using a simple query 
language, you can search through all of the logs in the Scalyr dashboard in real-time. 

For anyone working with distributed systems, this is an extremely powerful tool. It can literally save you hours. Not only that, in 
environments where servers are ephemeral, not having to look up multiple IP addresses and then SSH into multiple remote servers can 
mean the difference between resolving a production issue in minutes rather than hours. 

There are several other similar [Logging as a Service (LaaS)](https://en.wikipedia.org/wiki/Logging_as_a_service) startups out there 
(e.g. [Loggly](https://www.loggly.com), [Papertrail](https://papertrailapp.com)), but I've found Scalyr to be the best of the bunch 
if you're looking for pure log management.


# How does it work?

There are [several ways](https://www.scalyr.com/help/data-sources) that you can get your log data into Scalyr's system, but the most 
straight forward way to do it is to use the Scaly Agent. 

### Scalyr Agent

The Scalyr Agent is a daemon which you install on your servers. It monitors logs and system metrics and automatically sends them to Scalyr's servers. 

#### Installation 

{% highlight shell %}
wget -q https://www.scalyr.com/scalyr-repo/stable/latest/install-scalyr-agent-2.sh && \
  sudo bash ./install-scalyr-agent-2.sh \
      --set-api-key "{YOUR_API_KEY_HERE}" \
      --start-agent
{% endhighlight %}

#### Configuration

There are a [many configuration options](https://www.scalyr.com/help/scalyr-agent#configuration) available for the Scalyr agent. For 
example, you can customize the host name or provide a path to the particular log file you want to capture. To change the configuration, 
you will need to edit the config file: 

{% highlight shell %}
/etc/scalyr-agent-2/agent.json
{% endhighlight %}

<!-- There are a lot of options available. If you are using Elastic Beanstalk, then you most like have two types of servers: web servers and workers, bot of which will be autoscaled independently by Elastic Beanstalk. To make analyzing your logs much easier, I'd highly recommend using custom configuration to set the $tier...
-->


### Log Import
Alternatively, you can configure Scalyr to import logs from places like Heroku, Amazon RDS and Amazon S3. I won't be covering that in 
this post, but you can learn more [here](https://www.scalyr.com/help/data-sources).


# Elastic Beanstalk

AWS Elastic Beanstalk is an autoscaling [Platform as a Service (PaaS)](https://en.wikipedia.org/wiki/Platform_as_a_service), similar to 
Heroku. You provide your code to Amazon, along with some configuration settings, and Amazon will automatically spin up and down EC2 instances 
based off of scaling triggers.

When using Elastic Beanstalk, you have to assume that at any moment, Amazon might take down an existing server and replace it with a new one. 
In other words, your servers are [cattle, not pets](http://www.slideshare.net/randybias/pets-vs-cattle-the-elastic-cloud-story). Because of 
this, any custom environment configuration will need to be provided up front, which means you won't be able to SSH into the box to install and 
configure Scalyr.

#### .ebextensions

Custom environment configuration is achieved on Elastic Beanstalk through the use of 
[.ebextensions](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions.html) configuration files. These configuration files must be 
YAML-formatted documents and have the file extension `.config` and need to live in the `.ebextensions` directory in the root of your project.

## Scalyr setup with .ebextensions

#### Create .ebextensions directory

In the root of your project, create a new directory called `.ebextensions` (if you're using Spring, this would be at `/src/main/webapp`).

#### Add Scalyr installation script

Create a new file in the `.ebextensions` directory called `scalyr.config` with the following contents:

{% highlight yaml %}

files:
  "/tmp/scalyr.json":
    mode: "000755"
    owner: root
    group: root
    content: |
      {
        "api_key": "<YOUR_SCALYR_API_KEY_HERE>",
        "server_attributes": {
          "environment": "production",
          "tier": "web"
        },
        "logs": [
          {
            "path": "/var/log/tomcat8/catalina.out",
            "attributes": {
              "parser": "catalinaLog"
            }
          }
        ],
        "monitors": [
        ]
      }

commands:
   01-wget:
      command: "wget -q https://www.scalyr.com/scalyr-repo/stable/latest/scalyr-repo-bootstrap-1.2.1-1.alt.noarch.rpm"
   02-removeBootstrap:
      command: "yum remove -y scalyr-repo scalyr-repo-bootstrap  # Remove any previous repository definitions, if any."
   03-installBootstrap:
      command: "yum install -y --nogpgcheck scalyr-repo-bootstrap-1.2.1-1.alt.noarch.rpm"
   04-installScalyrRepo:
      command: "yum install -y  scalyr-repo"
   05-installScalyrAgent2:
      command: "yum install -y scalyr-agent-2"
   06-agentFile:
      command: "cp /tmp/scalyr.json /etc/scalyr-agent-2/agent.json"
   07-start:
      command: "scalyr-agent-2 restart"

{% endhighlight %}

There are two main components to this .ebextensions script. The first section (`files`) tells Elastic Beanstalk to create a temporary file 
at `/tmp/scalyr.json` with provided permissions and content. Replace or update the file content to match your desired Scalyr configuration. 

The second section (`commands`) tells Elastic Beanstalk to install the Scalyr agent, copy over the temporary Scalyr configuration file and start up the Scalyr agent. 
 

### Deploy

At this point, you should be good to go. Deploy your application just as normally would and keep an eye on the Elastic Beanstalk events console. If there are 
any problems, error messages will show up here. Good luck!  



