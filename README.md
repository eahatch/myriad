# myriad
AI Engine for AIX Node Management

Getting Started

Just getting the project off the ground. The goal is to buid an extensible/lightweight agent for AIX that can be used  
is a building block for integration into other systems.

This project values the following:

1. Efficient coding. The agent must be lightweight and fast. No Java.
2. AIX first. Yes I love Linux, but AIX needs some love as well.
3. AI. There will be a human interface that allows for conversational interaction.
4. Expendable. It will be build in a way that lends itself to broader applications.

The first iteration of this project is to create a lightweight OS monitor for AIX that looks at the following in real time:

1. CPU Queue.
2. Swap slot occupancy.
3. I/O waits (or other indicators of disk/network queuing)
4. Other factors as needed based on application performance tuning.

The first iteration of this project will also incorporate a very narrow AI to answer a limited set of questions when submitted.

For example:

     Descibe system health.
     Should I start another process? (This is specific to a current performance issue)
     What do you monitor?
     How are you?

The first extension of this project would be to interact with Nagios monitoring via a NRPE wrapper that asks the AI "questions"
and receives a response that can be translated into a  Nagios return code.

The second extension of this project would be to provide L2 with an AI based interaction for server health and monitoring:

    L2: How are you?
    Kami: Not well, /opt is at 95%
    L2: Do you know the root cause?
    Kami: Yes, it appears that PID 12345678 is logging to /opt/badbot/nohup.out and that file is 2GB
    L2: Can you extend the filesystem?
    Kami: Please contact L3 to fix the root cause.
    L2: Good bye.
    Kami: Good bye.

So we see in this interaction a policy at play that I see as useful. Instead of just applying a "band aide" to
the symptom, we are enforcing good practices through intelligent automation. We could simply provision enough extra space to 
support automatically keeping all filesytems below a standard threshold, but that approach is flawed in that abnormal system
behavior is usually an indicator of other problems (application logs that generate thousands of errors a second or debug logging
that was inadvertently left in place). If we automate the quiescing of these "early warnings" the cumulative effect is often much
worse (service outage due to exhausting resources by an application).

Another example:

   L2: How are you?
   Kami: Not well, it appears as if we have exhausted available open files.
   L2: Do you know the root cause?
   Kami: Yes, it appears that there are 64375 sqlplus processes running at this time.  
   L2: What can you tell me about the processes?
   Kami: There are 24675 orphaned sqlplus processes that are older than 24 hours.
   L2: Can you please kill all orphaned processes on the system?
   Kami: Yes. Sucessfully killed all orphaned processes on the system. 
   L2: How many available open files are on the system?
   Kami: There are 45768 open files on the system.
   L2: Good bye.
   Kami: Please contact L3 to determine the root cause. Good bye.  

In this example we didn't find the root cause, but we also didn't provide additioinal resources.  It is very likely that
the same issue will happen again. Best case is that the root cause is discovered and fixed on the first iteration. Worst case
is that someone fixes the symptom and forgets it ever happened.  In this case we provide immediate relief (could be trigged
based on application SLAs or time of day), log the issue and actions taken and request that the root cause is discovered and fixed.

Programming these interactions is going to be difficult, but I am hopeful that we can introduce a low level of AI simply by applying
workflows into the chatterbox module via list training. I'm just getting up to speed with chatterbox so mileage is likely to vary.  
  
The third extension of this project would be to build a dashboard for reporting and centralized standards management. I'm not really
sure how this would look or if we might just "plug into" another tool at this point (such as Puppet or Ansible), but we definitely
will want a centralized policy repository. Think of it as collected sysadmin wisdom applied across your AIX enterprise.

Built With

Pyton - Human interface 
C - Machine interface 
Chattbot - AI interface 

Contributing

Please read CONTRIBUTING.md for details on our code of conduct, and the process for submitting pull requests to us.

Versioning

We use SemVer for versioning. For the versions available, see the tags on this repository.

Authors

Alan Hatch - Initial Work 
See also the list of contributors who participated in this project.

License

This project is licensed under GNU General Public License v3.0  - see the LICENSE.md file for details

Acknowledgments

Hat tip to anyone who's code was used
Inspiration
etc
