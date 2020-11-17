---
id: 1940
title: Can you use NLP to predict the winner of Love Island? / OP
date: 2019-08-25T19:01:28+00:00
author: empiahanalysis
layout: post
guid: http://empiah-analysis.com/?p=1940
permalink: /?p=1940
publicize_twitter_user:
  - ophipps
timeline_notification:
  - "1566759719"
categories:
  - Other Analysis
  - Python
---
[Love Island](https://www.itv.com/loveisland) was kind of unavoidable&#8230;. if you weren&#8217;t personally watching it, WhatsApp groups or workplaces were full of people talking about the latest goings-on, whether it be a new islander, challenge or the most recent scandal ([scripted or not](https://www.express.co.uk/showbiz/tv-radio/1141554/Love-Island-2019-Is-Love-Island-2019-scripted-set-up-ITV)).

I was one of those that swept up by association &#8211; with my girlfriend the one sure to keep me (somewhat) unwillingly up to date.

Looking on my twitter feed, which is usuall pretty much exclusively finance orientated, I started to see &#8216;#LoveIsland&#8217; creep in, and that gave me an idea.

I wondered if you could predict the winner through these tweets using Natural Langauge Processing.

Up to now I haven&#8217;t had much done to do with machine learning, other than what I have seen at my job, and so this is likely to be part one of an NLP series as I learn the ropes. This also means that this analysis is be all means not as in depth as some other blogs you may have read, and is limited to [TextBlob](https://textblob.readthedocs.io/en/dev/), which I will talk about more later.

## Scraping Tweets

The first thing I need to do before I went off and started the NLP was to actually get some information to run through an algorithm, and obviously this meant sourcing tweets.

I wanted to get a lot of tweets over the duration of the show, and as the normal twitter API limits to the last 7 days I had to use another source.

For this I used a package I found on GitHub which allowed me to get data for the 2 months I needed &#8211; from 31st May to 31st July. I won&#8217;t link to this package in case it breaches any twitter T&C&#8217;s, but the creator did a great job and also answered some of my questions through (ironically) twitter DM&#8217;s.

So, I ran the script using Python (which took literally hours), and resulted in over 1.7m entries. Now it was time to analyse. I used this opportunity to give [Google Colab](https://colab.research.google.com/notebooks/welcome.ipynb#recent=true) a spin, as previously I had only used [Jupyter](https://jupyter.org/) and I wanted to see what all the fuss was about.

So I loaded the data into a dataframe and took a look. From here I had to do a bit of cleaning:

  1. The datetime column was using unix time. This wasn&#8217;t a problem but three zeros were appended to the end, so I had to remove these using the below 
      1. > df[&#8216;time&#8217;] = df[&#8216;time&#8217;].astype(str).str[:-3]  
        > df[&#8216;time&#8217;] = pd.to_datetime(df[&#8216;time&#8217;],unit=&#8217;s&#8217;)

  2. I then looked for any nulls, using the below code. We didn&#8217;t have any issues here. 
      1. > df.drop([&#8216;re_tweeter&#8217;], axis = 1, inplace = True)  
        > df.isnull().sum()

  3. I also created another column called &#8216;date&#8217; that converted the datetime to a pure date format so that I could take a look at the data in different ways 
      1. > df[&#8216;time&#8217;] = pd.to_datetime(df[&#8216;time&#8217;])  
        > df[&#8216;date&#8217;] = df[&#8216;time&#8217;].dt.date

So after the above I wanted to see how many tweets we had by day, to get an understanding if we had any highs/lows or the date function didnt work. To do this I used the following code, and got the resulting output.

> count\_by\_date = df.groupby(&#8216;date&#8217;).size()
> 
> plt.figure(figsize=(15,7))  
> plt.xlabel(&#8216;Date&#8217;)  
> plt.ylabel(&#8216;Count of Tweets&#8217;)  
> plt.plot(count\_by\_date);

<img loading="lazy" class="alignnone size-full wp-image-1944" src="https://empiahanalysis.files.wordpress.com/2019/08/download.png?resize=640%2C297" alt="download" width="640" height="297" data-recalc-dims="1" /> 

I could see from this that the date column seemed to be doing it&#8217;s job, and I didn&#8217;t have any blanks. There was a big spike in the middle, and I put this down to the [Casa Amor](https://www.thesun.co.uk/tvandshowbiz/6635917/love-island-casa-amor-2019/) period that is infamous among fans (I hate that I know that).

The script that I used to collect the tweets also stored the amounts of favourites and reweets, and I thought I would take a look at that too.

<img loading="lazy" class="alignnone size-full wp-image-1946" src="https://empiahanalysis.files.wordpress.com/2019/08/download-1.png?resize=640%2C299" alt="download (1)" width="640" height="299" data-recalc-dims="1" /> 

This seems to match with the tweet data that we had above, with favourites being the main tool for fans to agree with their favourite views on the show.

## Natural Language Processing

It was now time to run the NLP analysis. As mentioned before this is very basic due to my current grasp of the packages, but I plan to expand on this in the future.

As mentioned before, I used [TextBlob](https://textblob.readthedocs.io/en/dev/) to perform this. If you don&#8217;t know about TextBlob it is an extremely easy to use tool which performs sentiment analysis for you. An excerpt from their site can be seen below.

> _TextBlob_ is a Python (2 and 3) library for processing textual data. It provides a simple API for diving into common natural language processing (NLP) tasks such as part-of-speech tagging, noun phrase extraction, sentiment analysis, classification, translation, and more.

The expected output was for each tweet to have a rating for polarity (how positive or negative text is) and subjectivity (you guessed it, how subjective a tweet is).

All I had to do here was run the below code on my dataframe and I was good to go.

> from textblob import TextBlob
> 
> df[&#8216;sentiment&#8217;] = df[&#8216;text&#8217;].apply(lambda tweet: TextBlob(tweet).sentiment)

This is where Google Colab came into its own. My PC couldn&#8217;t quite handle the horsepower, and so I was able to a hosted PC which had 25+GB of RAM which made the job a breeze.

The output from TextBlob was a column appended on the end of my dataframe with the Polarity and Subjectivity comma delimted e.g. (polarity,subjectivity), so to carry on this analysis I wanted to split these into two seperate columns. For this, I ran the following code.

> df[&#8216;sentiment&#8217;] = df[&#8216;sentiment&#8217;].astype(str)  
> split = df[&#8216;sentiment&#8217;].str.split(&#8216;,&#8217;)  
> df[&#8216;polarity&#8217;] = split.apply(lambda x: x[0])  
> df[&#8216;subjectivity&#8217;] = split.apply(lambda x: x[1])

This still contained the brackets, and so I remove them too.

> df[&#8216;polarity&#8217;] = df[&#8216;polarity&#8217;].str[19:]  
> df[&#8216;subjectivity&#8217;] = df[&#8216;subjectivity&#8217;].str[14:-1]

I then saved my new dataframe ready for the next steps.

## Analysis

The first thing I wanted to do was to understand the overall polarity over the period of the show. Polarity is ranked from +1 (strongly positive) to -1 (strongly negative).

> df\_polarity.groupby(df\_polarity.date)[[&#8216;polarity&#8217;]].mean().plot()

<img loading="lazy" class="alignnone size-full wp-image-1948" src="https://empiahanalysis.files.wordpress.com/2019/08/download-2.png?resize=407%2C266" alt="download (2)" width="407" height="266" data-recalc-dims="1" /> 

This showed that tweets about the show were generall positive. I also looked at the median of the polarity by day to see if this painted a different picture.

<img loading="lazy" class="alignnone size-full wp-image-1949" src="https://empiahanalysis.files.wordpress.com/2019/08/download-3.png?resize=407%2C266" alt="download (3)" width="407" height="266" data-recalc-dims="1" /> 

This showed the same trend as I would have expected given the nature of the data and what we are plotting. I will use median going forward so that we can see the mid-point of the opinions, instead of a few really strong positive/negative tweets altering the results.

From here we got into the interesting stuff, looking at this data by day, and by contestant.

To do this, I created a new dataframe for each of the major contestants, simply searching for tweets that contained each of their names. From here, I plotted.

<img loading="lazy" class="alignnone size-full wp-image-1950" src="https://empiahanalysis.files.wordpress.com/2019/08/download-4.png?resize=640%2C318" alt="download (4)" width="640" height="318" data-recalc-dims="1" /> 

So the winner of Love Island was Amber and her partner Greg. I will focus on Amber as she was in the contest from the start, and I also thought that a positive tweet for her near the end would also mean a positive tweet for her partner.

As we can see from the data above, Amber (blue line), had a rocky road. But she did show a clear up trend in the ending days of the show and ended up on top.

The finished up on the 29th July, a few days prior to the end of the data (31st July), and so Jordan&#8217;s spike at the end was post the show ending.

Without going into the show and goings-on of the contestants (unless anyone really really wants me to (please no-one ask)), I wont look at trends over the period.

## Conclusion

This was rather crude analysis and I will look into going more in-depth in the future, but it looks like this worked! You can somewhat predict the winner using NLP! But only in the final few days of the show.

To properly validate this theory it would be best to go back and look at other seasons, but I am not sure I can subject myself to researching names/events any more than I really really have to, I don&#8217;t want Love Island to be my mastermind specialist subject.

As mentioned, this was a quick and dirty implentation of NLP that I will likely revisit using more robust measures in the future. But I hope this was interesting!

&nbsp;

&nbsp;