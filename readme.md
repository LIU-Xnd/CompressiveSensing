<!--
 * @Author: LIU-Xnd
 * @Date: 2023-04-28 11:26:41
 * @LastEditors: LIU-Xnd
 * @LastEditTime: 2023-04-28 11:44:07
 * @FilePath: \CompressiveSensing\readme.md
-->
**This is a project only used for private thesis 2023.**

Written languages:

- English;

- Chinese simplified.

# Navigation

- Realizations of the algorithms: see [`Algorithms.ipynb`](/Algorithms.ipynb).

- Numerical test results:

    - see [`Test.ipynb`](/Test.ipynb) for Static CS with prior support information;
    
    - see [`Thread2.ipynb`](/Thread2.ipynb) for Dynamic CS.

- All raw data refered above therein are saved in `.pickle` format, which could be loaded through Python package `pickle` like below:

```{python}
import pickle

# Variable saving.


def pickleSave(var, filename='.pickle'):
    if '.pickle' not in filename:
        filename = filename + '.pickle'
    with open(filename, 'wb') as f:
        pickle.dump(var, f)
    print('PickleSave Succeeded.')
    return

# Variable loading.


def pickleLoad(filename):
    """
    Make sure it's assigned to a variable.
    """
    if '.pickle' not in filename:
        filename = filename + '.pickle'
    with open(filename, 'rb') as f:
        cache = pickle.load(f)
    print("PickleLoad Succeeded. Make sure it's assigned to a variable.")
    return cache


# Load:
Var001 = pickleLoad('Var001.pickle')
# Or for short:
# Var001 = pickleLoad('Var001')
```

or more simply,

```
import pickle
Var001 = pickle.load('Var001.pickle')
```

Make sure all necessarily depended packages/libraries are imported before loading a specific `pickle` data.
