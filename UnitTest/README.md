# The Path to Learn Unittest
> The `unittest` supports **[test automation](https://en.wikipedia.org/wiki/Test_automation), sharing of setup and shutdown code for tests, aggregation of tests into collections, and indepenence of the tests for the reporting framework**.
## Basic Concept of Testing
1. __test fixture__
A test fixture represents the _preparation_ needed to perform one or more tests, and any associate cleanup actions.
2. __test case__
A test case is the _individual_ unit of testing. It checks for a specific response to a particular set of inputs. `unittest` module provides with a base class: `TestCase` which will be used to create new test cases.
3. __test suite__
A test suite is the _collection_ of test cases, test suites, or both. It is used to _aggregate tests should be executed together_.
4. __test runner__
A test runner is the component which _orchestrates the execution of tests and provides the outcome to the user_. The runner may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.
## Basic example
```
import unittest

class TestStringMethods(unittest.TestCase):
    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')
        
    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())
        
    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```
Something __important__ for this basic example:
1. A test case is creadted by subclassing `unittest.TestCase`.
2. All the individual tests are defined with methods whose name start with the letters _**test**_.
3. `assert` statement is not used because the test runner wants accumulates the results and produce a report.
4. The `setUp()` and `tearDown()` methods allow you to define instructions that will be executed before and after __each test method__.

## Command-Line Interface
[last link](https://docs.python.org/3/library/unittest.html#command-line-interface)
