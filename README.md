[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/orca-plotly-binderized/master?filepath=index.ipynb)

# orca-plotly-binderized

Run Plotly's Orca on MyBinder without a Dockerfile.

Click on any `launch binder` badge on this page to launch an active session that includes a demonstration notebook.

----

This is an alternative approach to [Mathieu Boudreau's implementation with a Dockerfile](https://github.com/mathieuboudreau/orca-plotly-dockerfile). It will allow saving Plotly-generated plots as static images in addition the more typical interactive Plotly plot. The static images are good for use elsewhere. And by combining it commandline/scripting it makes it possible to produce a lot of images without saving them by hand from the interactive form.


In the example here `requirements.txt` is used for specifying most of the repo-specific dependencies. `postBuild` is uded to handle setting up orca. Additionally, `apt.txt` was used for replacing the first section of the [Mathieu Boudreau's Dockerfile](https://github.com/mathieuboudreau/orca-plotly-dockerfile/blob/master/Dockerfile) to install some critical apt packages. Except for the `postBuild` file these are just lists of needed packages or dependencies, and so they offer a way to more easily customize a repo than editing than a Dockerfile.

-----

Click the badge to see a demonstration served from MyBinder.org:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/orca-plotly-binderized/master?filepath=index.ipynb)


