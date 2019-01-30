---
title: "3D Printing: Basic Engineering"
date: 2019-01-29
thumbnail: "articles/3d_engineering.png"
categories: ["3D Printing"]
tags: ["3D Printing", "Engineering", "Tabletop Gaming"]
draft: false
---

_Late last year (2018) I took the plunge and ordered up a 3D printer to help me with my tabletop gaming (and a few other things). I'd had my eye on one for some time, but they always seemed way too expensive (in excess of $1,000 CAD) and I was unwilling to commit such an amount when I wasn't sure of the benefits. Two things changed my mind: firstly, I did a lot of research into what could and could not be achieved with a sub-$1,000 printer, and secondly the [Creality Ender 3 Pro](https://www.creality3d.cn/creality3d-ender-3-pro-p00251p1.html) hit the market. Specificially, I came across articles and videos from Tom Tullis on his [Tomb of 3D Printed Horrors](https://www.youtube.com/channel/UC5Lbnd97HV3rU98gcwHklzQ) YouTube channel which showed what can be achieved with a relatively cheap 3D printer (~$350 CAD), and so I was sold._
 
 I ordered one from a local supplier, [Spool 3D](https://spool3d.ca/) - and here's my first key point: order and source locally if you can. You can order online, from Amazon or Creality directly, or any number of suppliers, but it's hard to be sure whether you're getting (in this case) a genuine Creality Ender 3 or one of the cheaper knock-offs with power supplies that burn up and cables that catch fire. That's not to say they're all bad, just that you can't be sure. Also, you're more likely to get support from a local supplier as they have more at stake than a distant online retailer and, for the most part, they have first-hand knowledge of the products they sell.

I could have paid $315 CAD and ordered from Amazon, but I chose to pay $350 CAD and ordered from Spool 3D. Turns out to be well worth it because I've been back to them a couple of times now and spoken to them about problems and upgrades, and taken at look at how they do things with their printers. I even got a free Pi camera cable from Richard[^0] because they didn't have one in stock and he gave me one of his. Then I told him where he could get boxes of cheap metric nuts & bolts. You don't get that kind of exchange of ideas with most online suppliers.

On the other hand, they are a wee bit expensive where filament is concerned but I have no qualms ordering that online and risking $20-25.

## Basic Engineering

Online support for 3D printing, and the Ender 3 in particular, is freely available. There are any number of Facebook groups and YouTube channels out there where you can ask questions, get help and show others your successes. That said, I have noticed that in all of these groups I see the same questions being asked over and over again with the same myriad of answers, which can be incredibly frustrating for a lot of the more experienced folks as well as being confusing for any noobs.

> Now, a quick disclaimer. I'm an ex-IBM Customer Engineer (80's and 90's). I've worked on everything from typewriters, typesetters, printers, copiers, retail scanners & terminals and System 34/36/38 to 3080 & 3090 mainframes and IBM PC's, both hardware and software. I've covered the most mechanical items (typewriters) to the pretty-much non-mechanical (PC's). For the last 25+ years I've been a software developer. So, I would say have a fair amount of hands-on engineering experience.

For anyone new to 3D printing (or any form of mechanized manufacturing, for that matter) I'll try to give you some basic engineering pointers that I work by and I hope will make your life easier.

### Understanding, Not Just Knowledge

The training course for the [IBM Selectric Typewriter](https://en.wikipedia.org/wiki/IBM_Selectric_typewriter) back in 1983 was twelve weeks long and it didn't cover much of the kind of problems you get with the machine. What we did do was disassemble a typewriter and then put it back together. I think it had something on the order of 3,500 parts and we had to know what each one did and where it went. We dealt with tolerances of a few thousandths of an inch and rapidly moving parts that could nip a fingertip off if you put it in the wrong place. I remember we had to wear ties (IBM CE's always wore a suit and tie) but had to tuck them in our shirts so that they (and we) didn't get sucked into the machinery and strangled, and we couldn't wear any jewellery for fear of losing a finger. Happy days.

When something didn't work, we had to figure out **WHY** it didn't work. Not by looking it up in a manual or by asking the instructor, but by understanding what it *should* be doing and then figuring out why it *wasn't*. The instructor would help, but they didn't give us the answers, they helped us understand.

>Occasionally, they would also get in 30 minutes before us in the morning and sabotage every machine so that even if we had everything working perfectly the day before it was broken now. As it turns out, exactly like real life once I was in the field.

So, start by learning **HOW** a 3D printer works. Get to the point where you can identify and name each part of the printer and what it's function is. More to the point, try to understand what happens when that part *doesn't* function correctly.

#### Spot Quiz

Go to your (FDM) printer now and point at the following parts, then say out loud what each one does:

1. Nozzle
1. Heat Break
1. Heat Sink
1. Extruder
1. X-Gantry
1. Heated Bed

That's only six of the most important out of about 100 parts on your average printer so if you couldn't get all of them it's time to do some reading, but don't get too paranoid because some printers may not have a particular part. That's fine. It's important to know what your printer has and *doesn't* have.

#### Google is your friend

Whenever a question is asked in an online group, it's inevitable the answer "Jeez dude, could you not just Google the answer, it's right here in the archives from a year ago" will appear somewhere, and it's very likely true. Most of the questions I see asked could be put on an FAQ list of maybe a dozen or so items. 

But, here's the thing: **you can't search for the answer if you don't know what the question is**.

If you don't know your way around your printer and the terms used to describe it's basic parts then you're stuck with Googling for "pointy brass thing gunks up when I print"[^5] or such-like. Once you've learned some basic terms and the names of the different pats of the printer you can search for "clogged nozzle" instead, which yields not only more results but *better* results. You don't have to know everything out of the gate, nobody expects you to, but some basic knowledge will help your online searches and lead to fewer frustrated answers. 

### Know It's Limitations

If you've purchased a sub-$1,000 printer, congratulations, you've probably got a bargain.

Now you need to understand that you have a complex set of low-cost electro-mechanical parts that will be working to micron-level tolerances for several hours a day almost every day (if you run your printer like most folks do) that collectively cost you (probably) less than $300. It's going to break down. It's going to produce some shitty prints. You're going to be spending a lot of your time trying to figure out why. Accept it. Live with it. Learn from it. Above all, try not to get stressed about it. 3D printing is not a plug-and-go consumer activity, it's for hobbyists. That's you, by the way.

Take a deep breath and - I know this is going to be hard - treat every failure as an opportunity to **LEARN**. Going back to my earlier point: when you look at that shitty print, ask yourself "where has this printer deviated from it's optimal functionality". Use those exact words, because they don't include any cursing and focus on how it went wrong rather than why the 3D gods have deserted you and how many dead chickens it's going to cost to win their favor again.

>In military slang there is the term **TITSUP** or Total Inability To Support Usual Performance. When your printer goes TITSUP, ask how, not why.

### Calibration

The day has come, your new 3D printer has arrived, you've taken it out of the box, built it and run the test dog print. It printed perfectly. Now you're trying one of your own prints aaaaand... it's like a bunch of spaghetti crap with blobs all over it. Why?

Part of recognising when your printer is performing sub-optimally is to learn when it is performing optimally and the best way (I've found) to do that is to run through various printer calibrations. Your printer was calibrated to factory settings before it was boxed, which doesn't mean it was calibrated for optimal performance at home - just that everything was set to a standard setting that should work after it's been put togther. That test dog gcode file has been tweaked so that it works well with those factory settings but anything you try to print may not.

I won't go into too much detail, but there are three basic calibrations you'll need to carry out periodically:

#### Printer Mechanics

The mechanical moving parts of the printer will need an initial setup despite the factory settings. For an FDM printer, for example, this will mean running extrusion, XYZ axis motion and bed-levelling (more accurately called tramming) calibrations at the very least. You'll also need to check the printer frame for squareness and any moving parts for slack (ie: rattling loose) or binding (ie: sticking or jamming). These checks should be re-run periodically as the printer wears in normal use.

Now, someone is going to say "but you don't need to do X that often", and they're probably right. I dont *need* to but I think it's good practice - literally - to calibrate on a regular basis. The more often I carry out a procedure, the more practiced I am at it, the better I can perform it when I need to and I can recognize poor calibration when I see it.

For my own part, I start each print-day with a bed level test and adjust while the test is running[^1], briefly check other parts for slack or binding about once a week and run various calibrations about once a month or so - depending on how much I've been printing.

#### GCode Preparation (slicing)

Every time you take an STL file you want to print you're going to be running it through some slicing software to produce the [GCode](https://en.wikipedia.org/wiki/G-code) that controls the printer. That translation involves managing a bewildering number of variables almost all of which can affect the quality of the finished print. The good news is that quite often other folks have already experimented with a particular set of slicer settings for a particular purpose and they'll either be built into the software or available for download as **profiles**.

That said, these profiles are a lot like the factory settings of your printer. They can be great for printing on a [platonic ideal](https://en.wikipedia.org/wiki/Platonic_idealism) printer but not necessarily perfect for your printer. So, once again, try to learn what those slicer settings mean and what they change. Intentionally screw up some of those setting from time to time and see what happens to a standard test print - like the XYZ cube.

#### Filament (or resin) characteristics

All filaments or resins are not the same, darn it. The chemical composition of a filament can affect the temperature you should print at, how quickly you can extrude it, retraction settings, print speed, non-print moves and so on. These characteristics will vary wildly with the different types of filament, but even if you only print with PLA something as inocuous as changing the colour can make a difference[^2].

As with slicer settings, try experimenting from time to time. When you try some new filament it's a good idea to print a [Temperature Tower](https://www.thingiverse.com/thing:2493504) and a [Printer Assessment Test](https://github.com/kickstarter/kickstarter-autodesk-3d) to determine the printing characteristics and optimal settings for the filament **on your printer**.

### Diagnose Methodically

When you do get a problem, like a crappy print or three, you need to exercise some restraint. Your instinct will be to dive in and start changing settings or adjusting things in the belief that when you change everything you *must* fix the problem first time. Believe me, that's really not the case. Chances are you'll only be making things worse. Instead...

1. Consider what variables might be causing the problem (printer mechanics, slicer settings, etc)
1. Change **ONE** variable and re-print *or* run a test print designed to highlight that particular problem[^3]. Sometimes causing a problem or making it worse can help fix it.
1. If it didn't fix it go back to #1

Make a note every time you change something (see below) and be methodical about how you approach the problem. Look for a [Root Cause](https://en.wikipedia.org/wiki/Root_cause_analysis) and not just a causal factor. For example, if your x-axis drive belt is loose you'll get poor alignment, banding and possible layer shifting. Slowing your print speed in the slicer settings may "fix" the problem but it's only a causal factor and not the root cause.

This also emphasizes the importance of having a well-calibrated printer. If your printer *was* performing well and now it's not, you should be asking the question: *What changed?* The answer will probably give you your root cause. Don't be afraid to change something back to its original setting to see if the problem reoccurs. Once you find the [magic switch](http://catb.org/jargon/html/magic-story.html), you'll have solved the problem.

### Don't Mod

If you've done some research you'll probably have come across articles or seen some videos on YouTube with titles like ["35 Must-Have Creality Ender 3 (Pro) Upgrades & Mods in 2019"](https://all3dp.com/1/20-must-creality-ender-3-upgrades-mods/). Big Tip: **Don't install ANY mods right away**. Run the printer with the stock setup for a while - a few days or a few weeks even - and learn to calibrate for optimal performance using that stock setup.

When you do come to install a mod, understand exactly **WHY** you're installing it. What problem are you trying to fix or what are you trying to improve on? Is the mod you're thinking of installing the best way to fix the problem you have? What are your expected results and how are you going to test for them?

Installing too many mods at the same time is like changing multiple settings at the same time: best case you may fix the problem but you'll never know why, worst case you'll introduce another problem or two and you won't know why. In three months operation, I've installed the following mods to my Ender 3:

* A desktop spool holder so that the filament doesn't have to do a ridiculous 180&deg; turn to enter the extruder
* A cable clip so that the hotend cabling doesn't catch on the bed as the two move around
* Clips on the bowden connectors to stop the tube from coming loose
* A back cover on the display so that I don't accidentally damage the electronics
* All metal extruder because the plastic one had already started to wear
* Adding Octoprint because I want to be able to remotely monitor and control the printer

I've not added any bed-levelling sensor, cable chains, stepper motor dampers or smoothers, changed the hot end, changed the cooling fans or ducts or switched to a glass bed. When I think I need to do any of those things, I'll do my research and *maybe* install them. But, for the moment, my prints are coming out just fine so I'm not going to change anything[^6].

### Keep a Notebook

To paraphrase [Adam Savage of Mythbusters](https://en.wikipedia.org/wiki/Adam_Savage): the difference between engineering and screwing around is writing it down.

Keep a notebook. Record your successes and failures and try to note why you think it went right or wrong. When you carry out any calibration, note the original settings, what you changed and what effect it had on your prints. When you print with a new filament, run those print tests and make a note of the settings - optimal temperature, extrusion tweaks, retractions settings, etc. Draw diagrams.

You months from now will thank you from today for having written it all down clearly and concisely[^4].

### Keep Your Mistakes

If I've learned one thing about 3D printing using an FDM printer it's the fact you're going to throw a *lot* of filament away. All those little bits of crap that get printed out before a print, the skirts, brims and supports, and the failed prints.

I keep a box of my failed prints for two reasons: firstly, it's a reminder that things don't always go as planned and I shouldn't get too upset when things go TITSUP (see above). Secondly, I refer back to my notebook and use those notes along with the failed prints to diagnose issues later on.

## Summary

So, that's it. I've not been at the 3D printing game for long but I do have some experience as a hands-on engineer and I have found much of that applies to my new hobby. I hope these notes have been of use to someone out there, and please feel free to disagree and contribute to the discussion.


[^0]: Incidentally, you may want to check out Rich's YouTube Channel, [The First Layer](https://www.youtube.com/channel/UCbqLaOyY9jLPO7oFH-uduNQ/featured).

[^1]: For anyone owning a 3D printer, bed levelling is a very personal matter. Some folks adjust using paper, some use feeler gauges, some prefer to abdicate responsibility to a touch sensor and software. It's also the first answer to the online question "Why is my print so crappy?" Personally, I prefer adjusting the bed by-eye while the test print is running and performing the levelling so often that it becomes second nature to me. Each to his own.

[^2]: Funny story there, but not now.

[^3]: On the Selectric typewriters, we used to diagnose a lot of [2D] print issues by typing the letters "H" and "y" because "H" covered the available print area well and "y" included a descender (the tail of the y). If those two letters worked, then the odds were good all the others would as well. No need to test every letter every time an adjustment was made.

[^4]: Yes, you can use an electronic notebook with photos if you like, but... I've found that there is something very personal and [visceral](https://www.merriam-webster.com/dictionary/visceral) about using a pen and paper. Taking the time to write things out longhand and draw diagrams [actually helps the memory and learning process](https://www.sciencedaily.com/releases/2011/01/110119095458.htm), and it's more fun. Also, by using a bound notebook, you're not so inclined to lose or delete anything.

[^5]: Which actually work surprisingly well, yay Google!

[^6]: Except for maybe some new bed springs 'cos those gold ones just look cool.