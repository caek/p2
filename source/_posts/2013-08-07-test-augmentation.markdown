---
layout: post
title: Test Augmentation
permalink: /issue03/test-augmentation/
byline: Ryan Boucher
category: issue03
authors:
    - name: Ryan Boucher
      twitter: distributedlife
      avatar: ryan-avatar.jpg
---
When a system has already been built and no automated tests have been written, automated testing is often brought in for one of three reasons: to improve quality, to reduce time spent testing or to reduce testing headcount. In such an environment I usually see two approaches to automation. The first is a breadth first approach: where we take a end-to-end, high value flows and automate them. The second option is depth first: where we take one system and wrap multiple tests around it before moving on. Any automation attempt is going to face challenges that get into the way of the delivering value in line with the original justification. I'll get onto these for later, as I want to talk about another option. An option often overlooked because it's not pure automation.

Instead of automating an entire test flow or even a system, aim to automate single, small steps. Something simple like 'create a basic order' or 'submit an order'. The testers must able to run these steps in any sequence. These automated steps will be disconnected from each other and can't be chained together without manual intervention. This disconnection and dependence on humans is this approach's strength.

To make it usable by humans; build a lightweight page for our disconnected steps. It could be something as simple as a page of Jenkins jobs, although some nice design wouldn't go astray. You may already know where I'm heading, create three pages of actions: one full of fixtures (givens), one full of actions (whens) and a third with (thens). 

The 'Given I have an order' automation script, when run, goes off and performs its short task. When complete it displays a newly created Order ID. Jotting ID numbers down is something testers have been doing since a bug first crawled out of off-by-one gap. The tester can take that Order ID and plug it into the 'Then the order is complete' step. That step reports a failure because the order isn't complete –it's brand new. But that's what the tester expected –so not a failed test. The tester makes a mental note and moves on. No automated suite goes green, red or is updated in any fashion.

So what? This is just interactive cucumber – reducing testers to being automation glue. I prefer to call them Cyborgs in Test. Part human, part machine, all tester. I jest, I call it test augmentation instead of test automation. The tester can chop and change between manual and automation as she sees fit. The value of the manual tester is their mind. Their ability to detect emergent scenarios. We lose that with automation and we consciously try and get it back with exploratory testing.

-> ⁂ <-

Previously, I mentioned that the all-or-nothing automation approach has to overcome a series of challenges –each more diabolical than the last –to deliver on it's original business justification. I'm going to touch on each of these with the aim of showing how test augmentation can help.

The first of these is interoperability between different automation technologies. Each shift in system under test can require a different automation tool. Java in places, mainframe in others, OpenScript when we can't avoid it. AutoHotKey and Sikuli when all else fails. Interoperability between these technologies isn't trivial and adds a layer of brittleness that only interop knows. This brittleness can erode the teams trust in the test. One way to reduce the impact of interop is to not do it. Give humans the responsibility; they're much more flexible. With test augmentation the tester is managing the state between the various steps.

The longer your test flow the more susceptible you are to change. If you're putting tests around a system, you're wanting change. When a single step in the larger automated flow breaks, the entire flow is failed until that step works again. This failing test is a good thing, it's telling us that either our test is wrong or the system is wrong and we'll change one to make it work again. The downside is that until the test is fixed the entire flow is failing. This may mean that we're missing out on failures after this point. It's also likely that the testers will have to manually re-execute the entire flow –to be sure, before the step gets fixed. With test augmentation the tester can use automation up to the point that the system has changed, shift into 4x4 mode and exercise that new code as in depth as they feel necessary before making use of the automation again.

The next set of challenges are human. When automation is sold as a means to reduce head count. You'll get resistance from the testers to provide support. Why should they help you when you're trying to take their jobs? Test augmentation isn't a way to reduce headcount. It's about giving your testers a helping hand. It's about allowing them to spend more time thinking and less time doing menial repetitive tasks.

The final challenge that I'll cover is that automated tests are opaque. This results in the testers not being able to see and trust what the automated tests do. They are uncertain what gets checked, which paths through the system are taken, whether shortcuts are used, etc. The end result is the testers rerun the automated tests as manual tests. It's still the their neck on the line if the system breaks so they are disinclined to use the automation. By giving testers smaller chunks of automation, they can learn to trust each individual piece.

I recently worked at a client where we did some of this. There was a three day wait for a process to be completed. The testers sent a request to another team of testers who would action it and respond. We automated just that step to be completed in five minutes. That covered the 80% use case. It didn't handle every scenario, but it handled the most common one. Look for steps that get executed frequently or when executed, take a long time to complete.

The downside for this approach is that you don't have an automated suite that you run every night. I don't mind this. I see more value in getting the developers to start writing unit tests for the code their changing. This will run on every commit and when combined with test augmentation is going to give you faster test cycles and better quality.
