
Functionals
===========

Here we'll discuss our progress for each functional requirement.

Population generator
--------------------

We had a rough start, since there was an inconsistency in the assignment. We wrote quite some code for this that was eventually not needed, since the assignment was changed.

After the change, we made reasonable progress and were able to implement all of the requested features. We finished quite early in the project and were able to use it during the development of multi region.


Checkpointing
-------------

Progress for this was rather consistent, until we had to write a ParaView plugin. Building and configuring ParaView turned out to be rather difficult, therefore the making of the paraview reader is put on hold. Meanwhile we have been working on an integration of checkpointing with our multi region functionality, this in combination with all the changes that will be made by MPI is not trivial, while the basis is there, the exact integration is not yet finished.


Multi region
------------

We splitted this in two parts, as described in the assignment.
Our goal here was to make an interface that is designed in such a way, that you wouldn't notice the difference between the shared memory approach and the MPI approach.
This had some serious consequences for the shared memory solution.

The first version was a shared-memory implementation.
We had to rewrite the above mentioned interface 3 times. This was due to some misunderstandings and miscommunications.
We've almost finished this. However, we still have to decide on the configuration.

We are now working on a prototype for the MPI part of multi region.
This prototype is almost finished but at the moment we only send messages between processes.
The messaging between real life computers is still a work in progress.
Besides this we also need to determine how we use :code:`std::future` in this specific situation.

The addition of travellers to the project brought lots of troubles. Originally we wanted to use pointers to associate a traveller with his home person, but this wouldn't work in a distributed system.
This resulted of course in a small performance hit.

TBB
---

We've already finished a prototype to familiarize ourselves with both OpenMP and TBB. The prototype also showed a small performance increase in favour of TBB.

Scientific visualization
------------------------

We have chosen for a lot of technologies to help build our visualization tool. For all the information on this topic we refer to our blogposts.
The development of the tool is in its final stages, but we risk spending a lot of time on this, since visualizing is just so fun and rewarding.
