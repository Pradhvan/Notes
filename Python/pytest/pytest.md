# Four Phase Test Pattern 
 
1 Setup: Establish the preconditions to the test.

2 Exercise: Do something to the system.

3 Verify: Check the expected outcome.

4 Cleanup: Return the system under test to its initial state after the test


# Introduction to pytest 

`pytest` execution goes off and finds which tests to run. `pytest` is able to find the all the tests that need to be run on the basis of the naming convention:  

* Test Files should be named `test_something.py` or `something_test.py`

* Test methods or functions should be named `test_something.py`

* Test classes should be named `TestSomething` 

### Running pytest 

`pytest`: This runs the entire test directory. 

`pytest -v tests/test_something.py::test_urlcheck.py`: To run one test, specify the file directly and add a `::test_name`. 


### pytest Representation 

```bash

platform darwin -- Python 3.7.6, pytest-5.3.5, py-1.8.1, pluggy-0.13.1
rootdir: /Users/glados/testing-with-python
collected 3 items                                                              

tests/test_something.py ...                                              [100%]

```

The **.** *dots* represent that tests passed - one dot for each test function or method. 

Failures, errors, skips, xfails and xpasses are denoted with `F`, `E`, `s`, `x` and `X` 

Here are the possible outcomes of a test functions: 

* **PASSED(.)**: The test ran sucessfully.

* **FAILED(F)**: The test did not ran sucessfully.(or XPASS +strict)

* **SKIPPED(s)**: The test was skipped with `@pytest.mark.skip()` or `pytest.mark.skipif()`

* **xfail(x)**: The test was not suppose to pass, ran, and failed. To fail a test `@pytest.mark.xfail()` is used. 

* **XPASS(x)**:The test was not suppose to pass, ran and passed. 


* **ERROR**: An exception happened outside the test function in either fixture or hook. 

### Using Options 

### Marking test functions 

#### Skipping tests 

You can mark tests to skip with `@python.mark.skip(reason="")` this way pytest would just skip the tests while the other tests run.

```python
@pytest.mark.skip(reason="Moved to alpha release")
def test_hardbreak():
    pass
```

#### Prametrized tests 

Prametrized tests is a way to send multiple sets of data through the same test and have pytest report if any of the test functions/classes failed. 

`@pytest.mark.parametrize(argnames,argvalue)` can be used to pass lots of data through the same test. 

### pytest Fixtures

Fixtures are functions that runs before and after the actual tests.Fixtures can be used in the following ways:

* to get a data set for the test to work on

* to get a system into a known state before running a test

* to get data ready for multiple tests 

`@pytest.fixtures()` decorator is used to tell pytest that a function is a fxture. 

***pytest philosophy***

> test fixtures refers to mechanism pytest provides to allow the sepration of  *getting ready for* and *cleaning up after* code from your test.

`conftest.py` is the file where all the fixtures are put and the file is centrally located in someplace like `project/test/conftest.py`. 

This was you can share fixtures into multiple test files. 

#### Fixtures for setup and teardown 

```python
@pytest.fixture
def task_db(tmpdir):
    pass
```
`tmpdir` 

Fixtures execution can be traced with `-setup-show`

Fixtures are great place to store data that can be used by other test functions. 

```python
@pytest.fixture
def a_tuple():
    """Returns a tuple"""
    return(1,'foo',{'bar':'2'})

def test_a_tuple(a_tuple):
    assert a_tuple[3]['bar'] == 3
```
#### Scopes in fixtures 

Fixtures include an optional parameter called scope, which controls how often a fixture gets setup and torn down. 

`scope = 'function'` : Run once per test function. The setup function runs every time the test function is run and teardown function is run after each test using the fixture. This is the default scope when no scope is mentioned in the scope.  

`scope = 'class'` : Runs once per test class regardless how many test functions are in the class. 


`scope = 'module'` : Runs once per module regardless how many test functions or methods or other fixtures in the module use it. 


`scope = 'session'` : Runs once per session. All test functions and methods sharing this session scope share one setup and teardown call.

* Scope is set at the definition of a fixture and not at the place where it's being called. 

* Fixtures can only depend on other fixtures of their same scope or wider i.e a function scope can depend upon on class, module or session scope fixtures but not the other way around. 

`@pytest.mark.userfixtures('fixture1', 'fixture2')` can be used to mark a class to use list of fixtures.

