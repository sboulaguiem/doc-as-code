# I. Monitoring Principles

## Chapter 1. Monitoring Anti-Patterns

> An anti-pattern is something that looks like a good idea, but which fires back badly when applied - Jim Coplien.

### Anti-Pattern #1: Tool Obsession

The author points out two problems in this first section:

1. Being captive to the features of your monitoring tool.
2. Searching for THE tool when many are needed.

He illustrates his first point with the following quote from Richard Bejtlich:

> Too many security organizations put tools before operations. They think "we need to buy a log management system" or "I will assign one analyst to antivirus duty, one to data leakage protection duty." And so on. A tool-driven team will not be effective as a mission-driven team. When the mission is defined by running software, analyst become captive to the features and limitations of their tools.
> 
> Richard Bejtlich - The Practice of Network Security Monitoring

Relatedly, **monitoring isn't just a single, cut-and-dry problem**. Monitoring is multiple complex problems under one name, so it stands to reason that it can't be solved with a single tool. Multiple tools are needed, and this is what mission-driven teams will naturally gravitate toward: 

> Analyst who think in terms of what they need in order to accomplish their mission will seek tools to meet those needs, and keep looking if their requirements aren't met. Sometimes they even decide to build their own tools.
> 
> Richard Bejtlich - The Practice of Network Security Monitoring

There is no [single-pane-of-glass](#glossary) tool that will suddenly provide us with perfect visibility into our network, servers and applications. Just like a professional mechanic has an entire box of tools, some general and some specialized, so should you.


Now that you are convinced that many tools are needed, you might start to get worried about the increase in complexity integrating many tools to your environment will bring. **How many tools are too many?** **How many tools do I need?** 

**<p style="text-align: center;"> As few as you need to get the job done</p>**

But there's a nuance to this general rule of thumb: In essence it's desirable that your teams are using tools that solve their problems, instead of being forced into tools that are a poor fit for their needs. On the other hand where you should be rightfully worried is when you have many tools that have an inability to work together. In other words: عينك ميزانك

### Anti-pattern #2: Monitoring-as-a-Job

Monitoring is not a job - it's a skill, and it's a skill everyone on your team should have to some degree. As you move along your monitoring journey, insist that everyone be responsible for monitoring. One of the core tenets of the DevOps movement is that we're all responsible for production, not just the operations team. Network engineers know best what should be monitored in the network and where the hot spots are. Your software engineers know the applications better than anyone else, putting them in the perfect position to design great monitoring for the applications.

Strive to make monitoring a first-class citizen when it comes to building and managing services. Remember, **it's not ready for production until it's monitored**. The end result will be far more robust with great signal-to-noise ratio, and likely far better signal than you've ever had before.

There is a distinction that must be made here, of course: the job of building self-service monitoring tools as as service you provide to another team is a valid and common approach. In these situations, there is a team whose job is to create and cultivate the monitoring tools that the rest of the company relies on. However, this team is not responsible for instrumenting the applications, creating alerts, etc.

### Anti-Pattern #3: Checkbox Monitoring

*Checkbox monitoring* is when you have monitoring systems for the sole sake of saying you have them (because of regulation compliance, or a higher up requirement). In order to to check it off the to-do list, you often set up the simplest and easiest monitoring system and the result is always the same: your monitoring is ineffective, noisy and untrustworthy. There are a few things you can do to fix this anti-pattern:

#### What Does "Working" Actually Mean? Monitor That.
To fix this problem, you first need to understand what it is you're monitoring. What does "working" mean in this context?

#### OS Metrics Aren't Very Useful – for Alerting
Some services are resource-intensive by nature and that's OK. If MySQL is using all of the CPU consistently, but response times are acceptable, then you don't really have a problem. That's why it's far more beneficial to alert on what "working" means as opposed to low-level metrics such as CPU and memory usage.

That isn't to say these metrics aren't useful, of course. OS metrics are critical for diagnostics and performance analysis, as they allow you to spot blips and trends in underlying system behavior that might be impacting performance. 99% of the time, they aren't worth waking someone up over. Unless you have a specific reason to alert on OS metrics, stop doing it.

#### Collect Your Metrics More Often
Imagine latency between two of your critical services spikes every 30 seconds. Only collecting metrics every five minutes means you're effectively blind. Opt for collecting metrics at least every 60 seconds. If you have a high-traffic system, opt for more often, such as every 30 seconds or even every 10 seconds.

Modern servers and network gear can easily handle the minuscule load more monitoring will place on them. Of course, keeping high-granularity metrics around on disk for a long period of time can get expensive. You probably don't need to store a year of CPU metric data at 10-second granularity. Make sure you configure a roll-up period that makes sense for your metrics.

If your devices are old however, they might fall over when hit with too many requests for monitoring data. Be sure to test them in a lab before increasing the polling interval for these.

### Anti-Pattern #4: Using Monitoring as a Crutch

Avoid the tendency to lean on monitoring as a crutch. Monitoring is great for alerting you to problems, but don't forget the next step: fixing the problems. If you find yourself with a finicky service and you're constantly adding monitoring to it, stop and invest your effort into making the service more stable and resilient instead. More monitoring doesn't fix the a broken system.

### Anti-Pattern #5: Manual Configuration

Your monitoring should be 100% automated. Services should self-register instead of someone having to add them. The difficulty in building a well-monitored infrastructure and app without automation cannot be overstated.

# Glossary

- **Single-pane-of-glass:** Single pane of glass is a term used throughout the IT and management fields relating to a management tool that unifies data or interfaces across several different sources and presents them in a single view.





