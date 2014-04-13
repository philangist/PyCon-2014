Porting Your Applications to Python 3

Main points
    - Straddling 2/3 within the same codebase
    - Choosing python versions
    - Porting is an iterative process
    - Add some tests to reduce risk

Porting Strategies
    - Port once, abandon 2 (using the 2to3 app that ships with py3)
    - "Fix up" at installation with 2to3
    * Unfortunately 2to3 is extremely slow on large codebases
      and makes stack traces opaque
    - Straddle py2 and py3 within the same codebase
        - use "compatble subset" of python syntax
        - conditonal imports to mask stdlib changes
        - `six` module can help

Targeting Python Versions
    - Anything less than python 2.6 is hard
        * no b'' (bytes) literal
        * no `except Exception as e:`
        * much more cruft/pain
        * 2.4/2.5 are long past eol

    - Anything less than python 3.2 is hard
        * wsgi is "fixed" in py3k (pep 3333), was broken before 3.2
        * callable() restored
        * unicode restored
        * if targeting long term release ubuntu servers, use 3.2 not 3.3

Managing Porting Risks
    - ports introduce bugs to already working code
    - fear of breaking working software is the barrier (even more than effort)
    - conquer fear by buiulding confidence: use better tests,
      modern py2 idioms, and have clarity in text vs bytes

Bottom Up porting
    - port pacakaged with no dependencies first
    - then port pacajages with already-ported dependencies
      (note python versions supported by dependencies)
    - lather, rinse, repeat

Testing Avoids Hair-Loss
    - Untested code is where bugs hide
    - 100% coverage is ideal BEFORE porting
        * unit testing preferable for libraries
        * functional testing for applications
    - Work to improve assertions as well ass coverage. you want to assert
      contracts, not implementation details
    - Automate running tests
    - Use tools like `tox` that ensure tests pass under all supported versions


"Common subset" idioms can be found in Lennart Regebro's book - python3porting.com
