[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/orca-plotly-binderized/master?filepath=index.ipynb)

# orca-plotly-binderized

Run Plotly's Orca on MyBinder without a Dockerfile.

Click on any `launch binder` badge on this page to launch an active session that includes a demonstration notebook.


----

Sessions launched from this repo will allow using commands in side a Jupyter environment to save Plotly-generated plots as static images in addition the more typical interactive Plotly plot. The static images are good for use elsewhere. And by combining it commandline/scripting it makes it possible to produce a lot of images without saving them by hand from the interactive form. To do this, it uses Plotly's orca. Learn more about Plotly's orca [here](https://github.com/plotly/orca) and [here](https://plot.ly/python/static-image-export/).


This repo uses an approach alternative to [Mathieu Boudreau's implementation with a Dockerfile](https://github.com/mathieuboudreau/orca-plotly-dockerfile). Here, `requirements.txt` is used for specifying most of the repo-specific dependencies. `postBuild` is uded to handle setting up orca. Additionally, `apt.txt` was used for replacing the first section of the [Mathieu Boudreau's Dockerfile](https://github.com/mathieuboudreau/orca-plotly-dockerfile/blob/master/Dockerfile) to install some critical apt packages. Except for the `postBuild` file these are just lists of needed packages or dependencies, and so they offer a way to more easily customize a repo than editing than a Dockerfile.

-----

## Technical details

*Many thanks to mathieuboudreau for working out using Plotly's orca with the MyBinder.org service.* This section details that as it explains why this repo needs a Dockerfile (or `apt.txt` and `postBuild`) to be binderized for full-featured abilities.  
Everything worked as in [the original demo]((https://twitter.com/Steve_Harborne/status/1133064277445627904)) with simply a repo with a `requirements.txt` file (link to that version is [here](https://github.com/fomightez/gel_image_annotation/tree/4421855f2b3a7d1ea53008456b4393371ec3cb10). However, I wanted to add automatic static image generation of the nice interactive plotly graphs to the workflow as that would automate things further for use of the generated content elsewhere, such as in a lab notebook. It looked like all from [here](https://plot.ly/python/static-image-export/) that all I'd need to do is add plot-orca using conda. I tried it first in an active session and it said it wasn't valid orca installation and listed what normally would be helpful installation directions if I wasn't inside a Binder session. I thought perhaps I just needed to switch to using conda to install, and so I removed the `requirements.txt` file I was using to direct dependency isntallation and tried including `plotly-orca` among the dependencies list in `environment.yml`. However, that resulted in the following:

```bash
Solving environment: ...working... failed

ResolvePackageNotFound:
  - plotly-orca
```

Fixed that build problem by adding `plotly` under the channels in `environment.yml`.  
So now the build ran (working `environment.yml` [here](https://github.com/fomightez/gel_image_annotation/tree/24bf618b43ef1451128868f4d3591efa9549cbdc), but when I tried running the `pio.write_image()` code from [here](https://plot.ly/python/static-image-export/), I was still getting the note about it not being valid plotly orca installation.  
Searching 'environment.yml plotly-orca', the title 'Error to locate Orca - Python - Plotly Forum' caught me eye and lead me to [here](https://community.plot.ly/t/error-to-locate-orca/16729/5) where [the original post](https://community.plot.ly/t/error-to-locate-orca/16729) was exactly what I had seen when I tried using conda inside a Binder session to install it for prototyping. Fortunately, down below that happened to list [mathieuboudreau's comment](https://community.plot.ly/t/error-to-locate-orca/16729/5) about also struggling with this, and I happened to click on [the link](https://github.com/plotly/orca/issues/150#issuecomment-482585518) in his comment and look around. That was a very lucky step because although the comment didn't reference Binder-based use, that is exactly what he was trying to work out as referenced in [the post below](https://github.com/plotly/orca/issues/150#issuecomment-482585956) the initially linked one. And indeed later her was able to work it out [here](https://github.com/plotly/orca/issues/150#issuecomment-483484860). It is apparent from [here](https://github.com/plotly/orca) it is complex and I'm very thankful that it was already worked out.
Actually later when I got the build working from `environment.yml`, it says the following at the bottom of the large segment that starts with saying there wasn't a valid orca installation when trying to the `pio.write_image()` code :
>"[Return code: 127]
/srv/conda/envs/notebook/lib/orca_app/orca: error while loading shared libraries: libgtk-x11-2.0.so.0: cannot open shared object file: No such file or directory
Note: When used on Linux, orca requires an X11 display server, but none was
detected. Please install X11, or configure your system with Xvfb. See
the orca README (https://github.com/plotly/orca) for instructions on using
orca with Xvfb."

That is in line with what mathieuboudreau ended up addressing.

Turns out that adding in `apt.txt` and `postBuild` can replace the additional abilities the Dockerfile was able to bring beyond `requirements.txt`, see [here](https://discourse.jupyter.org/t/using-plotlys-orca-to-generate-static-plots-in-binder-served-sessions/1232/3).Curiously, a library was required, namely `libasound2`, that even the Dockerfile didn't seem to need in order to run orca. Keeping the Dockerfile [here](https://github.com/fomightez/gel_image_annotation), but as a hidden file here since it may be useful for future efforts by myself or others. Especially since quite different approach for the last steps dealing with getting orca ready. In particular, I couldn't find a way to work with `usr/bin` in postBuild (or terminal) without permissions problems even though it seems to work for the Dockerfile. 

----

Click the badge to see a demonstration in a Jupyter notebook with a Python kernel served from MyBinder.org:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/orca-plotly-binderized/master?filepath=index.ipynb)


