Documentation plan
==================

Code documentation
------------------

We chose to have a not too strict form of documentation.
Everyone is responsible for the documentation of his own code/functionality.
Documenting the code of another person is discouraged.
Also documentation that doesn’t add additional information is left behind (see the following example):

.. code-block:: c++

  /// gets age of Person
  int getAge() const;

For reference documentation we chose to use Doxygen. This means we also use the associated syntax to provide more information for the arguments etc. We try to use the currently present documentation style as much as possible.

Hosting
-------

We plan to use readthedocs.org for both the general documentation (manual) and the reference documentation (doxygen). ReadTheDocs provides a couple of handy benefits:

 - Builds the documentation itself
 - Available for every branch (=> works well with our git workflow)
 - Easily searchable
 - PDF support

User manual
-----------

Concerning the user manual, we make further use of the existing structure of the Stride manual.
Each group will work on a feature. If the user manual needs to change as a result of such a feature the whole group will be responsible for this change. How this is arranged within the group is not determined.
The existing chapters will be expanded/changed if necessary. The command line arguments for checkpointing (chapter 3.2 - Run the simulator) will be extended with the checkpointing frequency.

Next to the existing chapters we will add one more chapter. This chapter will provide more information about the newly added tools. For each tool we will write different subsections like the following:

 - How to use the tool
 - How to configure the tool in the project
 - What is the function of the tool

For example if the user wants to use the multiregion extension he needs to know that it’s possible that he is working with a distributed system.
Below is a short general listing (per feature) of user questions and their specific answers:

- Checkpointing

  - How do I use checkpointing? How do I activate checkpointing?
  - Paraview ⇒ Where can I find the executable? How does it work? What do I get to see?

- TBB parallelisation

  - How do I use TBB? How do I activate it?
  - What are the differences in performance in comparison to other solutions?

- Population generator

  - Where do I find the executable?
  - How do I use this generator? What is the correct XML format?

- Multi region

  - How do I use multi region? Are there consequences I need to be aware of?

- Scientific visualisation

  - How do I use this? What do I get to see?
  - What is the meaning of the results?
