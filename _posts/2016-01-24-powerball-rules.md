---
layout: post
title: Powerball lottery - Rules and patterns of play
---

On January 13 2016, the [Powerball](https://en.wikipedia.org/wiki/Powerball) lottery made the news by reaching a jackpot of $1.5B, the largest in US history. [Lotteries](https://en.wikipedia.org/wiki/Lottery#United_States) are interesting because they are a gambling game used by governments to raise funds without raising taxes. Let's have a closer look at the rules, odds, and profits made by lotteries, using Powerball as an example since it's [one of the lotteries with highest sales](http://nylottery.ny.gov/wps/wcm/connect/e4ce705f-d71d-4c2d-b47f-5ae1368f61e8/annualReport2015_final.pdf?MOD=AJPERES&Annual%20Report).


## Basics

The [official simplified rules](http://www.powerball.com/powerball/pb_howtoplay.asp) stipulate that five white balls are drawn among 69, and one red ball among 26.
The jackpot is won by matching all five white balls in any order and the red Powerball. The jackpot starts at $40M, and increases every drawing  by at least $10M until won. Combined with the minuscule odds of being won, this mechanic makes it possible for the jackpot to become huge.
The match-5 prize, worth $1 million, is won by matching five white balls in any order. 
Consolation prizes, worth $4 to $50k, are won by matching at least three white balls or at least the red Powerball.
Tickets cost $2. Players can buy as many tickets as they want.

Drawings happen twice a week, on Wednesdays and Saturdays. The [boxplot](https://en.wikipedia.org/wiki/Box_plot) below plots the median number of [tickets sold](http://www.lottoreport.com/ticketcomparison.htm) per drawing. Data consists of drawings with jackpots below $200M, from April 13 2013 (right after California joined the Powerball group) to January 20 2016. Drawings sell an average of 14.0 million tickets on Wednesdays, versus 15.4 millions on Saturdays (p=.0001).

![More tickets are sold on weekends than weekdays](/images/powerball_sales_by_day_of_week.png)


## Jackpots predict sales

Ticket sales are very predictable from the jackpot amount. This is shown in the graph below. For jackpots under $300M, the number of tickets sold increases quadratically with the jackpot. Above $300M, we do not have enough data to build a model, but the trend seems logarithmic, probably because ticket sales grow much faster than the jackpot.

![Tickets sold against jackpot amount](/images/powerball_sales_against_jackpot.png)


## Optional features

Power Play is an optional feature that launched in 2001. As of 2015, it multiplies the value of non-jackpot winnings by 2 to 10 by paying an extra $1 per ticket. A wheel determines the multiplier for each drawing (24/43 chance for 2x down to 1/43 for 10x). Interestingly, Power Play used to have a [1x multiplier](https://en.wikipedia.org/wiki/Powerball#1992_Powerball), but it was removed within a year. Why have a bonus that is sometimes not a bonus?

Random picks: Players can choose their 6 numbers themselves, or have the computer pick them randomly. About [70% to 80%](http://www.powerball.com/pb_contact.asp) of purchases are computer picks.


## Annuity vs cash

Jackpot winners can [choose](http://www.powerball.com/powerball/pb_howtoplay.asp) to receive their share of the jackpot immediately through a 30-year [annuity](https://en.wikipedia.org/wiki/Annuity), or immediately in cash. 
When winners choose the cash, they immediately receive the advertised cash amount, which is usually 60-70% the annuity amount. That is why the lottery organizers advertise the jackpot's annuity, and not its cash.

When winners choose the annuity, they immediately receive 1/30th of the cash amount. The organizers invest the rest into [government bonds or securities](http://money.cnn.com/2016/01/14/news/companies/powerball-payouts-winners-annuity-lump-sum/). Every year for 29 years, they sell 1/29th of the bonds and give the proceeds to the winner, with a [5%-interest](http://www.powerball.com/powerball/pb_howtoplay.asp) per year.
Choosing the annuity prevents people from [blowing](http://www.nytimes.com/2016/01/13/upshot/dear-powerball-winner-take-our-advice-and-take-the-annuity.html) [through](http://www.usnews.com/news/articles/2016/01/12/odds-are-15-billion-powerball-winner-will-end-up-bankrupt) all their money quickly. Yet only [one jackpot winner out of 72](http://www.powerball.com/powerball/pb_stories.asp) chose the 30-year annuity from 2011 to 2015.

