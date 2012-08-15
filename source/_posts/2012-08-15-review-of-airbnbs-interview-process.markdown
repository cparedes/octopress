---
layout: post
title: "Review of Airbnb's SRE Interview Process"
date: 2012-08-15 14:40
comments: true
categories: 
- Interview
---

TL;DR: they have a strong design culture, but not a great engineering culture
from what I can tell with the interview process.

It all started with an email with the recruiter - I was immediately interested,
so I replied back, waited a day or two, then was issued the SRE Challenge,
where I was given a box to play around with, and had to solve a typical systems
engineering problem with whatever tools I wanted. I opted for configuring the
system and solving the problem with a combination of Chef, a few Ruby scripts,
and a shell script to get everything all bootstrapped on the box.

After that, I had a phone interview with another SRE, who asked me various sysadmin trivia. After answering his questions somewhat sufficiently, I was called in to fly over to San Francisco for two days, with one day dedicated to technical and soft skills, and the other day dedicated to interviews with the founders.

I didn't get to go on to the second day, I was eliminated after the first round
of in person interviews - a strenuous 4-5 hours worth, but I did not feel like
it was completely representative of my abilities (I'm not saying I'm awesome at
what I do, just that the questions seemed unfair in judging my abilities.)

Note: I'm going to compare a lot of this to my experience with Amazon's
interview process, as I think Amazon's interview process is similar in many
ways, yet I feel that Amazon's interview process is way more realistic than
Airbnb's.

Much of the questions were even more trivia and vocabulary. There was an
awesome algorithms question that was meant to see how I broke apart the
problem, but I felt like there was too much hand holding when I was trying to
discover a solution to the problem. Amazon's interviews usually have someone
write a ton of code or diagrams on the board before anyone asks any questions -
it's to discover the person's natural thinking process, and ask probing
questions after the solution is naturally discovered.

A few of the questions were downright hostile. I was told by one of the
engineers interviewing me, in no uncertain terms, that "Chef and Puppet
sucked," and was asked what I thought about that. I know what he was getting
at, which was to see if I had any strong opinions on the matter, and to see how
I defended my stance. But this is analogous to going up to a liberal and
saying, "yeah, so, fuck health care and lazy poor people. What do you think
about that shit?" (Aside: I'm a liberal. I'm also a huge supporter of
configuration management systems.) I did ask why he thought they sucked, and
was told that both Chef and Puppet tended to wreck perfectly good systems.  But
so do shell scripts and Ruby programs, given enough recklessness...

I also did notice throughout the entire interview, that there was a lot of
dogma surrounding the kinds of tools that Airbnb uses. I was asked how I could
coordinate actions between many machines, and I told them that I could probably
use Chef to do a lot of that, which was met with a huge red "no" response.  I
then had to play bingo and landed on the "correct answer" of "Zookeeper."
Great, I chose the right tool I guess, though I've always had a different
philosophy about tool choice: use what works, and it's almost always about the
methodology and approach, rather than the tools used.

At the tail end of the interview loop, I was asked how I would improve Airbnb's
site. I gave some suggestions, though I wasn't sure if this was supposed to
touch upon the "inventiveness" quality that Airbnb is looking for. I'm guessing
it was.

They were quick in letting me know whether I would go on to the founder
interviews, which I didn't. Least I got some Airbnb credit at the end. :)

At the end, I wasn't terribly impressed with the engineering organization in
Airbnb - I came away not really wanting to work with Airbnb as a systems
engineer. There was too much emphasis on tool choice/religion, Linux trivia,
and getting the 'right answer' versus solving engineering problems, where
multiple tools might have to be glued together to come up with one of *many*
solutions.

I realize this blog post might end up getting me black balled by Airbnb. My
only response is this: I really do hope the interview process is improved, and
for that to happen, I think the engineering culture probably has to change,
too. In some ways, Amazon's culture can be stultifying, as there can be a lot
of roadblocks before your code can hit production (depending on the team, of
course.) But I think, at least for me, I can appreciate the emphasis on
operations and engineering quality - it's not just the user interface and
smoothness of the site that matters to the customer, but also how fast the
results are delivered to the client (latency, how much load we can sustain),
how often that data is available to the client (high availability), and
sometimes, correctness of that data (system architecture, emphasizing different
parts of the architecture for consistency depending on the problem.)
