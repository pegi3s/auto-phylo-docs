Test data
*********

There are three test sets available:

- `test_1.zip <http://evolution6.i3s.up.pt/static/auto-phylo/test_data/test_1.zip>`_.
- `test_2.zip <http://evolution6.i3s.up.pt/static/auto-phylo/test_data/test_2.zip>`_.
- `test_3.zip <http://evolution6.i3s.up.pt/static/auto-phylo/test_data/test_3.zip>`_.

To run them, just follow the instructions that are given on the ``README.txt`` file for each test case. 

Specially, take care of the fact that the ``config`` file should be edited to put into ``dir`` the actual path to the test data directory in your computer.

Note that the second test may take a long time because of the ``mp_tree`` module (up to 24 hours depending on the available resources).

Running times
-------------

These are the running times for the tests using a high-performance computing server (1TB of RAM with 96 cores, AMD EPYC 7401 24-Core Processor):

- Test 1: ~30 minutes.
- Test 2: ~19 hours.
- Test 3: ~1 hour.