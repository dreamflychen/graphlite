graphlite
=========

![Build Stats](https://travis-ci.org/eugene-eeo/graphlite.svg?branch=master)

A simple social graph datastore using the SQLite library as
a backend. Graphlite provides storage for nodes- unsigned
integers that represent objects in another datastore, for
example the ID of your users and their posts.

```
from graphlite import Graph, V
g = Graph(uri=':memory:', graphs=['follows'])

g.store(V(1).knows(2))
g.store(V(1).knows(3))
g.store(V(2).knows(4))

for item in g.find(V(1).knows):
    print('1 follows %d' % (item))

g.find(V(1).knows).traverse(V().knows)
g.delete(V(1).knows)
g.close()
```

The relations, when stored in the SQLite database, are not
indexed by their recency or any time based value, but rather
by either the source or destination nodes. All queries are
performed using these clustered indexes as well.

Graphlite aims to be performant and sane, as well as offering
a nice API for developers to work with. I also aim for the
library being thread-safe.
