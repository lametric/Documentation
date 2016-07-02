# LaMetric Time Developer Documentation

This is the repository for the public LaMetric Time developer documentation.

This documentation is written using [reStructuredText](http://docutils.sourceforge.net/rst.html), powered by [Sphinx](http://www.sphinx-doc.org/en/stable/), and hosted on [ReadTheDocs](http://readthedocs.org).

## Building the docs

Install Software 

1. [Install python and `pip`](https://pip.pypa.io/en/stable/installing).
1. [Install sphinx and sphinx-autobuild](https://docs.readthedocs.io/en/latest/getting_started.html)
  `pip install sphinx shpinx-autobuild`
1. [Install sphinx-rtd-theme](https://github.com/snide/sphinx_rtd_theme#installation)
  `pip install sphinx_rtd_theme`
1. Install recommonmark
  `sudo pip install recommonmark`

Follow these steps to build the documentation locally:

1. Open terminal and cd to the project folder
1. Build HTML: `$ make html`
1. Open `_build/html/index.html` in a web browser.

To see the available make targets, simply execute `make`.

## Contributing

If you find a typo, error, or think something can be communicated better, fork this repository and make a pull request.

## Contact

You can reach us at <mailto:support@lametric.com> with any feedback or questions.
