---
layout: post
title: Powerball lottery - Rules and patterns of play
---

<p>
On January 13 2016, the <a href="https://en.wikipedia.org/wiki/Powerball">Powerball</a> lottery made the news by reaching a jackpot of $1.5B, the largest in US history. <a href="https://en.wikipedia.org/wiki/Lottery#United_States">Lotteries</a> are interesting because they are a gambling game used by governments to raise funds without raising taxes. Let's have a closer look at the rules, odds, and profits made by lotteries, using Powerball as an example since it's <a href="http://nylottery.ny.gov/wps/wcm/connect/e4ce705f-d71d-4c2d-b47f-5ae1368f61e8/annualReport2015_final.pdf?MOD=AJPERES&Annual%20Report">one of the lotteries with highest sales</a>.
</p>


<h2>Basics</h2>
<p>
The <a href="http://www.powerball.com/powerball/pb_howtoplay.asp">official simplified rules</a> stipulate that five white balls are drawn among 69, and one red ball among 26.
The jackpot is won by matching all five white balls in any order and the red Powerball. The jackpot starts at $40M, and increases every drawing  by at least $10M until won. Combined with the minuscule odds of being won, this mechanic makes it possible for the jackpot to become huge.
The match-5 prize, worth $1 million, is won by matching five white balls in any order. 
Consolation prizes, worth $4 to $50k, are won by matching at least three white balls or at least the red Powerball.
Tickets cost $2. Players can buy as many tickets as they want.
</p><p>
Drawings happen twice a week, on Wednesdays and Saturdays. The <a href="https://en.wikipedia.org/wiki/Box_plot">boxplot</a> below plots the median number of <a href="http://www.lottoreport.com/ticketcomparison.htm">tickets sold</a> per drawing. Data consists of drawings with jackpots below $200M, from April 13 2013 (right after California joined the Powerball group) to January 20 2016. Drawings sell an average of 14.0 million tickets on Wednesdays, versus 15.4 millions on Saturdays (p=.0001).
</p>

![More tickets are sold on weekends than weekdays](/images/powerball_sales_by_day_of_week.png)



<img src="http://i.imgur.com/ZhIpfYU.png" title="More tickets are sold on weekends than weekdays.">

<h2>Jackpots predict sales</h2>
<p>
Ticket sales are very predictable from the jackpot amount. This is shown in the graph below. For jackpots under $300M, the number of tickets sold increases quadratically with the jackpot. Above $300M, we do not have enough data to build a model, but the trend seems logarithmic, probably because ticket sales grow much faster than the jackpot.
</p>

![Tickets sold against jackpot amount](/images/powerball_sales_against_jackpot.png)


<h2>Optional features</h2>
<p>
Power Play is an optional feature that launched in 2001. As of 2015, it multiplies the value of non-jackpot winnings by 2 to 10 by paying an extra $1 per ticket. A wheel determines the multiplier for each drawing (24/43 chance for 2x down to 1/43 for 10x). Interestingly, Power Play used to have a <A href="https://en.wikipedia.org/wiki/Powerball#1992_Powerball">1x multiplier</a>, but it was removed within a year. Why have a bonus that is sometimes not a bonus?
</p><p>
Random picks: Players can choose their 6 numbers themselves, or have the computer pick them randomly. About <a href="http://www.powerball.com/pb_contact.asp">70% to 80%</a> of purchases are computer picks.
</p>
<h2>Annuity vs cash</h2>
<p>
Jackpot winners can <a href="http://www.powerball.com/powerball/pb_howtoplay.asp">choose</a> to receive their share of the jackpot immediately through a 30-year <a href="https://en.wikipedia.org/wiki/Annuity">annuity</a>, or immediately in cash. 
When winners choose the cash, they immediately receive the advertised cash amount, which is usually 60-70% the annuity amount. That is why the lottery organizers advertise the jackpot's annuity, and not its cash.
</p><p>
When winners choose the annuity, they immediately receive 1/30th of the cash amount. The organizers invest the rest into <a href="http://money.cnn.com/2016/01/14/news/companies/powerball-payouts-winners-annuity-lump-sum/">government bonds or securities</a>. Every year for 29 years, they sell 1/29th of the bonds and give the proceeds to the winner, with a <a href="http://www.powerball.com/powerball/pb_howtoplay.asp">5%-interest</a> per year.
Choosing the annuity prevents people from <a href="http://www.nytimes.com/2016/01/13/upshot/dear-powerball-winner-take-our-advice-and-take-the-annuity.html">blowing</a> <a href="http://www.usnews.com/news/articles/2016/01/12/odds-are-15-billion-powerball-winner-will-end-up-bankrupt">through</a> all their money quickly. Yet only <a href="http://www.powerball.com/powerball/pb_stories.asp">one jackpot winner out of 72</a> chose the 30-year annuity from 2011 to 2015.
</p>

