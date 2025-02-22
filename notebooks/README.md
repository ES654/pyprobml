# Notebooks

## Instructions for contributors

### How to contribute?

1. Choose a figure from [book1](https://probml.github.io/pml-book/book1.html) ([pdf](https://github.com/probml/pml-book/releases/latest/download/book1.pdf)) or [book2](https://probml.github.io/pml-book/book2.html) ([pdf](https://github.com/probml/pml2-book/releases/latest/download/pml2.pdf)) and find out its source code notebook in this repo (mostly in the `notebooks` folder).
2. Fork the main repo and create a new branch with a meaningful name.
3. Take [this notebook](https://github.com/probml/pyprobml/blob/master/notebooks/book1/02/discrete_prob_dist_plot.ipynb) as a reference while converting the source code to a notebook. In perticular, follow these steps:
    * Wrap imports in `try: except:` blocks. for example:
    ```python
    try:
        import tensorflow as tf
    except:
        %pip install tensorflow
        import tensorflow as tf

    from tensorflow import keras
    ```

    * Do not wrap imports in `try: except:` blocks if a package is present in [requirements.txt](requirements.txt) or it is an inbuilt python package such as `os`, `sys`, `functools` etc.
    * Make sure you import and use `latexify` function within `if "LATEXIFY" in os.environ:` block.
    * Set appropriate height and width using the latexify function. for example: 
    ```py
    latexify(width_scale_factor=1, fig_height=1.5)  # width = 6 inch, height = 1.5 inch
    latexify(width_scale_factor=2, fig_height=2)  # width = 3 inch, height = 2 inch
    ```
    * Do not use `.pdf` or `.png` extension while saving a figure with `probml_utils.savefig`. For example:
    ```py
    savefig("foo")  # correct
    # savefig("foo.pdf")  # incorrect
    # savefig("foo.png")  # incorrect
    ```

4. To ensure your code passes the code formatting check, `pip install pre-commit` locally and run `pre-commit install`.
    * Install `black` for jupyter notebooks with: `pip install black[jupyter]` (bash) and `pip install 'black[jupyer]'` (zsh).
    * `pre-commit` will automatically format your notebook as per [this config](https://github.com/probml/pyprobml/blob/master/.pre-commit-config.yaml).
6. Follow PEP 8 naming convention.
7. Convert the existing code to `jax`, `flax` and `distrax` wherever possible.
8. (If applicable) In the last cell, create an interactive demo with `@interact`, `interactive` or any other tools available with `ipywidgets`. Make sure the demo works on Google colab.
9. Please modify existing figure names by adding `_latexified` suffix and remove the `.pdf`/`.png` extension if present. e.g. `uniform_distribution.pdf` should be renamed as `uniform_distribution_latexified`.

### Generating figures and saving them locally
* By default, figures are not saved:
```py
ipython foo.ipynb
```
* To save figures locally (in `.png` format):
```py
export FIG_DIR=/path/to/figures/directory
ipython foo.ipynb
```
* To save latexified figures locally (in `.pdf` format):
```py
export FIG_DIR=/path/to/figures/directory
export LATEXIFY=1
ipython foo.ipynb
```

### Gotchas

* Use `latexify` function carefully with `seaborn`. Check if the generated figure is as expected.
* VS code does not behave well when using notebooks with `ipywidgets`, so double check with `jupyter notebook` GUI if something does not work as expected.
