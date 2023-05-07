<!--
 * @Author: LIU-Xnd
 * @Date: 2023-04-28 11:26:41
 * @LastEditors: LIU-Xnd lqxnds@foxmail.com
 * @LastEditTime: 2023-05-07 17:33:14
 * @FilePath: \CompressiveSensing\readme.md
-->
**This is a project only used for private thesis 2023.**

# Navigation

- Realizations of the algorithms: see [`Algorithms.ipynb`](/Algorithms.ipynb).

- Numerical test results:

    - see [`Test.ipynb`](/Test.ipynb) for Static CS with prior support information;
    
    - see [`Thread2.ipynb`](/Thread2.ipynb) for Dynamic CS.

- All raw data refered above therein are saved in `.pickle` format, or `.pickle.part` format if too large, which could be loaded through Python package `pickle` like below:

```{python}
import pickle
import os

# Variable saving.


def pickleSave(var, filename='.pickle'):
    if '.pickle' not in filename:
        filename = filename + '.pickle'
    with open(filename, 'wb') as f:
        pickle.dump(var, f)
    print('PickleSave Succeeded.')
    return

# Variable loading.


def pickleMergeParts(filename):
    if '.pickle' not in filename:
        filename = filename + '.pickle'
    with open(filename, 'wb') as f:
        partId = 1
        partFilename = filename + '.part' + str(partId)
        while True:
            with open(partFilename, 'rb') as fPart:
                f.write(fPart.read())
            partId += 1
            partFilename = filename + '.part' + str(partId)
            if not os.path.isfile(partFilename):
                break
    print('MergeParts succeeded.')
    return



def pickleLoad(filename, tryMergeParts=True):
    """
    Make sure it's assigned to a variable.
    """
    if '.pickle' not in filename:
        filename = filename + '.pickle'

    if not tryMergeParts:
        with open(filename, 'rb') as f:
            cache = pickle.load(f)
        print("PickleLoad Succeeded. Make sure it's assigned to a variable.")
        return cache
    else:
        if not os.path.isfile(filename):
            pickleMergeParts(filename)
        return pickleLoad(filename, tryMergeParts=False)


# Load:
Var001 = pickleLoad('Var001.pickle')
# Or for short:
# Var001 = pickleLoad('Var001')
```

Make sure all necessarily depended packages/libraries are imported before loading a specific `pickle` data.

Note: Some `.pickle` data are too large (>100MB) that they cannot be directly uploaded on Github, so some of these files might be saved in `.pickle.part` format (the `pickleLoad()` function can also deal with it without any specific change). How all the `.pickle` files are produced is available to find in source code files such as `Algorithms.ipynb`, etc. Moreover these too-large data can also be loaded the same way you load `.pickle` data (take `sampMats_m` as an example):

```
# Load:
sampMats_m = pickleLoad('sampMats_m.pickle')
# Or for short:
# sampMats_m = pickleLoad('sampMats_m')
```

The first time you run this code to load `.pickle.part` files, a full `.pickle` data file will be created.

**----- Note -----** 20230507

`sampMats_m.pickle` is the only "too-large" file as mentioned above. 