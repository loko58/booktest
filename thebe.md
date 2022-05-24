---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.10.3
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(launch:thebe)=
# Make your code cells executable

This section describes how to bring interactivity to your book. This lets users
run code and see outputs *without leaving the page*. Interactivity is provided
by a kernel running on the public [**MyBinder**](https://mybinder.org) service.

For an example, click the {fa}`rocket` --> {guilabel}`Live Code` button above on this page, and run the code below.

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt
plt.ion()

x = np.arange(500)
y = np.random.randn(500)

fig, ax = plt.subplots()
ax.scatter(x, y, c=y, s=x)
```

:::{warning}
This is an experimental feature, and may change in the future or work unexpectedly.
:::

## Pre-execute cells when Thebe is initialized

Sometimes you'd like to run some code cells *immediately* when a kernel is requested.
This might be code that you then hide from the user in order to narrow the focus of what they interact with.
This is possible by using **cell tags** for the Jupyter Notebook.

Adding the tag {guilabel}`thebe-init` to any code cell will cause Thebe to run this cell after it has received a kernel.
Any subsequent Thebe cells will have access to the same environment (e.g. any module imports made in the initialization cell).

You can then pair this with something like {guilabel}`hide-input` in order to run initialization code that your user doesn't immediately see.
For example, below we'll initialize a variable in a hidden cell, and then tell another cell to print the output of that variable.

```{code-cell} ipython3
:tags: [hide-input, thebe-init]

my_hidden_variable = 'wow, it worked!'
```

```{code-cell} ipython3
# The variable for this is defined in the cell above!
print(my_hidden_variable)
```
