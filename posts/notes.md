---
title: Notes
description: Notes taken in threaded-discussion's early design phases. 
date: 2022-03-20
tags:
  - Info
  - Design
layout: layouts/post.njk
---

## Week 11 ##
### Comment Workflow ###
![Comment-workflow-diagram](https://user-images.githubusercontent.com/48635853/160300983-77c89afa-554d-4e28-8648-06e6f9034c39.png)
### Reply Workflow ###
![Reply-userflow-diagram](https://user-images.githubusercontent.com/48635853/160300745-cb69a590-b35b-4a5f-abbd-390a0f993d2f.png)


## Week 10 ##
### Initial Mock-up ###
![mockup](https://user-images.githubusercontent.com/48635853/159184135-4fe54c8c-8fd3-4602-a754-17766fb57065.jpg)

### Details ###

#### Visual Changes ####
1. Add post more visible
2. Padding
3. Visuals-- make everything pretty
4. Seed Propic?
5. Edit/delete/reply
6. Call BE to get comments

#### Backend Changes ####
1. Delete post-main-- content unavliable/replys stay
2. Delete reply== gone from the post-main
3. Update schema
4. Update demo
5. Local Storage-- demo
6. post-main-- UUID
7. comments-- UUID
8. Get all comments

#### Database Schema
[See DBDiagram ER diagram for relational database schema](https://dbdiagram.io/d/623369b20ac038740c529b9c) 
![Diagram Image](https://i.imgur.com/mFoLAaT.png)

### Questions ###
- What is the best way to tie comments to each other in the database?
- What can we use from the Nikki's work vs. what will we need to reinvent? 
### Next Steps ###
- Continue examining Nikki's code to determine what can/should be used in our work.
- Begin fledging out design and initial backend.