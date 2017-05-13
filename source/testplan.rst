Test plan
=========

We use `Google Test <https://github.com/google/googletest>`_ for our tests. We split the tests in two major parts: unit tests and scenario tests. We choose between the two parts via a parameter provided at runtime.

We have also decided that CTest did not have any more value to us, except making the build process more complicated. Therefore, we no longer use it.

Continuous Integration
----------------------

There are 4 different choices to be made:

  - (short) **unit tests** or (long) **scenario tests**

  - **gcc** or **clang**

  - **TBB**, **OpenMP** or the **dummy** implementation

  - with or without **MPI** (however, see MultiRegio_)

All tests are executed often; on all commits. A pull request may only be merged if CI says it's ok, on top of a manual review. To get quick feedback from unit tests, we split unit tests from scenario tests using `Travis Stages <https://docs.travis-ci.com/user/build-stages>`_, a very recent feature.

Assignments
-----------

For each assignment we'll discuss how we are going to test this functionality.

HDF5 checkpointing
^^^^^^^^^^^^^^^^^^

We test checkpointing in different ways:

A first form of testing is checking the format and content of different HDF5 files. We make a difference between happy-day scenario files and wrong files (not according to the format, differing from the simulator's state, ...). Another form is running from various interim checkpoints, after which we compare the results from those runs with runs that ran uninterrupted from start to finish (when using no parallelization, this has to be an exact match). 

TBB Parallelization
^^^^^^^^^^^^^^^^^^^

To test our implementation of TBB, we'll first write some scenario's and run them manually. After this, we check the results ourselves. If the results are free of errors, we create a test case from it.

Apart from that, we'll also write some unit tests to ensure the behaviour of the code of is as we expect in all three implementations (TBB, OpenMP, Dummy).

Population generator
^^^^^^^^^^^^^^^^^^^^

There are a few classes that help the generator, for example one that provides an Alias distribution or a class that works with geo-coordinates. These classes will have unit tests for various edge cases and configurations.

Testing the generator itself is split in three parts:

  - **Input files**: When input files are syntactically or semantically incorrect, the generator has to properly handle them.
  
  - **Distributions**: We have to check whether the distribution of the generated data is as we expect. Extreme values shouldn't occur in sufficiently large populations. For example, it is virtually impossible for a random generated population of one million people to have half a million unemployed people when the given unemployment rate is 10%.
  
  - **Output**: Parts of the output can be checked without resorting to statistical analysis. For example, all possible family compositions are known at the start. It shouldn't happen that a family is generated of which the composition is nonexistent.

.. _MultiRegio:

Multi regio
^^^^^^^^^^^

In our architecture we plan to abstract all MPI communication details in an interface equal to the one used in a shared-memory implementation. Once the MPI implementation for MPI is finished, we'll extensively test it. However, because of the added complexity that is distributed testing, we will do this manually and preferably only once. Testing with multiple processes (and not multiple machines) could be repeated more often. In the build configuration, MPI can still be turned on or off, but no unit tests will be written testing the actual distributed nature of the system. Therefore, the only reason to try compiling with MPI is to test whether it interferes with other components.

To write unit tests for multi regio, we'll use only the shared-memory implementation. In theory, if the interface behaves exactly like the one used by MPI, this should be enough. To make up for the loss in testing, we plan to spend more attention to code reviews regarding MPI.

Scientific Visualisation
^^^^^^^^^^^^^^^^^^^^^^^^

Scientific visualisation is primarily a GUI implemenation and therefore rather hard to test. The quality of our visualisation is also not objectively measurable. Therefore, we'll mainly test the scientific visualisation manually, throughout the project.
