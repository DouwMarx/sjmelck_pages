---
title: "Pretty plotting in Python."
publishdate: 2023-01-11T17:18:41+02:00
draft: false
author: Ryan Balshaw
toc: true
tags: ["tag1", "tag2", "tag3"]
categories: ["category1"]
---

## How to get really nice plots

Good day :waving_hand:

The purpose of this explanation is to give an example of how to get really nice plots in Python. This is still in development. At this point in time I used it as a trial post when setting up the blog. Hopefully I will fix it soon (17 April 2023).

Kind regards,

Ryan Balshaw :troll:

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Sit amet commodo nulla facilisi nullam vehicula ipsum a. Ipsum consequat nisl vel pretium lectus quam id leo in. Malesuada bibendum arcu vitae elementum curabitur vitae nunc. Interdum velit euismod in pellentesque. Adipiscing tristique risus nec feugiat in fermentum posuere. Feugiat vivamus at augue eget arcu dictum varius duis. Odio euismod lacinia at quis risus sed vulputate. Id leo in vitae turpis massa sed. Dictum sit amet justo donec enim. Ridiculus mus mauris vitae ultricies leo integer. Duis convallis convallis tellus id interdum velit laoreet id donec.

## Minimal working example:

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Sit amet commodo nulla facilisi nullam vehicula ipsum a. Ipsum consequat nisl vel pretium lectus quam id leo in. Malesuada bibendum arcu vitae elementum curabitur vitae nunc. Interdum velit euismod in pellentesque. Adipiscing tristique risus nec feugiat in fermentum posuere. Feugiat vivamus at augue eget arcu dictum varius duis. Odio euismod lacinia at quis risus sed vulputate. Id leo in vitae turpis massa sed. Dictum sit amet justo donec enim. Ridiculus mus mauris vitae ultricies leo integer. Duis convallis convallis tellus id interdum velit laoreet id donec.

### Did this work?

In this write up, I will demonstrate how to adjust any python plot
to have formatting akin to LaTeX. The first step of this process is
include the code, then figure out how to include mathsjax and then move
on with my life.
```python
from matplotlib import pyplot as plt
import numpy as np


def fix(ax=None, minor_flag=True, flag_3d=True):
    if ax is None:
        ax = plt.gca()

    fig = ax.get_figure()
    # Force the figure to be drawn

    fig.canvas.draw()

    if minor_flag:
        # Remove '\mathdefault' from all minor tick labels
        labels = [
            label.get_text()
            .replace("\\times", "}$.$\\mathdefault{")
            .replace("-", "$\\mathdefault{-}$")
            .replace("−", "$\\mathdefault{-}$")
            for label in ax.get_xminorticklabels()
        ]
        ax.set_xticklabels(labels, minor=True)

        labels = [
            label.get_text()
            .replace("\\times", "}$.$\\mathdefault{")
            .replace("-", "$\\mathdefault{-}$")
            .replace("−", "$\\mathdefault{-}$")
            for label in ax.get_yminorticklabels()
        ]
        ax.set_yticklabels(labels, minor=True)

        if flag_3d:
            labels = [
                label.get_text()
                .replace("\\times", "}$.$\\mathdefault{")
                .replace("-", "$\\mathdefault{-}$")
                .replace("−", "$\\mathdefault{-}$")
                for label in ax.get_zminorticklabels()
            ]
            ax.set_zticklabels(labels, minor=True)

    else:
        # Remove '\mathdefault' from all minor tick labels
        labels = [
            label.get_text()
            .replace("\\times", "}$.$\\mathdefault{")
            .replace("-", "$\\mathdefault{-}$")
            .replace("−", "$\\mathdefault{-}$")
            for label in ax.get_xmajorticklabels()
        ]
        ax.set_xticklabels(labels, minor=False)

        labels = [
            label.get_text()
            .replace("\\times", "}$.$\\mathdefault{")
            .replace("-", "$\\mathdefault{-}$")
            .replace("−", "$\\mathdefault{-}$")
            for label in ax.get_ymajorticklabels()
        ]
        ax.set_yticklabels(labels, minor=False)

        if flag_3d:
            labels = [
                label.get_text()
                .replace("\\times", "}$.$\\mathdefault{")
                .replace("-", "$\\mathdefault{-}$")
                .replace("−", "$\\mathdefault{-}$")
                for label in ax.get_zmajorticklabels()
            ]
            ax.set_zticklabels(labels, minor=False)


fig, ax = plt.subplots(figsize = (10, 6))

x_range = np.linspace(-10, 10, 1000)
ax.plot(x_range, x_range**2, label = r"$y=x^2$")
ax.set_title("Base example (no nice plots)")

ax.legend()
ax.set_xlabel("Record number")
ax.set_ylabel("$y$")

plt.show(block=False)

#Override parameters
plt.rc("mathtext", fontset="cm")
plt.rc("font", family="serif", size=12, serif="cmr10")

fig, ax = plt.subplots(1, 2, figsize = (10, 6))
fig.suptitle("The ideal plot (with and without fix)")
ax = ax.flatten()

x_range = np.linspace(-10, 10, 1000)
ax[0].plot(x_range, x_range**2, label = r"$y=x^2$")
ax[1].plot(x_range, x_range**2, label = r"$y=x^2$")

ax[0].set_title("Figure without fix")
ax[1].set_title("Figure with fix")

for axs in ax:
    axs.legend()
    axs.set_xlabel("$x$")
    axs.set_ylabel("$y$")

#Fix the second figure
fix(ax[1], minor_flag=False, flag_3d=False)

plt.show(block=True)
```

Do equations render?
$$ y = x^2 \( 4 - 3 \) $$
