---
title: 'VIX Correlation to S&P 500 Performance / OP'
date: 2017-05-07T22:44:08+00:00
layout: post
---
One of the posts that did recently was around the correlation between Tube delays in London and the subsequent returns of some major stock indices. Whilst we did find some correlation it is obvious that this is extremely random. As we looked to do some more correlation type exercises there seemed to be one that jumped right out at us, and that was the relationship between the VIX and S&P 500

For those that do not know what the VIX is, please see the following description from the CBOE website:

> The CBOE Volatility Index® (VIX® Index) is considered by many to be the world&#8217;s premier barometer of equity market volatility. The VIX Index is based on real-time prices of options on the S&P 500® Index (SPX) and is designed to reflect investors&#8217; consensus view of future (30-day) expected stock market volatility. The VIX Index is often referred to as the market&#8217;s &#8220;fear gauge&#8221;.

It has been in the news a lot recently as we are going through a period of low volatility that some experts are saying it due to complacency &#8211; we thought that it would be interesting to see if the low level of the VIX has any bearing on future returns of the S&P 500.

It is important to say here that I am just using very basic calculations and have put this together purely because it is something that interests me. If this was of any use I am sure a lot of people that are a lot more intelligent that me would have written about it or would be trading off the back of it.

The data that I am using is the VIX and S&P 500 daily close from the period of 2nd Jan 1990 &#8211; 4th May 2017 which can be sourced from the internet for free (if you would like this data let me know and I can send it over). What I have done is calculated the average VIX return over this period and have flagged any daily close that is below 75% of the average. The reason I am doing this is so we get numbers that are significantly below what is typically expected, which would signify low volatility.

After I have flagged the days of volatility below 75% of the average, I have narrowed the data down to where there has been 50 consecutive trading days going the same way. I hope you are all still with me here.

The reason that I have set a marker (50 days) is so that at close of business on the 50th day, an algorithm could place a trade.

Lastly, the numbers in the row at the bottom of the charts below show the bias of positive vs negative returns. If there were only positive/negative results it would show 100%, and if there was an even number of both positive and negative, it would show 0%. The idea is that the closer it is to 100%, the more of a possible trading opportunity it is. All returns are from the 50th consecutive day, and the day count refers to business days only ( e.g. 5 days=1 week) and if the columns reference more than one day, that is the performance over that whole period (if you invested on the 50th day, what return you would have got after each specific time period).

Below are the results that I found &#8211;  I have not included the dates, but if you want this information please let me know.

<img loading="lazy" class="alignnone size-full wp-image-1413" src="https://empiahanalysis.files.wordpress.com/2017/05/returns-chart2.png?resize=640%2C353" alt="Returns Chart" width="640" height="353" data-recalc-dims="1" /> 

What this data seems to show, is that there is come correlation between 50 day periods of low volatility and future stock returns.

Although the first few periods do not present trading opportunities &#8211; the last 3 periods seem to indicate that following 50 days of low volatility, is relatively high chance that you can expect positive gains.  We can see average returns of between 4.1% &#8211; 10.9% if the S&P 500 was bought on the 50th day of trading.

It is worth noting that because the general trend of the stock market is up, you would always be likely to see positive returns if you gave enough time. This may explain the 260 day positive correlation.

As I have said before, I would imagine that if this was any use it would have already been digested by the data-driven trading firms out there, but I hope that you found this interesting.

**Please note that all information is provided for information purposes only and we do not warrant its completeness or accuracy. Everything is our own opinion and the data used is subject to change. We do not trade or hold positions in any securities or currencies mentioned in any posts. Any material is not intended to be used when making decisions around the purchase or sale of currencies or securities and we are not liable for any losses incurred as a result of using the information.**

&nbsp;

&nbsp;