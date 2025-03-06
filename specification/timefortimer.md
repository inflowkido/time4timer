# TIME FOR TIMER: SPECIFICATION

## Background

While working on a programming project. It can be helpful to track one's time.

Often this is done to bill clients or to ensure employee productivity. However, even if one is working on their own personal project time tracking is beneficial.

It can help focus one's work and see how long various projects are taking. This can help see what is efficient and what could be improved. It can help the team estimate future work better. It can also help the programmer realize if they are stuck and then take steps to get unstuck.

## Net Gain

While there are benefits, there are also costs. It can be time-consuming to use time tracking. It can break or get in the way of workflow. It can also give a feeling of being judged or evaluated only on efficiency and not quality, given pressure to get things done quickly rather than well - or it can give rise to self consciousness which can slow work down.

So, in order to be useful, it must be easy to use and integrate easily into one's work flow. And the data the tool provides must be used for the benefit of the person whose time is being tracked.

To this end, it seems best if it is a voluntary choice by the programmer to use time tracking.

## Name

The name of the program is "Time for Timer" a reference to the [public service announcements](https://en.wikipedia.org/wiki/Time_for_Timer) of the same name.

Because it is used often, the executable name must be no more than two characters, so it will be called `tt`.

This should also be quick to type because both letters are the same.

## Initial API

### start

`tt start issue`

This will record the issue as being started at the current time.

If start is called without an issue, an error message will be displayed to the user called... and exit with status 1.

If start is called with additional arguments, an error message will be displayed to the user which reads and the program will exit with a status of 1.

If the arguments are correct and an error is encountered while running, a helpful, descriptive error message will be displayed to the user and the program will exit with a status of 2.

If the arguments are correct and runs successfully, no message will be displayed to the user and the program will exit with a status of 0.

Only one issue may be started at a given moment. If `start` is called while an issue is already being time-tracked, an error message will be displayed to the user giving the name of the already tracked issue and the name of the new issue the user wanted start. The progam will exit with a status of 2.

### stop

`tt stop`

This will record the issue as being stopped at the current time.

If stop is called without additional arguments and there is a issue which was previously started it will record the current time. If this is done successfully no message will be displayd to the user and the program will exit with status 0. If an error is encountered during runtime, a helpful, descriptive message will be displayed to the user and the program will exit with status 2.

If there are no issues being timed, an error message will be displayed saying so and the program will exit with status 1.

If stop is called with additional arguments, an error message will be displayed to the user saying that no additional arguments are required and an example of proper usage will be given. The program will exit with status 1.

### error code summary

0 - success
1 - invocation
2 - runtime

## Implementation

### Language

The initial version must be implemented in a language which is available on a fresh install of MacOS Sequoia 15.2. The program must have no external dependencies.

### Persistence

The data must persist and only persist locally without any networking calls.

## Anticipated API

### Parameterizing start/stop time

It's easy to forget to start or stop the timer. We could parameterize these, but then again it deincentivizes remembering to start/stop and should probably be recorded when the parameterized start/stop action took place.

A better solution would be to have such a frictionless way to interact with the timer that starting / stopping will become a natural part of workflow.

So, do not implement this without serious consideration.

### bare `tt` invocation

Maybe this should display the currently running timer or the most recently stopped one?

### listing issues tracked

It would be good to be able to know which issues have been tracked

### listing issue(s) tracked with data

first started, last stopped, duration between these two
sum of all intervals worked on particular issue
ratio of work time to wall clock

could give this for all issues or just one (or more)

what should sorting be? by most recently closed? by total time? by first started?

### color

Should color be used to emphasize or improve legibility. Think this through really carefully and only implement after code is solid, stable.

## Anticipated UI

### iPhone

Could have iphone app

### Linear Integration

Start / stop button right in linear

Post intervals to subissue - maybe when stopped?

### github integration

Embed in commit?

### web page

could see all current issues and the total time for each and start time from there

but really, it's not good practice to have a bunch of issues open at the same time and this seems like it would encourage / support disorganization.

But it raises the question, where should the entry point be? On the command line or in linear?

Well, maybe there should be an xcode integration because the command line isn't everyone's IDE.

So, where is the user working from / going to when they want to start the timer?

It feels like initially it's linear (or whatever project management app they're using), but then it becomes their development environment. So, maybe an iphone app is a good idea?

It feels like this needs to be resolved.

### Linear Integration, really simple

I just realized that I can create a subissue like "Time Tracking" and type "start" or "stop" in a comment and it will automatically have the current timestamp. This is really simple and could be like a mini db for each issue.

Branches should be named like will/pro-11-implement-foo-bar where pro-11 is the name of the issue in Linear.

If one were in a branch and they typed `tt`, if there were no `Time Tracker` subissue, it would create one and post a mesasge to the subissue with `start`.

If there were a `Time Tracker` subissue and the last entry were `start`, it would post a message to the subissue with `stop`.

If there were a `Time Tracker` subissue and the last entry were `stop`, it would post a message to the subissue with `start`.

Basically it's a toggle.

So each repository needs to know which Linear workspace manages its work.

The a branch needs to correspond to the issues it is working on.

And we need some way of storing the credentials for the Linear API.