```python
@pytest.mark.userfixtures('fixture1', 'fixture2').usefixture
class TestSomething:
    def test1():
        pass 
    def test2():
        pass 

```

* A function using a fixture due to usefixtures cannnot use the fixture's return value. 

* `@pytest.fixture(name='foobar')` is used to rename a fixture.

```python
@pytest.fixture(name='foobar')
def a_tuple():
    """Returns a tuple"""
    return(1,'foo',{'bar':'2'})

def test_a_tuple(foobar):
    assert a_tuple[3]['bar'] == 3
```


#### tmpdir and tmpdir_factory 

The `tmpdir` and `tmpdir_factory` builtin fixtures are used to create a temporary files system directory before your test runs, and remove the directory when your test is finished. 

##### Temporary directories and files for function scope.

```python
def test_tmpdir(tmpdir):
    # tmpdir already has a path name associated with it
    # join() extends the path to include a filename
    # the file is created when it's written to
    a_file = tmpdir.join('something.txt')

    # you can create directories
    a_sub_dir = tmpdir.mkdir('anything')

    # you can create files in directories (created when written)
    another_file = a_sub_dir.join('something_else.txt')

    # this write creates 'something.txt'
    a_file.write('contents may settle during shipping')

    # this write creates 'anything/something_else.txt'
    another_file.write('something different')

    # you can read the files as well
    assert a_file.read() == 'contents may settle during shipping'
    assert another_file.read() == 'something different'
```

`tmpdir` fixture is defined as function scope so the files/directories created will only stay for only one test function.

For class,module or session `tmpdir_factory` is used.

```python
def test_tmpdir_factory(tmpdir_factory):
    # you should start with making a directory
    # a_dir acts like the object returned from the tmpdir fixture
    a_dir = tmpdir_factory.mktemp('mydir')

    # base_temp will be the parent dir of 'mydir'
    # you don't have to use getbasetemp()
    # using it here just to show that it's available
    base_temp = tmpdir_factory.getbasetemp()
    print('base:', base_temp)

    # the rest of this test looks the same as the 'test_tmpdir()'
    # example except I'm using a_dir instead of tmpdir

    a_file = a_dir.join('something.txt')
    a_sub_dir = a_dir.mkdir('anything')
    another_file = a_sub_dir.join('something_else.txt')

    a_file.write('contents may settle during shipping')
    another_file.write('something different')

    assert a_file.read() == 'contents may settle during shipping'
    assert another_file.read() == 'something different'
```

##### Temporary directories and files for class and module scope.

```python
import json
import pytest


@pytest.fixture(scope='module')
def author_file_json(tmpdir_factory):
    """Write some authors to a data file."""
    python_author_data = {
        'Ned': {'City': 'Boston'},
        'Brian': {'City': 'Portland'},
        'Luciano': {'City': 'Sau Paulo'}
    }

    file_ = tmpdir_factory.mktemp('data').join('author_file.json')
    print('file:{}'.format(str(file_)))

    with file.open('w') as f:
        json.dump(python_author_data, f)
    return file

```


#### Cache

cache fixture is used to pass in information from one test session to another test session. 



#### capsys



```python
import sys
import pytest
import random


def greeting(name):
    print('Hi, {}'.format(name))


def test_greeting(capsys):
    greeting('Earthling')
    out, err = capsys.readouterr()
    assert out == 'Hi, Earthling\n'
    assert err == ''

    greeting('Brian')
    greeting('Nerd')
    out, err = capsys.readouterr()
    assert out == 'Hi, Brian\nHi, Nerd\n'
    assert err == ''


def yikes(problem):
    print('YIKES! {}'.format(problem), file=sys.stderr)


def test_yikes(capsys):
    yikes('Out of coffee!')
    out, err = capsys.readouterr()
    assert out == ''
    assert 'Out of coffee!' in err


def test_capsys_disabled(capsys):
    with capsys.disabled():
        print('\nalways print this')
    print('normal print, usually captured')


@pytest.mark.parametrize('i', range(40))
def test_for_fun(i, capsys):
    if random.randint(1, 10) == 2:
        with capsys.disabled():
            sys.stdout.write('F')

```

### Coverage

Code coverage is the measurment of what percentage of code under test is being tested by our test suite. 

```bash
pip install pytest-cov
```
`pytest-cov` is plugin that can generate the coverage of the project. 

```bash
pytest --cov=src
```

`src` is the example directory that has all the sorce code of the project. 
Thus `--cov=` take the dir that you want to generate code coverage for.

