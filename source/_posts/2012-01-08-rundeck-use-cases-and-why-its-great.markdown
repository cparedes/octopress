---
layout: post
title: "RunDeck"
date: 2012-01-08 21:50
comments: true
categories: 
- Systems Administration
- Service Orchestration
---

There's times when we need to enforce adhoc control over our machines. [This blog post by Alex Honor](http://dev2ops.org/blog/2011/2/16/peanut-butter-in-my-chocolate-convergence-vs-ad-hoc-control.html)
does a way better job than I could to explain why we still need to worry about
adhoc command execution, but a quick summary would probably be the following:

1. Sometimes, we just need to execute commands ASAP - unplanned downtime
and adhoc information gathering both spur this activity.
2. We need to orchestrate any set of commands across many machines - things
like getting your DB servers up and prepped before your web servers come
online is one example of this.

[RunDeck](http://rundeck.org/) can handle these two scenarios perfectly.  It's
a central job server that can execute any given set of commands or scripts
across many machines.  You can define machines via XML, or use web servers that
respond with a set of XML machine definitions (see
[chef-rundeck](https://github.com/opscode/chef-rundeck) for a good example of
this.)  You can code in whatever language you want for your job scripts -
RunDeck will run them on the local machine if the execute bit is set (or, if
you're running jobs across many machines, it will SCP them onto the machine and
execute them via SSH.)

You can define multiple job steps within a job (including using other jobs as a
job step) - thus, you can, for example, have a job step that pulls down your
web application code from git across all web application servers, another job
step that pulls down dependencies, then one more to start the web application
across all of those machines, all of which is coordinated by the RunDeck
server. As another example, you can also coordinate scheduled jobs that
provision EC2 servers at a certain time of the day, run some kind of processing
job across all of those machines, then shut all of them down as soon as the job
is finished.

There's another way these jobs can be started, not only just by manual button
pushing and cron schedules: they can also be started by hitting a URI via the
provided API with an auth token.  To expand on the previous example, if say you
don't have a reliable way to check to see if the processing is finished from
RunDeck's point of view, you can probably have some kind of job that's fired
from the workers, which hits the API and tells RunDeck to run a 'reap workers'
job.

mcollective vs. RunDeck?
------------------------

A few people have asked me how this compares with mcollective.

I would probably say that they're actually complimentary with each other -
mcollective is incredibly nice, in that it has a bit of a better paradigm for
executing commands across a fleet of hosts (pub/sub vs. SSH in a for loop.) You
can actually use mcollective as an execution provider in RunDeck, by simply
specifying 'mco' as the executor in the config file ([here's a great example of this.](https://github.com/phobos182/rundeck-mcollective/blob/master/framework.properties))
RunDeck is nice, in that you can use arbitrary scripts with RunDeck and it'll
happily use them for execution - plus, it has a GUI, which makes it nice if you
need to provide a 'one button actiony thing' for anyone else to use. RunDeck
can also run things 'out of band' (relative to mcollective) - for example,
provisioning EC2 machines is an 'out of band' activity (though you can
certainly implement this with mcollective as well, mcollective's execution
distribution model doesn't seem to 'fit' well with actions that are meant to be
run on a central machine.)

But again, you can tie mcollective with RunDeck, and they'll both be happy
together.  I can see right away that the default SSH executor will likely
be a pain in the ass once you get to about 100+ machines or so.

Conclusion
----------

RunDeck is pretty damn nice. We've been putting it through its paces in our
staging environment, and it's held up very nicely with a wide variety of
tasks that we've thrown at it. The only worries I have are the following:

1. Default SSH command executor will likely start sucking after getting to
about 100+ machines.
2. Since it can execute whatever you throw at it, it's possible that you
might end up with yet another garbled mess of shell and Perl scripts.
This is probably better solved with team discipline, however.
3. There doesn't seem to be a clear way to automate configuration changes for
RunDeck - thus, be sure to keep good backups for now (though, this is probably
because of my own ignorance - the API is pretty full featured, and I believe
you can add new jobs via the API, but it would've been awesome to be able
to just edit job definitions in a predictable location on the disk.)

Despite these worries, I highly recommend RunDeck - it's helped us quite a bit
so far, it's quick to get setup, and quick to start coding against for fleet
wide adhoc control.
