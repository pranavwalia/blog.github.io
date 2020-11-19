---
layout: post
title: The ONLY Poker Books Worth Reading
categories: [Poker Strategy, Book Reviews]
tags: [Poker,Book Reviews,GTO]
fullview: false
usemathjax: true
comments: false
---

One of the trickiest parts about improving as a Poker player is finding high quality learning resources. There are numerous successful players over the years who have written books on their approaches to the game, yet Poker evolves so quickly that these books are often outdated within a few years. 

During my time playing at [Encore in Boston](https://www.encorebostonharbor.com/), I came across many older gentleman who were poker book junkies. They had read dozens of strategy books yet still struggled to beat relatively easy live games. This is because poker books that actually give quality information are very rare. Additionally, these books are extremely technical and often scare away the mathematically illiterate.

In this article I will review the few and only books I would ever recommend reading if you want to become a winning player.

### [Modern Poker Theory](https://www.amazon.com/Modern-Poker-Theory-unbeatable-principles/dp/1909457892) by Michael Acevedo 

I genuinely cannot say enough good things about this book. It is a culmination of the best parts of every poker book I've ever read and it's backed by rigorous research in [PioSolver](https://www.piosolver.com/). The author has experienced significant success on the tournament circuit both live and online and has a background as a financial analyst and mathematician.

This book bridges theoretical analysis with a grounding in practical hand examples without becoming just another hand review book.

This book is primarily geared towards MTT's and will be most useful if you are used to playing poker at shorter stack depths. As a cash game player, I still found this book extremely useful as he approaches the game from a formal context grounded in Game Theory.

In this book, you will learn the following

- Fundamental game theory concepts
- How to classify ranges as condensed, polarized, capped/uncapped based on various situations
- The relationship between range polarization and bet size
- How to classify various hands into equity buckets and build a strategy for all your holdings
- How to analyze complex data and outputs from solvers in order to execute GTO lines

It is worth noting that this book alone won't leave you walking away as a significantly better player, but it will give you the background knowledge to approach the game like a pro.

### [Applications of No Limit Hold'em](https://www.amazon.com/Applications-No-Limit-Hold-Matthew-Janda/dp/1880685558/ref=sr_1_1?dchild=1&keywords=applications+of+no+limit+holdem&qid=1605807752&s=books&sr=1-1) by Matthew Janda

Applications of No-limit Holdem is considered a classic and is an essential read for anyone seeking to become a competent player. I consider myself extraordinarily lucky to have read this book early on in my poker journey. It is worth noting that while this book has aged extraordinarily well, there are a few aspects of it that are outdated.

1. Preflop Ranges: The original preflop ranges in this book were constructed based on frequencies and manual calculations. In the age of solvers, you are better off using ranges constructed from sims.
2. Hand Reviews Chapter: I would recommend skipping the hand reviews chapter at the end of the book since modern solvers have revealed flaws in Matthew's range construction.

This book formed the back-bone of Doug Polk's strategy and guided much of his analysis. Doug Polk at the height of his career was considered the very best heads up no limit player in the world after beating Ben Sulsky. If you plan on going through this book I would recommend a slow read and to carefully work through all the equations and examples. This will result in a strong foundational knowledge of poker theory which you will be able to build on very rapidly. Applications of No Limit Hold'em can be a daunting read and is theoretically intensive but is absolutely necessary to developing a background in GTO play.

###  [Expert Heads Up No Limit Hold'em](https://www.amazon.com/Expert-Heads-Limit-Holdem-Exploitative/dp/1904468942/ref=sr_1_1?dchild=1&keywords=expert+heads+up+no+limit+hold%27em&qid=1605809356&s=books&sr=1-1) by Will Tipton

Will Tipton has become sort of a cult icon in the Poker Theory community. He was the very first person to create a [weighted flop subset representation](https://www.piosolver.com/blogs/news/62725637-choosing-a-subset-of-flops-to-represent-the-whole-game) of the game and even released a package of [video tutorials](https://husng.com/content/will-tipton-video-pack-0) with his book that walk through analyzing toy games in [Gambit](gambit-project.org/). Many concepts in the book were completely foreign to most players in the community back in 2012. Additionally, Tipton brings the advantage of his background in theoretical computer science which allows him to rigorously formalize his ideas. 

Some of my favorite lessons from the book are:

- Thinking of expected value in terms of the overall game tree
- Proper definition of maximally exploitative strategies
- How iterative exploitation leads to [nash equilibria](https://en.wikipedia.org/wiki/Nash_equilibrium)
- How turn and river runouts influence equity distributions
- Range distributions on various board structures

It is worth noting that the title of this book is misleading. This book is extremely useful for ALL poker players, not just heads up players. Although, this is the style Will is most known for specializing in.

### [Expert Heads Up No Limit Hold'em Volume 2](https://www.amazon.com/Expert-Heads-Limit-Holdem-Play/dp/1909457035/ref=sr_1_3?crid=3MW6AB8TPNCVS&dchild=1&keywords=expert+heads+up+no+limit+hold%27em&qid=1605810277&sprefix=expert+heads+up+no+limi%2Caps%2C164&sr=8-3) by Will Tipton

Expert heads up No Limit Hold'em is slightly more practical than the first book as it applies his earlier ideas to multi-street situations. This is a welcome contrast to the first volume which focuses primarily on preflop play and turn/river scenarios. The book brings more nebulous concepts down to earth. As a Computer Scientist, I enjoyed this book simply for its mathematical elegance however, I still believe the concepts will hold value for many players. The book also comes with a [video pack](https://www.dandbpoker.com/video/experthunlhe) where Tipton walks you through building your own poker game tree solver in Python!

### [No Limit Hold'em For Advanced Players: Emphasis on Tough Games](https://www.amazon.com/No-Limit-Hold-em-Advanced-Players/dp/1880685590/ref=sr_1_3?dchild=1&keywords=no+limit+holdem+for+advanced+players&qid=1605811195&sr=8-3) by Matthew Janda

Out of all the books on GTO poker, this is likely the most practical. Matthew walks through an array of common spots in the game and explains reasonable lines to take based on analysis in [Poker Snowie](https://www.pokersnowie.com/) and [PioSolver](https://www.piosolver.com/). This book is good for developing overall heuristics for executing GTO strategies at the table. I do not however, think the heuristics are so detailed or advanced that they will necessarily prepare you to beat tough games. That being said, the value in this book is that it is a much easier read than the others and is good for getting your feet wet in GTO.

### [The Grinder's Manual](https://www.amazon.com/Grinders-Manual-Complete-Course-Online-ebook/dp/B01GBFF890) by Peter Clarke

This book is not a theoretically focused book but rather a very pragmatic book on heuristics for executing somewhat solid lines at the table. The strength of this book is that it's focused on 6-max cash games and includes some very useful models and approaches for determining which spots are good to C-bet and how to think through ranges. Additionally the book does a good job of explaining the advantages of being in position.

This book is by far the most beginner friendly book on this list and will lay a great foundation to becoming a winning player. Additionally, the book does an excellent job of covering various HUD stats for effective exploitation of player pool tendencies. 

### [Mathematics of Poker](https://www.amazon.com/Mathematics-Poker-Bill-Chen/dp/1886070253/ref=sxts_sxwds-bia-wc-nc-drs1_0?cv_ct_cx=mathematics+of+poker&dchild=1&keywords=mathematics+of+poker&pd_rd_i=1886070253&pd_rd_r=d2ac7e2c-691a-4541-bcf7-9d34f317d170&pd_rd_w=cNto7&pd_rd_wg=n10De&pf_rd_p=84ce0865-d9ca-42e3-87ed-168be8f93162&pf_rd_r=NC2KGXFY5KM339ZKVZ8R&psc=1&qid=1605811698&s=digital-text&sr=1-1-88388c6d-14b8-4f70-90f6-05ac39e80cc0) by Bill Chen and Jerrod Ankenman

Out of all the books on this list, you would be better of reading this last. It's not that the book itself isn't brilliant, but rather that the math in the book is so difficult and complex for anyone without a few semesters of university math behind them that it isn't worth reading for most players. I thoroughly enjoyed the book and recommended it to many of my friends. Many of them reported not being able to make it through the first few chapters. If you have taken Calculus, Probability and Statistics and perhaps a Game Theory course, you'll get through the book just fine. 

The book is extremely abstracted and generally not applicable to decisions at the table but is an amazing read for those who are fans of mathematics and poker.



