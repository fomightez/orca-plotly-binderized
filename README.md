[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/orca-plotly-binderized/master?filepath=index.ipynb)

# orca-plotly-binderized

Run Plotly's Orca on MyBinder without a Dockerfile.

Click on any `launch binder` badge on this page to launch an active session that includes a demonstration notebook.


----

You may not need this!!!

Usually using [nbviewer](https://nbviewer.org/), Jupyter's supported notebook viewer, the interactive Plotly plots show up. Although Github's rendering has improved vastly of late, nbviewer remains the way to view and share static versions notebooks that are hosted on GitHub. Compare [this at Github](https://github.com/fomightez/3Dscatter_plot-binder/blob/master/Plotly3d-scatter-plots.ipynb) vs. [on nbviewer](https://nbviewer.org/github/fomightez/3Dscatter_plot-binder/blob/master/Plotly3d-scatter-plots.ipynb). Advise only relying on Github's viewer for a quick preview.

Plus Kaleido is the newest version doing what Orca did.

-------------------


Sessions launched from this repo will allow using commands in side a Jupyter environment to save Plotly-generated plots as static images in addition the more typical interactive Plotly plot. The static images are good for use elsewhere. And by combining it commandline/scripting it makes it possible to produce a lot of images without saving them by hand from the interactive form. To do this, it uses Plotly's orca. Learn more about Plotly's orca [here](https://github.com/plotly/orca) and [here](https://plot.ly/python/static-image-export/).


This repo uses an approach alternative to [Mathieu Boudreau's implementation with a Dockerfile](https://github.com/mathieuboudreau/orca-plotly-dockerfile). Here, `requirements.txt` is used for specifying most of the repo-specific dependencies. `postBuild` is uded to handle setting up orca. Additionally, `apt.txt` was used for replacing the first section of the [Mathieu Boudreau's Dockerfile](https://github.com/mathieuboudreau/orca-plotly-dockerfile/blob/master/Dockerfile) to install some critical apt packages. Except for the `postBuild` file these are just lists of needed packages or dependencies, and so they offer a way to more easily customize a repo than editing than a Dockerfile.



----

Click the badge to see a demonstration in a Jupyter notebook with a Python kernel served from MyBinder.org:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/orca-plotly-binderized/master?filepath=index.ipynb)


