---
title: "Packing a Dash App with PyFladesk and PyInstaller"
description: "Turn your Dash App into a stand alone desktop application"
layout: post
toc: true
comments: true
categories: [Python, Plotly, Dash, Flask, Dash Bootstrap Components, PyFladesk, PyInstaller]
---


# Packing Dash Apps into an Executable

The first question is - why bother? This is a very valid question. Dash Apps are built for the web and best run in the browser, hosted on a server. But there are times when a stand alone app can be useful.

Mostly I wanted to see if it is feasible  to create a small desktop GUI based tool (similar to Electron based JS software) with Dash. Turns out, its not hard - I'm sure there are some details to this that could be tuned up but the purpose of this post is to share the basic workflow for packing a dash app.


## Step 1: Build A Dash App

Diamond Drillhole Quality-Assurance Quality-Control (DDH-QAQC) is a small dash app designed to desurvey and composite mining drill hole data as well as provide some basic data visualization for QA/QC purposes. This is a work in progress and hasn't been optimized, as previously mentioned the main goal here was to try packing a dash app.

This App takes advantage of a couple nice Dash add-ons including [dash_router](https://github.com/ericbdaniels/dash_router), [Dash Bootstrap Components](https://dash-bootstrap-components.opensource.faculty.ai/) and [Dash DataTable](https://dash.plotly.com/datatable).

The app itself is used to load some data from a few CSV files and do a bit of math to generate average values with x, y, coordinates. Ultimately, the user will want to compare the composited values to the original values and export the results once satisfied. To do all this, I added a very basic use of sqllite to support all this.

The app code can be seen on the [DDH-QAQC Repo](https://github.com/ericbdaniels/ddh-qaqc/tree/main/App). A few screen shots in the next section..


## Step 2: Running Dash using QtWebEngine with PyFladesk

Under the hood Dash is built on flask, this makes implementing [PyFladesk](https://github.com/smoqadam/PyFladesk) easy. Really its a single line, instead of the usual `app.run_server` use `init_gui(app.server)`. There are a handful of other options to set the screen size, icon, port. Heres a snippet of the current setup:

```python
if __name__ == "__main__":
    from pyfladesk import init_gui

    init_gui(
        app.server,
        port=5000,
        width=1200,
        height=800,
        window_title="DDH-QAQC",
        icon="App/assets/favicon.ico",
        argv=None,
    )
```

Ultimately, its super easy and works great:

![image]({{ site.baseurl }}/images/splash_page.png)
![image]({{ site.baseurl }}/images/upload.png)
![image]({{ site.baseurl }}/images/composite.png)
![image]({{ site.baseurl }}/images/composite_eda.png)


## Step 3: Packaging it all with PyInstaller

There are a few tools available for packaging python into an executable. Used [PyInstaller](https://www.pyinstaller.org/) and I've heard [cx_freeze](https://cx-freeze.readthedocs.io/en/latest/) works well too but its not something I've tried. Creating the executable took a bit of trial and error. For some reason the dash dependencies weren't picked up automatically and had top be included in th `main-dir.spec` file manually:

```python
import os
import site

site_pkgs_dir = site.getsitepackages()[1]
addl_pkgs = ["plotly", "dash_renderer","dash_html_components","dash_bootstrap_components", "dash_core_components", "dash_table"]

a = Analysis(['main.py'],
             pathex=['c:\\code-dev\\ddh-qaqc\\App'],
             binaries=[],
             datas=[(os.path.join(site_pkgs_dir,pkg),pkg) for pkg in addl_pkgs],
```

Also, I ran into some trouble with flask-compress. See [this Stack Overflow question](https://stackoverflow.com/questions/64290390/pyinstaller-executable-cannot-find-flask-compress-distribution-that-is-include ) for the solution. This was copied to the app.py file prior to importing dash.

With all that taken care of, creating an executable that includes a directory full of dependencies works nicely. There is a flag to run PyInstaller and produce a single file but for some reason this simply wasn't working. For now, the directory based solution works fine and is available [here](https://github.com/ericbdaniels/ddh-qaqc/blob/main/ddh-qaqc.tar.gz) should you want to give it a try.


## Conclusion

There are plenty of great ways to create desktop based software, but this approach makes it pretty damn easy - even if its not perfect. If you have a need to make nice looking GUI and don't want to get building a full on React/Electron app Dash with PyFladesk and PyInstaller is an option. Give it a go, would love to see more creative uses of Dash!