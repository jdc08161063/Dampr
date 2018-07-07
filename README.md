Polymr - Pure Python MapReduce
===

Polymr is intended for use as single machine map-reducing: it's natively out of core, supports reduce side joins, and provides a high level interface for constructing MapReduce DAGs.

## Example - WC

```
import sys 

from polymr import Polymr

def main(fname):

    polymr = Polymr()
    wc = polymr.text(fname) \
            .map(lambda v: len(v.split())) \
            .group_by(lambda x: 1) \
            .sum()

    results = wc.run("word-count")[0]
    for k, v in results.read():
        print("Word Count:", v)

    results.delete()

if __name__ == '__main__':
    main(sys.argv[1])
```