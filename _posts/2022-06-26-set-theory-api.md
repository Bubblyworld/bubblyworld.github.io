---
layout: post
title:  "Command-Line Interfaces and the Rabbithole Principle"
date:   3000-06-26 20:34:32 +0200
categories: maths programming
---

The other day I was thinking about Command-Line Interface (CLI) design, and how to create a command-line tool that is as easy to use as possible. Like any programming interface, a CLI is just a frontend for controlling the flow of a messy, complicated mass of code. Since understanding large masses of code is an infuriating full-time occupation, I'm going to simplify the picture a bit and think of code as specifying a _set of possible behaviours_ for your computer:

(TODO image)

Each of these dots represents a different behaviour that your computer might display when the code is executed. This behaviour may depend on a huge number of things, such as the inputs you provide the program, the state of your hard-drive at the time the code is executed, the speed of your internet connection, and who-knows-what-else. The point I'm trying to make here is that understanding the entire space of possible behaviours is completely hopeless once the code is doing anything interesting. Humans - even those of us who write code for a living - just don't work like that.

Programming interfaces try to combat this situation by carving up the space of behaviours into pieces that are (hopefully) easier for humans to understand:

(TODO image)
