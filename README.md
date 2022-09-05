# Intro

Some personally suggested practices for dependency management using requirements.txt file. PRs, issues are welcome!

# The story

From https://github.com/python-poetry/poetry#why :
```
Packaging systems and dependency management in Python are rather convoluted and hard to understand for newcomers. Even for seasoned developers it might be cumbersome at times to create all files needed in a Python project: setup.py, requirements.txt, setup.cfg, MANIFEST.in and Pipfile.

So I wanted a tool that would limit everything to a single configuration file to do: dependency management, packaging and publishing.

It takes inspiration in tools that exist in other languages, like composer (PHP) or cargo (Rust).

And, finally, I started poetry to bring another exhaustive dependency resolver to the Python community apart from Conda's.
```

From https://github.com/python-poetry/poetry#introduction :
```
poetry is a tool to handle dependency installation as well as building and packaging of Python packages. It only needs one file to do all of that: the new, standardized pyproject.toml.

In other words, poetry uses pyproject.toml to replace setup.py, requirements.txt, setup.cfg, MANIFEST.in and Pipfile.
```

# And...

If you don't want to switch to modern solutions like poetry, Pipfile (pip-env) and ..., here are some suggested practices for dependency management using requirements.txt file:

### Suggested methods for updating requirements.txt file:

* `pip freeze > requirements.txt`
    * Pros:
        * Already available.
    * Cons:
        * Outputs an absolute path for packages installed directly via file urls (Relative path is preferred).
        
        Current status:
        ```
        ...
        my-custom-module @ file:///home/me/code/my_project/my_custom_module-0.1.0-py3-none-any.whl
        ...
        ```
        
        Prefred:
        ```
        ...
        my-custom-module @ file:///./my_custom_module-0.1.0-py3-none-any.whl
        ...
        ```

* `pip list --format=freeze > requirements.txt`
    * Pros:
        * Already available.
    * Cons:
        * Outputs the version for packages installed directly via file urls, just like other modules (Relative path is preferred).

* `pip-chill > requirements.txt`
    * Pros:
        * Outputs only directly installed packages (without their dependencies).
    * Cons:
        * Just like pip, outputs an absolute path for packages installed directly via file urls (Relative path is preferred).
        * pip_chill package should be manually installed via pip.

* `pip-chill -v > requirements.txt`
    * Pros:
        * Outputs only directly installed packages. Their dependencies are printed as comments.
    * Cons:
        * Just like pip, outputs an absolute path for packages installed directly via file urls (Relative path is preferred).
        * pip_chill package should be manually installed via pip.
