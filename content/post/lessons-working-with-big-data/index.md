---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Lessons from working with large datasets on my Mac"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-24T10:12:11+02:00
lastmod: 2020-04-24T10:12:11+02:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---


Lesson 1: data format makes a huge difference!

Lesson 2: don't optimise your workflow (e.g. your data cleaning process) around work with a small sample of the data you'll eventually use. Start work with the full sample, because chances are you'll encounter problems that require solutions which make some of your code for working with the small sample obsolete.

