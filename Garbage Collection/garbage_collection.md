Garbage Collection in Python

Outline
    - How GC Works in Cpython and PyPy
        * implementations
        * optimizations
    - GC semantics & subtleties


What is GC
    - Unused objects are finalized and deallocated. When? "eventually".. or never!
    - To prevent OOM errors


CPython
    - Reference counting
       * Objects have a count of how many objects want them to be alive
       * When ref count is 0 the object is dead and can be deallocated
       * All new ovjects have a ref count of 1
       * Sometimes two dead objects reference each other, and stay in
         memory instead of being deallocated


PyPy
    - An interpreter written in RPython, translated to low level language(C)
    - Interpreter is abstracted from GC
    - This allows us to plug in custom GCs
    - Mark and Sweep GC:
        * Start from known live objects, recursively traverse all objects marking them as reachable
        * Walk through ALL known objects, removing any objects that were not marked as reachable


Fancy PyPy GC optimizations
    - Python allocates new objects constantly, and they often don't live very long.
      This is called 'High Infant Mortality'
    - To address this we use the nursery:
        store newly allocated objects in a buffer called the "nursery"
        collect the nursery often and move surviving objects elsewhere
        gc old objects less frequently (major collection)
    - When the GC is running, the program is blocked. To address this PyPy uses a
      proces called incremental GC
    - Major collection is split into multiple passes, each lasting only a few milliseconds


GC in PyPy summary
    - pluggable
    - generational
    - incremental
    - JIT compiler


GC Semantics
    - '__del__' kills kittens. Cycles with finalizers lead to a conundrum.
      Which finalizer do we want to run first
    - In versions of CPython < 3.4 this was essentially an ignored problem
    - PEP 442 addresses this in CPython >= 3.4
        * "Safe object finalization"
    - PyPy opologically sorts objects in a reasonable order, and handles
      them that way
