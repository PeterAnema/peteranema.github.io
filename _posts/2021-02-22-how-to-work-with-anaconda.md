---
layout: post
title: "How to work with ... Anaconda"
description: "Tips and tricks for working with Anaconda"
date: 2021-02-22
category: Dev
tags: [Python, Anaconda]
---

## Anaconda

## My shortlist

```
conda install dateutils
conda install pyodbc
conda install requests
conda install numpy
conda install scipy
conda install pandas
conda install scikit-learn
conda install geopandas
conda install pillow
conda install opencv
conda install django
conda install flask
```

## Conda Forge

A community-led collection of recipes, build infrastructure and distributions for the conda package manager.

### To install a conda-forge packages

```
conda install -c conda-forge <package-name>
```
or
```
conda config --add channels conda-forge
conda config --set channel_priority strict
conda install <package-name>
```

