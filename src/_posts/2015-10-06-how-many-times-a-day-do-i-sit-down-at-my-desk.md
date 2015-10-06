---
layout: post
title: "How many times a day do I sit down at my desk"
comments: true
---

Since September 21, I record every day when I'm (and when I'm not) seated at
my desk. I'm going to conduct this, somewhat weird, experiment during seven or
eight weeks. I would like to known how many times a day do I sit down at my
desk, and also to see if there is some recurring patterns.
I record those data with an arduino linked to a
[Force Sensing Resistor](http://www.interlinkelectronics.com/FSR406.php).
The [code for the arduino](https://github.com/lkdjiin/sit-down)
(along with some photos) is available on Github.

This blog post is a debriefing of the first week of data recording.

<img src="{{site.baseurl}}/public/images/raw.jpg" class="" />

The pressure is recorded with a scale varying from 0 to 1023.
Zero being the absence of pressure and 1023 being the maximum pressure that the
device can measure up. I take a measure every 30 seconds.

On the preceding plot, we can see the raw data for the week. They represent the
whole scale of values. Depending how I'm sitting the device record different
values. The blue points at bottom clearly indicate when I am seated.
After a few trials and errors, I found that 20 is a good threshold to separate
raw data in two categories: *seated* and *not seated*.

Here is the result for the first week:

<table>
<tr>
  <th>Day</th>
  <th>Times seated</th>
</tr>
<tr><td>2015-09-21</td><td>32</td></tr>
<tr><td>2015-09-22</td><td>30</td></tr>
<tr><td>2015-09-23</td><td>33</td></tr>
<tr><td>2015-09-24</td><td>33</td></tr>
<tr><td>2015-09-25</td><td>40</td></tr>
<tr><td>2015-09-26</td><td>26</td></tr>
<tr><td>2015-09-27</td><td>26</td></tr>
</table>

One can visualize the processed data in an interesting way, for example the
Monday ; maroon areas represent when I am seated at my desk (the duration):

<img src="{{site.baseurl}}/public/images/visualize-day.png" class="" />

One can leverage this type of visualization to look at the whole week.
It could be a mean to identify patterns. But this week was special for me
(*I worked also during the weekend, I normally never do this*) so I'm going to
wait for more data before to conclude anything.

<img src="{{site.baseurl}}/public/images/visualize-week.png" class="" />

I will surely write a following, more technical, post to show the R code to
process the data and for the plots.

If you have a similar project (in your head or in the real world) I would
like to hear about it, so leave your comment.
