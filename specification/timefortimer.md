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

## Specification

### Environment / Assumptions

A repository should know which linear workspace manages its work.

A branch should be named after the code owners handle followed by a slash followed by the issue id and title.

For example:

    will/tim-11-specify-api-for-timefortimer

### API and Behavior

When `tt` is typed

If the issue does not have a subissue called `Time Tracker`, one is created and the message "start" is posted to the subissue.

If the issue does have a subissue called `Time Tracker` and the last message posted is `start`, the message "stop" is posted to the subissue.

If the issue does have a subissue called `Time Tracker` and the last message posted is `stop`, the message "start" is posted to the subissue

If the issue does have a subissue called `Time Tracker` and the last message posted is neither `start` nor `stop` and error is returned.

### Alpha Considerations

For the alpha version, the messages, timestamps and issue id could be written to disk in some way (tsv, json file, sqlite3).

### Future Considerations

We will need some way of storing the credentials for the Linear API. This should be thought through.
