MEMCACHED

What is it?
- O(1) everything
- Key Object store, objects can expire


Where does it fit?
Primary data: RDBMS
Data you can lose, regenerate slow: Persitent Store (mongo db, redis)
Data you can lose, regenerate fast: RAM Store (memcached)

Operations
Get, set, delete
N.B: Bulk of latency is network bound when using memcahced, so we prefer to use *_many operations
Counter increment
set vs add - add is like set, but only works if the key doesn't exist

Naming conventions
- Ascii Based
- Short and sweet (key names are hashed)
- succint but explicit
- Do not trust user id

Good example:
    json.user.<name>

Bad:
    md5(sql_object)

It's a cache, not a database - You can't query Memcached

Distributed, run as many nodes as you want. Nodes have no knowledge of each other.

Application --> Client ----> Node
                       ----> Node
                       ----> Node

Expiration:
Expired objects are only removed when they're accessed, not when they're set to expire
Data is evicted when memory is full and you add new keys (useing a least recently used cache)


Common Design Patterns

Cache Name
@property
def _cache_name():
    return 'json.book.{}'.format(self.name)

Model Versioning
Class Variable MODEL_VERSION
Update model version when model is saved, old versions miss in the cache

Bulk get
- Get all pks
- Get all keys from db with pks
- Create set of any missing keys (no guarantee keys are returned in previous step)
- set_many missing keys
- Return all objects

Use locks to avoid "thundering herd"


Caching Large Values
- Memcahced has a defalt 1 mb page size
- If your object is large than 1mb your objects won't be stored and you'll get none when trying to get them

Use a 2-phase fetch to store these objects
Use a paginated cache (break big obejcts into smaller chunks, store each chunk and indexes in a list)
