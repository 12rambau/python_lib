:html_theme.sidebar_secondary.remove:

Usage
=====

#.  Define a project name. It can be anything with any normal character (`w+ <regexr.com/7aj95>`__) like "Python Project".

#.  Init an empty github repository with the slug name of your project. A slug should only use lower case characters and replace all spaces with ``-`` like "python-project".

#.  Enable the repository on codecov and add a ``CODECOV_TOKEN`` github action env variable.

#.  Start a new readthedocs project hooked to the repository. in the admin tick the "build on PR" option.

#.  In your local computer start the project by running the following code. Set the same names as in the github repository.

    .. note::
        You will need to install 2 extra python libs if it's not already done, ``copier`` and ``jinja2-time``.

        .. code-block:: console

            pip install copier jinja2-time

    .. code-block:: console

        copier copy --trust gh:12rambau/pypackage <python-project>

#.  Go to the folder and init the git project:

    .. code-block:: console

        cd python-project
        git init

#.  Run ``nox`` tests to see if everything is working. This command will run the 4 nox sessions.

    .. code-block:: console

        nox

#.  Install pre-commits:

    .. code-block:: console

        pre-commit install

#.  Push to distant repository following Github instructions

    .. code-block:: console

        git add .
        git commit -m "build: initial commit"
        git remote add origin git@github.com:<username>/<python-project>.git
        git branch -M main
        git push -u origin main

#.  Once you are ready to make a release (or a pre-release to lock the name), Create a new project on pipy by running the first push yourself using version number ``0.0.0``:

    .. code-block:: console

        python -m build
        twine upload dist/**

#.  Modify the lib as you see fit

#.  Update version with commitizen tools:

    .. code-block:: console

        cz bump

#.  Add a token to a new github action env variable ``PYPI_PASSWORD`` from your pypi profile. limit the scope to this repository only.

#.  Start a new release in github and let actions do the rest

#. The generated package will automatically detect new releases of the template and create update PR. To allow this workflow to work, one needs to give "Read and write permissions" to Workflow and Actions in the "Manage access" tab of the repository settings. One should also "Allow GitHub Actions to create an approve pull requests".
