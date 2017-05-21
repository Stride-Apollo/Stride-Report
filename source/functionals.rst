
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

We splitted this in two parts, as described in the assignment. The first version was a shared-memory implementation. We've almost finished this. However, we still have to decide on the configuration.

The second part, an MPI implementation, is planned later in the project.

TBB
---

We've already finished a prototype to familiarize ourselves with both OpenMP and TBB. The prototype also showed a small performance increase in favour of TBB.

Scientific visualization
------------------------

We have chosen for a lot of technologies to help build our visualization tool. We use electron to build a native cross-platform desktop application with web technologies like javascript and css. Electron is able of extracting a buildable executable tool which is what we want for our visualization tool. Due to usage of web technologies we have access to a number of useful libraries. We use mapbox for the mapview, plotly for elegant graphs, angularjs for the dynamic content of our tool and material design lite for the overall styling. Once we were all acquainted with these new languages development went very smooth.

The development of the tool is in its final stages, but we risk spending a lot of time on this, since visualizing is just so fun and rewarding.

