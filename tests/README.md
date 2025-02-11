## Test Suite
`Location`: ./test_sample.py or ./tests  
`Purpose`:  Package integration and unit tests.  

Starting out, a small test suite will often exist in a single file:

    ./test_sample.py
Once a test suite grows, you can move your tests to a directory, like so:

    tests/test_basic.py  
    tests/test_advanced.py

Obviously, these test modules must import your packaged module to test it. You can do this a few ways:

  - Expect the package to be installed in site-packages.
  - Use a simple (but explicit) path modification to resolve the package properly.

I highly recommend the latter. Requiring a developer to run setup.py develop to test an   
actively changing codebase also requires them to have an isolated environment setup for   
each instance of the codebase.

To give the individual tests import context, create a tests/context.py file:

    import os
    import syssys.path.insert(0, os.path.abspath('..'))
    
    import sample

Then, within the individual test modules, import the module like so:

    from .context import sample

This will always work as expected, regardless of installation method.

Some people will assert that you should distribute your tests within yourmodule itself -- I disagree.  
It often increases complexity for your users; many test suites often require additional dependencies   
and runtime contexts.

