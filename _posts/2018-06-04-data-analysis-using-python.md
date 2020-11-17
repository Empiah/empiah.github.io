---
id: 1877
title: 'Data Analysis using Python &#8211; Football Betting / OP'
date: 2018-06-04T22:32:48+00:00
author: empiahanalysis
layout: post
guid: http://empiah-analysis.com/?p=1877
permalink: /?p=1877
publicize_twitter_user:
  - ophipps
timeline_notification:
  - "1528151571"
categories:
  - Football
  - Other Analysis
  - Python
---
The original can be found on GitHub, [here](https://github.com/Empiah/FootballBetting---DAND/blob/master/Betting%20Trends%20in%20Football.ipynb).

<div id="notebook" class="border-box-sizing">
  <div id="notebook-container" class="container">
    <div class="cell border-box-sizing text_cell rendered">
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="Project:-Investigate-a-Dataset---Football-Betting-Analysis">
            Project: Investigate a Dataset &#8211; Football Betting Analysis
          </h1>
          
          <h2 id="Table-of-Contents">
            Table of Contents
          </h2>
          
          <ul>
            <li>
              <a href="#intro">Introduction</a>
            </li>
            <li>
              <a href="#wrangling">Data Wrangling</a>
            </li>
            <li>
              <a href="#eda">Exploratory Data Analysis</a>
            </li>
            <li>
              <a href="#conclusions">Conclusions</a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            &nbsp;
          </p>
          
          <h2 id="Introduction">
            Introduction
          </h2>
          
          <blockquote>
            <p>
              The dataset I will be investigating will be ‘Soccer Database’ (original source on Kaggle). I am using this dataset because I have an interest in football and I am a lifelong Arsenal fan, and also because I was interested in improving the SQL skills that I have learnt whilst taking part in this course.
            </p>
            
            <p>
              My first steps were to download the data and also ‘DB Browser for SQL Lite’, which enabled me to view the data.<br /> After taking a look at the database and getting to grips with the program I decided I wanted to look at betting trends in football. I personally do not bet on football but it is interesting to see how bookmakers may price their odds and if there are any trends.
            </p>
            
            <p>
              I have already talking through the database and SQL query that I have used in my project submission document. The data resulting from the SQL query was saved to csv ready for analysis in Python.
            </p>
            
            <p>
              The goal for the analysis we are about to perform is to answer two questions:
            </p>
            
            <ul>
              <li>
                Do certain bookmakers give better odds than others consistently?¶
              </li>
              <li>
                Are there certain teams that may defy bookmakers consistently?
              </li>
            </ul>
            
            <p>
              I believe that answering these questions will give us some insight into the betting activities over the period chosen and it will help us understand which football teams outperformed their expectations.
            </p>
          </blockquote>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [42]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="o">%</span> <span class="n">matplotlib</span> <span class="n">inline</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            &nbsp;
          </p>
          
          <h2 id="Data-Wrangling">
            Data Wrangling
          </h2>
          
          <blockquote>
            <p>
              As I have mentioned in my project submission document, I tried to clean the data as much as possible using SQL and so I expect the data that I have to be relevatively clean. I will of course perform some inital analysis to ensure that is is ready for further investigation.
            </p>
          </blockquote>
          
          <h3 id="General-Properties">
            General Properties
          </h3>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [43]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'soccer_database_csv.csv'</span><span class="p">)</span>
<span class="c1"># looking at the data to make sure it is clear and agrees with what I pulled from the SQL database</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[43]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <div>
                <table class="dataframe" border="1">
                  <tr style="text-align:right;">
                    <th>
                    </th>
                    
                    <th>
                      country_name
                    </th>
                    
                    <th>
                      league_name
                    </th>
                    
                    <th>
                      season
                    </th>
                    
                    <th>
                      home_team_goal
                    </th>
                    
                    <th>
                      away_team_goal
                    </th>
                    
                    <th>
                      Bet365_Home
                    </th>
                    
                    <th>
                      Bet365_Draw
                    </th>
                    
                    <th>
                      Bet365_Away
                    </th>
                    
                    <th>
                      Ladbrokes_Home
                    </th>
                    
                    <th>
                      Ladbrokes_Draw
                    </th>
                    
                    <th>
                      Ladbrokes_Away
                    </th>
                    
                    <th>
                      WilliamHill_Home
                    </th>
                    
                    <th>
                      WilliamHill_Draw
                    </th>
                    
                    <th>
                      WilliamHill_Away
                    </th>
                    
                    <th>
                      home_team
                    </th>
                    
                    <th>
                      away_team
                    </th>
                  </tr>
                  
                  <tr>
                    <th>
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      6.0
                    </td>
                    
                    <td>
                      12.00
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      5.5
                    </td>
                    
                    <td>
                      12.0
                    </td>
                    
                    <td>
                      1.30
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      11.0
                    </td>
                    
                    <td>
                      Arsenal
                    </td>
                    
                    <td>
                      West Ham United
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      1
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.6
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      2.05
                    </td>
                    
                    <td>
                      3.3
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      1.91
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      Bournemouth
                    </td>
                    
                    <td>
                      Aston Villa
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      2
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.36
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      11.00
                    </td>
                    
                    <td>
                      1.40
                    </td>
                    
                    <td>
                      4.5
                    </td>
                    
                    <td>
                      10.0
                    </td>
                    
                    <td>
                      1.40
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      10.0
                    </td>
                    
                    <td>
                      Chelsea
                    </td>
                    
                    <td>
                      Swansea City
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      3
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.70
                    </td>
                    
                    <td>
                      3.9
                    </td>
                    
                    <td>
                      5.50
                    </td>
                    
                    <td>
                      1.75
                    </td>
                    
                    <td>
                      3.8
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      1.73
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      Everton
                    </td>
                    
                    <td>
                      Watford
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      4
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.4
                    </td>
                    
                    <td>
                      4.2
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.1
                    </td>
                    
                    <td>
                      2.7
                    </td>
                    
                    <td>
                      Leicester City
                    </td>
                    
                    <td>
                      Sunderland
                    </td>
                  </tr>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [44]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span> <span class="c1">#getting an idea as to what the data looks like to see if we can make any predictions</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[44]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <div>
                <table class="dataframe" border="1">
                  <tr style="text-align:right;">
                    <th>
                    </th>
                    
                    <th>
                      home_team_goal
                    </th>
                    
                    <th>
                      away_team_goal
                    </th>
                    
                    <th>
                      Bet365_Home
                    </th>
                    
                    <th>
                      Bet365_Draw
                    </th>
                    
                    <th>
                      Bet365_Away
                    </th>
                    
                    <th>
                      Ladbrokes_Home
                    </th>
                    
                    <th>
                      Ladbrokes_Draw
                    </th>
                    
                    <th>
                      Ladbrokes_Away
                    </th>
                    
                    <th>
                      WilliamHill_Home
                    </th>
                    
                    <th>
                      WilliamHill_Draw
                    </th>
                    
                    <th>
                      WilliamHill_Away
                    </th>
                  </tr>
                  
                  <tr>
                    <th>
                      count
                    </th>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                    
                    <td>
                      760.000000
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      mean
                    </th>
                    
                    <td>
                      1.555263
                    </td>
                    
                    <td>
                      1.167105
                    </td>
                    
                    <td>
                      2.785921
                    </td>
                    
                    <td>
                      4.179961
                    </td>
                    
                    <td>
                      5.027408
                    </td>
                    
                    <td>
                      2.704000
                    </td>
                    
                    <td>
                      4.051342
                    </td>
                    
                    <td>
                      5.017447
                    </td>
                    
                    <td>
                      2.758461
                    </td>
                    
                    <td>
                      3.826645
                    </td>
                    
                    <td>
                      4.940908
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      std
                    </th>
                    
                    <td>
                      1.358950
                    </td>
                    
                    <td>
                      1.147706
                    </td>
                    
                    <td>
                      2.271973
                    </td>
                    
                    <td>
                      1.803000
                    </td>
                    
                    <td>
                      4.714756
                    </td>
                    
                    <td>
                      2.074897
                    </td>
                    
                    <td>
                      1.751469
                    </td>
                    
                    <td>
                      5.292513
                    </td>
                    
                    <td>
                      2.128664
                    </td>
                    
                    <td>
                      1.511267
                    </td>
                    
                    <td>
                      4.901914
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      min
                    </th>
                    
                    <td>
                      0.000000
                    </td>
                    
                    <td>
                      0.000000
                    </td>
                    
                    <td>
                      1.040000
                    </td>
                    
                    <td>
                      3.000000
                    </td>
                    
                    <td>
                      1.080000
                    </td>
                    
                    <td>
                      1.050000
                    </td>
                    
                    <td>
                      2.900000
                    </td>
                    
                    <td>
                      1.100000
                    </td>
                    
                    <td>
                      1.020000
                    </td>
                    
                    <td>
                      2.800000
                    </td>
                    
                    <td>
                      1.080000
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      25%
                    </th>
                    
                    <td>
                      1.000000
                    </td>
                    
                    <td>
                      0.000000
                    </td>
                    
                    <td>
                      1.670000
                    </td>
                    
                    <td>
                      3.375000
                    </td>
                    
                    <td>
                      2.537500
                    </td>
                    
                    <td>
                      1.670000
                    </td>
                    
                    <td>
                      3.300000
                    </td>
                    
                    <td>
                      2.500000
                    </td>
                    
                    <td>
                      1.670000
                    </td>
                    
                    <td>
                      3.100000
                    </td>
                    
                    <td>
                      2.575000
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      50%
                    </th>
                    
                    <td>
                      1.000000
                    </td>
                    
                    <td>
                      1.000000
                    </td>
                    
                    <td>
                      2.150000
                    </td>
                    
                    <td>
                      3.600000
                    </td>
                    
                    <td>
                      3.550000
                    </td>
                    
                    <td>
                      2.100000
                    </td>
                    
                    <td>
                      3.500000
                    </td>
                    
                    <td>
                      3.500000
                    </td>
                    
                    <td>
                      2.150000
                    </td>
                    
                    <td>
                      3.300000
                    </td>
                    
                    <td>
                      3.400000
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      75%
                    </th>
                    
                    <td>
                      2.000000
                    </td>
                    
                    <td>
                      2.000000
                    </td>
                    
                    <td>
                      2.900000
                    </td>
                    
                    <td>
                      4.200000
                    </td>
                    
                    <td>
                      5.500000
                    </td>
                    
                    <td>
                      2.900000
                    </td>
                    
                    <td>
                      4.000000
                    </td>
                    
                    <td>
                      5.500000
                    </td>
                    
                    <td>
                      2.885000
                    </td>
                    
                    <td>
                      3.800000
                    </td>
                    
                    <td>
                      5.500000
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      max
                    </th>
                    
                    <td>
                      10.000000
                    </td>
                    
                    <td>
                      8.000000
                    </td>
                    
                    <td>
                      26.000000
                    </td>
                    
                    <td>
                      17.000000
                    </td>
                    
                    <td>
                      41.000000
                    </td>
                    
                    <td>
                      23.000000
                    </td>
                    
                    <td>
                      19.000000
                    </td>
                    
                    <td>
                      51.000000
                    </td>
                    
                    <td>
                      21.000000
                    </td>
                    
                    <td>
                      17.000000
                    </td>
                    
                    <td>
                      41.000000
                    </td>
                  </tr>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            In this phase we are looking at the data to see if it needs further cleaning. WIth the above feature we are looking to see if there are any extreme results that do not look to follow similiar columns. For example if the average odds for different bookmakers were vastly different this would raise some questions, as odds are typically similiar due to the fact there are only thee outcomes.
          </p>
          
          <p>
            We can immediately see from this descriptive data that the Home side tends to have lower odds than the Away side. We can also see that at least one match has seen 10 home goals in it, and another has 8 away goals &#8211; impressive.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [45]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">shape</span> <span class="c1">#getting an idea as to how much data we are working with</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[45]:
            </div>
            
            <div class="output_text output_subarea output_execute_result">
              <pre>(760, 16)</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsnbsp;[46]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span> <span class="c1">#checking we dont have any missing values</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 760 entries, 0 to 759
Data columns (total 16 columns):
country_name        760 non-null object
league_name         760 non-null object
season              760 non-null object
home_team_goal      760 non-null int64
away_team_goal      760 non-null int64
Bet365_Home         760 non-null float64
Bet365_Draw         760 non-null float64
Bet365_Away         760 non-null float64
Ladbrokes_Home      760 non-null float64
Ladbrokes_Draw      760 non-null float64
Ladbrokes_Away      760 non-null float64
WilliamHill_Home    760 non-null float64
WilliamHill_Draw    760 non-null float64
WilliamHill_Away    760 non-null float64
home_team           760 non-null object
away_team           760 non-null object
dtypes: float64(9), int64(2), object(5)
memory usage: 95.1+ KB
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            The above is a step that lets us confirm that there are no null values that need to be resolved. We identified from the &#8216;shape&#8217; code that this data has 760 rows, so if any of the above had less than 760 results we would have to investigate.
          </p>
          
          <p>
            Looking at the above we can see that we do not have any null values and all are showing 760 rows. Next let’s make some charts to see the distribution of data. If we are seeing a large number of outliers it would be a call to investigate.
          </p>
          
          <p>
            We can also see here the data types.
          </p>
          
          <ul>
            <li>
              We would expect any name variables to show as &#8216;objects&#8217; &#8211; pandas name for a string.
            </li>
            <li>
              Any data about goals would be a integer as it would be an absolute value and could not have decimal points (you cannot score half a goal).
            </li>
            <li>
              Odds would be floats as they would include decimal places.
            </li>
          </ul>
          
          <p>
            The above assumptions hold true in our data, I am happy to move to the next step &#8211; checking the distribution of our data via histograms.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [47]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">12</span><span class="p">));</span> <span class="c1">#plotting some histograms to get some first impressions</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img /><img loading="lazy" class="alignnone size-full wp-image-1896" src="https://empiahanalysis.files.wordpress.com/2018/06/output_10_0.png?resize=640%2C508" alt="output_10_0" width="640" height="508" data-recalc-dims="1" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            This visual representation is really helpful in seeing if there are any obvious errors and getting an idea of what you may find in your analysis. For example if there was a huge amount of games which had 10 goals, or a large amount of games with betting odds at 20 it would be a call to do some analysis to clean the data before we preceded. Looking at the above, the data looks sensible.
          </p>
          
          <blockquote>
            <p>
              There isnt much we didnt already know here, e.g. goals are skewed to right towards one, although we can see that there are more zero values for goals for away teams. We can also see that the home odds (right charts) are maybe slightly more skewed to the right when compared to away odds &#8211; this may show us the bookies are doing a good job, as we saw earlier that the mean amount of goals for the home team is above that of the away team.
            </p>
            
            <p>
              To confirm out suspicion about goals and betting for home teams vs away teams, lets plot some more charts. For the betting odds we will just use Bet365.
            </p>
          </blockquote>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [48]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">home_team_goal</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">'Home Goals'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">away_team_goal</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">'Away Goals'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span><span class="o">=</span><span class="s1">'upper right'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Goals scored Home vs Away'</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img loading="lazy" class="alignnone size-full wp-image-1888" src="https://empiahanalysis.files.wordpress.com/2018/06/download-1.png?resize=378%2C264" alt="download (1)" width="378" height="264" data-recalc-dims="1" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            This graph makes it clear to us that the away goals are more skewed towards 0-2, whilst we can actually see clearly that there are actually more instances where the home teams scores one goal, than the home team not scoring at all. This is also true for the away team, but by a much smaller margin.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [49]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">bins</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="mi"></span><span class="p">,</span> <span class="mf">12.5</span><span class="p">,</span> <span class="mi">15</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">Bet365_Home</span><span class="p">,</span> <span class="n">bins</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">'B365 Home Odds'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">Bet365_Away</span><span class="p">,</span> <span class="n">bins</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">'B365 Away Odds'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span><span class="o">=</span><span class="s1">'upper right'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Bet 365 Odds by Match Outcome'</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img loading="lazy" class="alignnone size-full wp-image-1889" src="https://empiahanalysis.files.wordpress.com/2018/06/download-2.png?resize=378%2C264" alt="download (2)" width="378" height="264" data-recalc-dims="1" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            This histogram has been manipulated and cuts out any odds that are over 12.5 &#8211; this makes the graph more concise and clear. We have also not shown the odds for a draw so the graph is comparable to that of the above.
          </p>
          
          <p>
            We can see that Home odds are more skewed to the right and are concentrated around 1 to 2, whilst the odds for an Away win are more spread out and peak at around 3. This shows us that bookmakers believe that a home win is more likely and therefore want to limit what they want to pay out by offering lower odds.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h3 id="Data-Cleaning---Adding-Columns">
            Data Cleaning &#8211; Adding Columns<a class="anchor-link" href="#Data-Cleaning---Adding-Columns">¶</a>
          </h3>
          
          <blockquote>
            <p>
              As the data I have is already quite clean thanks to the SQL used earlier, and the checks we have performaed above &#8211; I will use this section to add some columns that may give us some more insights in the exploratory phase.
            </p>
          </blockquote>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [50]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="p">[</span><span class="s1">'total_goals'</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">'home_team_goal'</span><span class="p">]</span> <span class="o">+</span> <span class="n">df</span><span class="p">[</span><span class="s1">'away_team_goal'</span><span class="p">]</span>
<span class="c1"># creating a total goals column as this may be useful later on</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [51]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">tail</span><span class="p">()</span> <span class="c1">#just to check that this has been added</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[51]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <div>
                <table class="dataframe" border="1">
                  <tr style="text-align:right;">
                    <th>
                    </th>
                    
                    <th>
                      country_name
                    </th>
                    
                    <th>
                      league_name
                    </th>
                    
                    <th>
                      season
                    </th>
                    
                    <th>
                      home_team_goal
                    </th>
                    
                    <th>
                      away_team_goal
                    </th>
                    
                    <th>
                      Bet365_Home
                    </th>
                    
                    <th>
                      Bet365_Draw
                    </th>
                    
                    <th>
                      Bet365_Away
                    </th>
                    
                    <th>
                      Ladbrokes_Home
                    </th>
                    
                    <th>
                      Ladbrokes_Draw
                    </th>
                    
                    <th>
                      Ladbrokes_Away
                    </th>
                    
                    <th>
                      WilliamHill_Home
                    </th>
                    
                    <th>
                      WilliamHill_Draw
                    </th>
                    
                    <th>
                      WilliamHill_Away
                    </th>
                    
                    <th>
                      home_team
                    </th>
                    
                    <th>
                      away_team
                    </th>
                    
                    <th>
                      total_goals
                    </th>
                  </tr>
                  
                  <tr>
                    <th>
                      755
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1.57
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      6.50
                    </td>
                    
                    <td>
                      1.57
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      6.50
                    </td>
                    
                    <td>
                      1.62
                    </td>
                    
                    <td>
                      3.3
                    </td>
                    
                    <td>
                      7.0
                    </td>
                    
                    <td>
                      Atlético Madrid
                    </td>
                    
                    <td>
                      Valencia CF
                    </td>
                    
                    <td>
                      3
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      756
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      2.38
                    </td>
                    
                    <td>
                      3.1
                    </td>
                    
                    <td>
                      3.1
                    </td>
                    
                    <td>
                      Málaga CF
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                    
                    <td>
                      2
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      757
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.53
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      1.50
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      6.50
                    </td>
                    
                    <td>
                      1.57
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      7.0
                    </td>
                    
                    <td>
                      Athletic Club de Bilbao
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                    
                    <td>
                      3
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      758
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      2.40
                    </td>
                    
                    <td>
                      3.1
                    </td>
                    
                    <td>
                      3.1
                    </td>
                    
                    <td>
                      Granada CF
                    </td>
                    
                    <td>
                      Real Betis Balompié
                    </td>
                    
                    <td>
                      2
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      759
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.4
                    </td>
                    
                    <td>
                      3.2
                    </td>
                    
                    <td>
                      Rayo Vallecano
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                    
                    <td>
                      3
                    </td>
                  </tr>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [52]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">conditions</span> <span class="o">=</span> <span class="p">[</span>
    <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'home_team_goal'</span><span class="p">]</span> <span class="o">==</span> <span class="n">df</span><span class="p">[</span><span class="s1">'away_team_goal'</span><span class="p">]),</span>
    <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'home_team_goal'</span><span class="p">]</span> <span class="o">&gt;</span> <span class="n">df</span><span class="p">[</span><span class="s1">'away_team_goal'</span><span class="p">]),</span>
    <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'home_team_goal'</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">df</span><span class="p">[</span><span class="s1">'away_team_goal'</span><span class="p">])]</span>
<span class="n">choices</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'D'</span><span class="p">,</span> <span class="s1">'H'</span><span class="p">,</span> <span class="s1">'A'</span><span class="p">]</span>
<span class="n">df</span><span class="p">[</span><span class="s1">'result'</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">select</span><span class="p">(</span><span class="n">conditions</span><span class="p">,</span> <span class="n">choices</span><span class="p">)</span> 

<span class="c1">#creates a new column that will give a letter to indicate result of match. H = Home team win, A = Away team win, D = Draw</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [53]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span> <span class="c1"># check that this has added succesfully</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[53]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <div>
                <table class="dataframe" border="1">
                  <tr style="text-align:right;">
                    <th>
                    </th>
                    
                    <th>
                      country_name
                    </th>
                    
                    <th>
                      league_name
                    </th>
                    
                    <th>
                      season
                    </th>
                    
                    <th>
                      home_team_goal
                    </th>
                    
                    <th>
                      away_team_goal
                    </th>
                    
                    <th>
                      Bet365_Home
                    </th>
                    
                    <th>
                      Bet365_Draw
                    </th>
                    
                    <th>
                      Bet365_Away
                    </th>
                    
                    <th>
                      Ladbrokes_Home
                    </th>
                    
                    <th>
                      Ladbrokes_Draw
                    </th>
                    
                    <th>
                      Ladbrokes_Away
                    </th>
                    
                    <th>
                      WilliamHill_Home
                    </th>
                    
                    <th>
                      WilliamHill_Draw
                    </th>
                    
                    <th>
                      WilliamHill_Away
                    </th>
                    
                    <th>
                      home_team
                    </th>
                    
                    <th>
                      away_team
                    </th>
                    
                    <th>
                      total_goals
                    </th>
                    
                    <th>
                      result
                    </th>
                  </tr>
                  
                  <tr>
                    <th>
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      6.0
                    </td>
                    
                    <td>
                      12.00
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      5.5
                    </td>
                    
                    <td>
                      12.0
                    </td>
                    
                    <td>
                      1.30
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      11.0
                    </td>
                    
                    <td>
                      Arsenal
                    </td>
                    
                    <td>
                      West Ham United
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      1
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.6
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      2.05
                    </td>
                    
                    <td>
                      3.3
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      1.91
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      Bournemouth
                    </td>
                    
                    <td>
                      Aston Villa
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      A
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      2
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.36
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      11.00
                    </td>
                    
                    <td>
                      1.40
                    </td>
                    
                    <td>
                      4.5
                    </td>
                    
                    <td>
                      10.0
                    </td>
                    
                    <td>
                      1.40
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      10.0
                    </td>
                    
                    <td>
                      Chelsea
                    </td>
                    
                    <td>
                      Swansea City
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      3
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.70
                    </td>
                    
                    <td>
                      3.9
                    </td>
                    
                    <td>
                      5.50
                    </td>
                    
                    <td>
                      1.75
                    </td>
                    
                    <td>
                      3.8
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      1.73
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      Everton
                    </td>
                    
                    <td>
                      Watford
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      4
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.4
                    </td>
                    
                    <td>
                      4.2
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.1
                    </td>
                    
                    <td>
                      2.7
                    </td>
                    
                    <td>
                      Leicester City
                    </td>
                    
                    <td>
                      Sunderland
                    </td>
                    
                    <td>
                      6
                    </td>
                    
                    <td>
                      H
                    </td>
                  </tr>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [152]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">total_goals</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[152]:
            </div>
            
            <div class="output_text output_subarea output_execute_result">
              <pre>2069</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [157]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">'result'</span><span class="p">)[</span><span class="s1">'total_goals'</span><span class="p">]</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Total Goals by Match Outcome'</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img loading="lazy" class="alignnone size-full wp-image-1894" src="https://empiahanalysis.files.wordpress.com/2018/06/download-7.png?resize=384%2C276" alt="download (7)" width="384" height="276" data-recalc-dims="1" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            The graph above shows us the total amount of goals per match outcome. We can see that draws had the least amount of goals, whilst wins for the side at home had by far the most amount of goals here. This would suggest to us that the home side is likely to score the most amount of goals.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [155]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">'result'</span><span class="p">)</span><span class="o">.</span><span class="n">total_goals</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">unstack</span><span class="p">(</span><span class="mi"></span><span class="p">)</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Count of Match Outcome by Total Goals'</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img loading="lazy" class="alignnone size-full wp-image-1891" src="https://empiahanalysis.files.wordpress.com/2018/06/download-4.png?resize=378%2C282" alt="download (4)" width="378" height="282" data-recalc-dims="1" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            This graph shows us a count of matches and how many goals they had by result. We can see that obviously goals with no goals are all draws, and that the most common is a home draw with 3 goals in it.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h3 id="Initial-Analysis-&-Enhanced-Data-Preperation">
            Initial Analysis & Enhanced Data Preperation<a class="anchor-link" href="#Initial-Analysis-&-Enhanced-Data-Preperation">¶</a>
          </h3>
          
          <blockquote>
            <p>
              Now we have added some columns to the report, I want to make some masks so that we can quickly perform analysis to answer the questions that we pose. I also want to do some quick initial analysis to help us get a rough idea of what the data is showing &#8211; this will help us tailor our questions and make some first impressions.
            </p>
          </blockquote>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [55]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">result_hw</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">result</span> <span class="o">==</span> <span class="s1">'H'</span> <span class="c1"># mask for home win</span>
<span class="n">result_aw</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">result</span> <span class="o">==</span> <span class="s1">'A'</span> <span class="c1"># mask for away win</span>
<span class="n">result_d</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">result</span> <span class="o">==</span> <span class="s1">'D'</span> <span class="c1"># mask for draw</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [56]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">hw_prc</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">result</span><span class="p">[</span><span class="n">result_hw</span><span class="p">]</span><span class="o">.</span><span class="n">count</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span> <span class="c1"># getting a percentage of games that the home team has won</span>
<span class="n">aw_prc</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">result</span><span class="p">[</span><span class="n">result_aw</span><span class="p">]</span><span class="o">.</span><span class="n">count</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span> <span class="c1"># getting a percentage of games that the away team has won </span>
<span class="n">d_prc</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">result</span><span class="p">[</span><span class="n">result_d</span><span class="p">]</span><span class="o">.</span><span class="n">count</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span> <span class="c1"># getting a percentage of games that are drawn </span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [57]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># this will plot a pie chart for us</span>
<span class="n">labels</span> <span class="o">=</span> <span class="s1">'Home_Win'</span><span class="p">,</span> <span class="s1">'Away_Win'</span><span class="p">,</span> <span class="s1">'Draw'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">hw_prc</span><span class="p">,</span> <span class="n">aw_prc</span><span class="p">,</span> <span class="n">d_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mf">0.1</span><span class="p">,</span><span class="mi"></span><span class="p">,</span><span class="mi"></span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Percentage of Club wins per Scenario'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
               <img loading="lazy" class="alignnone size-full wp-image-1897" src="https://empiahanalysis.files.wordpress.com/2018/06/output_20_0.png?resize=356%2C251" alt="output_20_0" width="356" height="251" data-recalc-dims="1" />
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            As expected here, we can see that 45% of the time the home side is winning the matches. We can also see that a draw is the most unlikely to occur.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [58]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">league_pl</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">league_name</span> <span class="o">==</span> <span class="s1">'England Premier League'</span> <span class="c1">#mask to filter English teams</span>
<span class="n">league_bbva</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">league_name</span> <span class="o">==</span> <span class="s1">'Spain LIGA BBVA'</span> <span class="c1">#mask to filter Spanish teams</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [59]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="p">[</span><span class="s1">'home_bet_average'</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'Bet365_Home'</span><span class="p">]</span> <span class="o">+</span> <span class="n">df</span><span class="p">[</span><span class="s1">'Ladbrokes_Home'</span><span class="p">]</span> <span class="o">+</span> <span class="n">df</span><span class="p">[</span><span class="s1">'WilliamHill_Home'</span><span class="p">])</span> <span class="o">/</span> <span class="mi">3</span>
<span class="n">df</span><span class="p">[</span><span class="s1">'away_bet_average'</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'Bet365_Away'</span><span class="p">]</span> <span class="o">+</span> <span class="n">df</span><span class="p">[</span><span class="s1">'Ladbrokes_Away'</span><span class="p">]</span> <span class="o">+</span> <span class="n">df</span><span class="p">[</span><span class="s1">'WilliamHill_Away'</span><span class="p">])</span> <span class="o">/</span> <span class="mi">3</span>
<span class="n">df</span><span class="p">[</span><span class="s1">'draw_bet_average'</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'Bet365_Draw'</span><span class="p">]</span> <span class="o">+</span> <span class="n">df</span><span class="p">[</span><span class="s1">'Ladbrokes_Draw'</span><span class="p">]</span> <span class="o">+</span> <span class="n">df</span><span class="p">[</span><span class="s1">'WilliamHill_Draw'</span><span class="p">])</span> <span class="o">/</span> <span class="mi">3</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            We have created some columns showing us the average of the odds for each match, for each outcome.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [60]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># this will give us a value which shows the average </span>
<span class="n">home_av_odds</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">home_bet_average</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
<span class="n">away_av_odds</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">away_bet_average</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
<span class="n">draw_av_odds</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">draw_bet_average</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [61]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># pltting a bar chart to see the average odds for each scenario</span>
<span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="s1">'Home'</span><span class="p">,</span> <span class="n">home_av_odds</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">'Average Home Odds'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="s1">'Away'</span><span class="p">,</span> <span class="n">away_av_odds</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">'Average Away Odds'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="s1">'Draw'</span><span class="p">,</span> <span class="n">draw_av_odds</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">'Average Draw Odds'</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'Match Outcome'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'Average Odds'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Average Betting Odds by Result Type'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">();</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
               <img loading="lazy" class="alignnone size-full wp-image-1898" src="https://empiahanalysis.files.wordpress.com/2018/06/output_26_0.png?resize=380%2C278" alt="output_26_0" width="380" height="278" data-recalc-dims="1" />
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            We can see the average odds for home games are far lower than the odds for away games and draws. This is interesting as it shows that even though a draw it the most unlikely scenario, the longest odds come from that of an away win.
          </p>
          
          <p>
            These two charts help tell a story of predictions (betting odds) and results.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            &nbsp;
          </p>
          
          <h2 id="Exploratory-Data-Analysis">
            Exploratory Data Analysis
          </h2>
          
          <blockquote>
            <p>
              We have now cleaned the data, added some columns and also created some masks. In addition to this we have also performed some basic visual analysis to understand the data we are looking at.
            </p>
          </blockquote>
          
          <h3 id="Research-Question-1---Do-certain-bookmakers-give-better-odds-than-others-consistently?">
            Research Question 1 &#8211; Do certain bookmakers give better odds than others consistently?
          </h3>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            What we want to do first it to try and understand how many times that certain bookmakers have odds that are the highest out of the three bookmakers for which we have data &#8211; this will help us get an idea of which bookmaker we would want to be using based upon the outcome we believe will occur.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [62]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># Looks for when the highest odds of a team at home equal what the Bet365 are giving </span>
<span class="n">b365H_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Home"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Home"</span><span class="p">,</span> <span class="s2">"WilliamHill_Home"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">Bet365_Home</span>
<span class="n">b365H_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">b365H_max</span><span class="p">)</span>

<span class="c1"># Looks for when the highest odds of a team at home equal what the Ladbrokes are giving </span>
<span class="n">ladbrokesH_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Home"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Home"</span><span class="p">,</span> <span class="s2">"WilliamHill_Home"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">Ladbrokes_Home</span>
<span class="n">ladbrokesH_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">ladbrokesH_max</span><span class="p">)</span>

<span class="c1"># Looks for when the highest odds of a team at home equal what the Willliam Hill are giving </span>
<span class="n">williamhillH_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Home"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Home"</span><span class="p">,</span> <span class="s2">"WilliamHill_Home"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">WilliamHill_Home</span>
<span class="n">williamhillH_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">williamhillH_max</span><span class="p">)</span>


<span class="nb">print</span><span class="p">(</span><span class="n">b365H_max_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">ladbrokesH_max_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">williamhillH_max_count</span><span class="p">)</span> <span class="c1">#here we are just checking that the results are sensible</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>431
259
518
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            We can see that above the values do not total our amount of rows, 760. This indicates that in some rows two bookmakers offer the same odds. This is to be expected as it is common for odds to be close to each other in games with only three scenarios, such as football.
          </p>
          
          <p>
            We will look to still plot the information above into a pie chart, using the total of all three values the denominator to derive the relevant percentages. This will still show us who is consistantly offering better odds in the football matches.
          </p>
          
          <p>
            First of all lets repeat this for the Away games, and Draws. This will let us see if the top bookmaker is the same across all scenarios.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h4 id="This-is-for-the-outcome-of-an-away-win">
            This is for the outcome of an away win<a class="anchor-link" href="#This-is-for-the-outcome-of-an-away-win">¶</a>
          </h4>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [63]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># Looks for when the highest odds of a team playing away equal what the Bet365 are giving </span>
<span class="n">b365A_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Away"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Away"</span><span class="p">,</span> <span class="s2">"WilliamHill_Away"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">Bet365_Away</span>
<span class="n">b365A_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">b365A_max</span><span class="p">)</span>

<span class="c1"># Looks for when the highest odds of a team  playing away equal what the Ladbrokes are giving </span>
<span class="n">ladbrokesA_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Away"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Away"</span><span class="p">,</span> <span class="s2">"WilliamHill_Away"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">Ladbrokes_Away</span>
<span class="n">ladbrokesA_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">ladbrokesA_max</span><span class="p">)</span>

<span class="c1"># Looks for when the highest odds of a team  playing away equal what the Willliam Hill are giving </span>
<span class="n">williamhillA_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Away"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Away"</span><span class="p">,</span> <span class="s2">"WilliamHill_Away"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">WilliamHill_Away</span>
<span class="n">williamhillA_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">williamhillA_max</span><span class="p">)</span>


<span class="nb">print</span><span class="p">(</span><span class="n">b365A_max_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">ladbrokesA_max_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">williamhillA_max_count</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>504
279
383
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h4 id="This-is-for-the-outcome-of-a-draw">
            This is for the outcome of a draw<a class="anchor-link" href="#This-is-for-the-outcome-of-a-draw">¶</a>
          </h4>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [64]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># Looks for when the highest odds of a team playing away equal what the Bet365 are giving </span>
<span class="n">b365D_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Draw"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Draw"</span><span class="p">,</span> <span class="s2">"WilliamHill_Draw"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">Bet365_Draw</span>
<span class="n">b365D_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">b365D_max</span><span class="p">)</span>

<span class="c1"># Looks for when the highest odds of a team  playing away equal what the Ladbrokes are giving </span>
<span class="n">ladbrokesD_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Draw"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Draw"</span><span class="p">,</span> <span class="s2">"WilliamHill_Draw"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">Ladbrokes_Draw</span>
<span class="n">ladbrokesD_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">ladbrokesD_max</span><span class="p">)</span>

<span class="c1"># Looks for when the highest odds of a team  playing away equal what the Willliam Hill are giving </span>
<span class="n">williamhillD_max</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Draw"</span><span class="p">,</span> <span class="s2">"Ladbrokes_Draw"</span><span class="p">,</span> <span class="s2">"WilliamHill_Draw"</span><span class="p">]]</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">WilliamHill_Draw</span>
<span class="n">williamhillD_max_count</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">count_nonzero</span><span class="p">(</span><span class="n">williamhillD_max</span><span class="p">)</span>


<span class="nb">print</span><span class="p">(</span><span class="n">b365D_max_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">ladbrokesD_max_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">williamhillD_max_count</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>664
248
99
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            To make these visualisations a bit clearer &#8211; lets make some pie charts!
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [65]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">home_win_odds_count</span> <span class="o">=</span> <span class="n">b365H_max_count</span> <span class="o">+</span> <span class="n">ladbrokesH_max_count</span> <span class="o">+</span> <span class="n">williamhillH_max_count</span> <span class="c1">#total count of odds values for home</span>
<span class="n">away_win_odds_count</span> <span class="o">=</span> <span class="n">b365A_max_count</span> <span class="o">+</span> <span class="n">ladbrokesA_max_count</span> <span class="o">+</span> <span class="n">williamhillA_max_count</span> <span class="c1">#total count of odds values for away</span>
<span class="n">draw_odds_count</span> <span class="o">=</span> <span class="n">b365D_max_count</span> <span class="o">+</span> <span class="n">ladbrokesD_max_count</span> <span class="o">+</span> <span class="n">williamhillD_max_count</span> <span class="c1">#total count of odds values for a draw</span>

<span class="n">b365H_prc</span> <span class="o">=</span> <span class="n">b365H_max_count</span> <span class="o">/</span> <span class="n">home_win_odds_count</span> <span class="c1">#getting percentage of Bet 365 Home Wins against the total</span>
<span class="n">ladbrokesH_prc</span> <span class="o">=</span> <span class="n">ladbrokesH_max_count</span> <span class="o">/</span> <span class="n">home_win_odds_count</span> <span class="c1">#getting percentage of Ladbrokes Home Wins against the total</span>
<span class="n">williamhillH_prc</span> <span class="o">=</span> <span class="n">williamhillH_max_count</span> <span class="o">/</span> <span class="n">home_win_odds_count</span> <span class="c1">#getting percentage of William Hill Home Wins against the total</span>

<span class="n">b365A_prc</span> <span class="o">=</span> <span class="n">b365A_max_count</span> <span class="o">/</span> <span class="n">away_win_odds_count</span> <span class="c1">#getting percentage of Bet 365 Away Wins against the total</span>
<span class="n">ladbrokesA_prc</span> <span class="o">=</span> <span class="n">ladbrokesA_max_count</span> <span class="o">/</span> <span class="n">away_win_odds_count</span> <span class="c1">#getting percentage of Ladbrokes Away Wins against the total</span>
<span class="n">williamhillA_prc</span> <span class="o">=</span> <span class="n">williamhillA_max_count</span> <span class="o">/</span> <span class="n">away_win_odds_count</span> <span class="c1">#getting percentage of William Hill Away Wins against the total</span>

<span class="n">b365D_prc</span> <span class="o">=</span> <span class="n">b365D_max_count</span> <span class="o">/</span> <span class="n">draw_odds_count</span> <span class="c1">#getting percentage of Bet 365 Draws against the total</span>
<span class="n">ladbrokesD_prc</span> <span class="o">=</span> <span class="n">ladbrokesD_max_count</span> <span class="o">/</span> <span class="n">draw_odds_count</span> <span class="c1">#getting percentage of Ladbrokes Draws against the total</span>
<span class="n">williamhillD_prc</span> <span class="o">=</span> <span class="n">williamhillD_max_count</span> <span class="o">/</span> <span class="n">draw_odds_count</span> <span class="c1">#getting percentage of William Hill Draws against the total</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [66]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">labels</span> <span class="o">=</span> <span class="s1">'Bet365'</span><span class="p">,</span> <span class="s1">'Ladbrokes'</span><span class="p">,</span> <span class="s1">'William_Hill'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">b365H_prc</span><span class="p">,</span> <span class="n">ladbrokesH_prc</span><span class="p">,</span> <span class="n">williamhillH_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mi"></span><span class="p">,</span><span class="mi"></span><span class="p">,</span><span class="mi"></span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Best odds for Home wins per bookmaker'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img /><img loading="lazy" class="alignnone size-full wp-image-1899" src="https://empiahanalysis.files.wordpress.com/2018/06/output_38_0.png?resize=356%2C251" alt="output_38_0" width="356" height="251" data-recalc-dims="1" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            This pie chart has been analysed in the comments down below.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [67]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">labels</span> <span class="o">=</span> <span class="s1">'Bet365'</span><span class="p">,</span> <span class="s1">'Ladbrokes'</span><span class="p">,</span> <span class="s1">'William_Hill'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">b365A_prc</span><span class="p">,</span> <span class="n">ladbrokesA_prc</span><span class="p">,</span> <span class="n">williamhillA_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mi"></span><span class="p">,</span><span class="mi"></span><span class="p">,</span><span class="mi"></span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Best odds for Away wins per bookmaker'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img /><img loading="lazy" class="alignnone size-full wp-image-1900" src="https://empiahanalysis.files.wordpress.com/2018/06/output_39_0.png?resize=356%2C251" alt="output_39_0" width="356" height="251" data-recalc-dims="1" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            This pie chart has been analysed in the comments down below.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [68]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">labels</span> <span class="o">=</span> <span class="s1">'Bet365'</span><span class="p">,</span> <span class="s1">'Ladbrokes'</span><span class="p">,</span> <span class="s1">'William_Hill'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">b365D_prc</span><span class="p">,</span> <span class="n">ladbrokesD_prc</span><span class="p">,</span> <span class="n">williamhillD_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mi"></span><span class="p">,</span><span class="mi"></span><span class="p">,</span><span class="mi"></span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Best odds for Draws per bookmaker'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
               <img loading="lazy" class="alignnone size-full wp-image-1901" src="https://empiahanalysis.files.wordpress.com/2018/06/output_40_0.png?resize=356%2C251" alt="output_40_0" width="356" height="251" data-recalc-dims="1" />
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            From the charts above we can see that the choosing a bookermaker which has the best odds is different for each possible scenario. Bet365 typically gives the best (or odds equal with the best) odds for Draws and Away wins, and William Hill typically gives the best odds for home wins.
          </p>
          
          <p>
            To summarise, it seems that if you want the best odds, it depends on what outcome you are going for!
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h3 id="Research-Question-2---Are-there-certain-teams-that-may-defy-bookmakers-consistently?">
            Research Question 2 &#8211; Are there certain teams that may defy bookmakers consistently?
          </h3>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            Here we are looking to see if there are certain teams that defy the bookmakers.
          </p>
          
          <p>
            We will define &#8216;beating the bookmakers&#8217; as a final outcome happening which has the longest odds (highest number). Becuase Bet 365 seems to have either the best odds, or close to the best, we will just look at their odds.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [69]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># this will create a column that gives us the column name which contains the longest odds</span>
<span class="n">df</span><span class="p">[</span><span class="s1">'longest_odds'</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s2">"Bet365_Home"</span><span class="p">,</span> <span class="s2">"Bet365_Away"</span><span class="p">,</span> <span class="s2">"Bet365_Draw"</span><span class="p">]]</span><span class="o">.</span><span class="n">idxmax</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [70]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># This will remove everything before the underscore e.g the Bet365 prefix</span>
<span class="n">df</span><span class="o">.</span><span class="n">longest_odds</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">longest_odds</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">'_'</span><span class="p">)</span><span class="o">.</span><span class="n">str</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [71]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># This only takes the letter of the column, meaning we can compare directly with the 'result' column</span>
<span class="n">df</span><span class="o">.</span><span class="n">longest_odds</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">longest_odds</span><span class="o">.</span><span class="n">str</span><span class="p">[</span><span class="mi"></span><span class="p">]</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [72]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1"># I will check that this works</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[72]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <div>
                <table class="dataframe" border="1">
                  <tr style="text-align:right;">
                    <th>
                    </th>
                    
                    <th>
                      country_name
                    </th>
                    
                    <th>
                      league_name
                    </th>
                    
                    <th>
                      season
                    </th>
                    
                    <th>
                      home_team_goal
                    </th>
                    
                    <th>
                      away_team_goal
                    </th>
                    
                    <th>
                      Bet365_Home
                    </th>
                    
                    <th>
                      Bet365_Draw
                    </th>
                    
                    <th>
                      Bet365_Away
                    </th>
                    
                    <th>
                      Ladbrokes_Home
                    </th>
                    
                    <th>
                      Ladbrokes_Draw
                    </th>
                    
                    <th>
                      &#8230;
                    </th>
                    
                    <th>
                      WilliamHill_Draw
                    </th>
                    
                    <th>
                      WilliamHill_Away
                    </th>
                    
                    <th>
                      home_team
                    </th>
                    
                    <th>
                      away_team
                    </th>
                    
                    <th>
                      total_goals
                    </th>
                    
                    <th>
                      result
                    </th>
                    
                    <th>
                      home_bet_average
                    </th>
                    
                    <th>
                      away_bet_average
                    </th>
                    
                    <th>
                      draw_bet_average
                    </th>
                    
                    <th>
                      longest_odds
                    </th>
                  </tr>
                  
                  <tr>
                    <th>
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      6.0
                    </td>
                    
                    <td>
                      12.00
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      5.5
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      11.0
                    </td>
                    
                    <td>
                      Arsenal
                    </td>
                    
                    <td>
                      West Ham United
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      1.293333
                    </td>
                    
                    <td>
                      11.666667
                    </td>
                    
                    <td>
                      5.500000
                    </td>
                    
                    <td>
                      A
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      1
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.6
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      2.05
                    </td>
                    
                    <td>
                      3.3
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      Bournemouth
                    </td>
                    
                    <td>
                      Aston Villa
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      1.986667
                    </td>
                    
                    <td>
                      4.000000
                    </td>
                    
                    <td>
                      3.466667
                    </td>
                    
                    <td>
                      A
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      2
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.36
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      11.00
                    </td>
                    
                    <td>
                      1.40
                    </td>
                    
                    <td>
                      4.5
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      10.0
                    </td>
                    
                    <td>
                      Chelsea
                    </td>
                    
                    <td>
                      Swansea City
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      1.386667
                    </td>
                    
                    <td>
                      10.333333
                    </td>
                    
                    <td>
                      4.500000
                    </td>
                    
                    <td>
                      A
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      3
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.70
                    </td>
                    
                    <td>
                      3.9
                    </td>
                    
                    <td>
                      5.50
                    </td>
                    
                    <td>
                      1.75
                    </td>
                    
                    <td>
                      3.8
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      Everton
                    </td>
                    
                    <td>
                      Watford
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      1.726667
                    </td>
                    
                    <td>
                      5.166667
                    </td>
                    
                    <td>
                      3.733333
                    </td>
                    
                    <td>
                      A
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      4
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.4
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.1
                    </td>
                    
                    <td>
                      2.7
                    </td>
                    
                    <td>
                      Leicester City
                    </td>
                    
                    <td>
                      Sunderland
                    </td>
                    
                    <td>
                      6
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.983333
                    </td>
                    
                    <td>
                      3.743333
                    </td>
                    
                    <td>
                      3.333333
                    </td>
                    
                    <td>
                      A
                    </td>
                  </tr>
                </table>
                
                <p>
                  5 rows × 22 columns
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [73]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">result</span> <span class="o">==</span> <span class="n">df</span><span class="o">.</span><span class="n">longest_odds</span> 
<span class="c1">#this will flag as true if the longest_odds and results columns match, showing us its applicable to get the team name</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [74]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[74]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <div>
                <table class="dataframe" border="1">
                  <tr style="text-align:right;">
                    <th>
                    </th>
                    
                    <th>
                      country_name
                    </th>
                    
                    <th>
                      league_name
                    </th>
                    
                    <th>
                      season
                    </th>
                    
                    <th>
                      home_team_goal
                    </th>
                    
                    <th>
                      away_team_goal
                    </th>
                    
                    <th>
                      Bet365_Home
                    </th>
                    
                    <th>
                      Bet365_Draw
                    </th>
                    
                    <th>
                      Bet365_Away
                    </th>
                    
                    <th>
                      Ladbrokes_Home
                    </th>
                    
                    <th>
                      Ladbrokes_Draw
                    </th>
                    
                    <th>
                      &#8230;
                    </th>
                    
                    <th>
                      WilliamHill_Away
                    </th>
                    
                    <th>
                      home_team
                    </th>
                    
                    <th>
                      away_team
                    </th>
                    
                    <th>
                      total_goals
                    </th>
                    
                    <th>
                      result
                    </th>
                    
                    <th>
                      home_bet_average
                    </th>
                    
                    <th>
                      away_bet_average
                    </th>
                    
                    <th>
                      draw_bet_average
                    </th>
                    
                    <th>
                      longest_odds
                    </th>
                    
                    <th>
                      beating_bookies_team
                    </th>
                  </tr>
                  
                  <tr>
                    <th>
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      6.0
                    </td>
                    
                    <td>
                      12.00
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      5.5
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      11.0
                    </td>
                    
                    <td>
                      Arsenal
                    </td>
                    
                    <td>
                      West Ham United
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      1.293333
                    </td>
                    
                    <td>
                      11.666667
                    </td>
                    
                    <td>
                      5.500000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      True
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      1
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.6
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      2.05
                    </td>
                    
                    <td>
                      3.3
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      4.0
                    </td>
                    
                    <td>
                      Bournemouth
                    </td>
                    
                    <td>
                      Aston Villa
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      1.986667
                    </td>
                    
                    <td>
                      4.000000
                    </td>
                    
                    <td>
                      3.466667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      True
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      2
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.36
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      11.00
                    </td>
                    
                    <td>
                      1.40
                    </td>
                    
                    <td>
                      4.5
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      10.0
                    </td>
                    
                    <td>
                      Chelsea
                    </td>
                    
                    <td>
                      Swansea City
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      1.386667
                    </td>
                    
                    <td>
                      10.333333
                    </td>
                    
                    <td>
                      4.500000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      3
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.70
                    </td>
                    
                    <td>
                      3.9
                    </td>
                    
                    <td>
                      5.50
                    </td>
                    
                    <td>
                      1.75
                    </td>
                    
                    <td>
                      3.8
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      5.0
                    </td>
                    
                    <td>
                      Everton
                    </td>
                    
                    <td>
                      Watford
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      1.726667
                    </td>
                    
                    <td>
                      5.166667
                    </td>
                    
                    <td>
                      3.733333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      4
                    </th>
                    
                    <td>
                      England
                    </td>
                    
                    <td>
                      England Premier League
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      3.5
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.4
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.7
                    </td>
                    
                    <td>
                      Leicester City
                    </td>
                    
                    <td>
                      Sunderland
                    </td>
                    
                    <td>
                      6
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.983333
                    </td>
                    
                    <td>
                      3.743333
                    </td>
                    
                    <td>
                      3.333333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                </table>
                
                <p>
                  5 rows × 23 columns
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [94]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span> <span class="p">(</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'longest_odds'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'A'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">==</span> <span class="kc">True</span> <span class="p">)</span> <span class="p">)</span> <span class="p">,</span> <span class="n">df</span><span class="o">.</span><span class="n">away_team</span><span class="p">,</span> <span class="n">df</span><span class="o">.</span><span class="n">beating_bookies_team</span><span class="p">)</span>
<span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span> <span class="p">(</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'longest_odds'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'H'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">==</span> <span class="kc">True</span> <span class="p">)</span> <span class="p">)</span> <span class="p">,</span> <span class="n">df</span><span class="o">.</span><span class="n">home_team</span><span class="p">,</span> <span class="n">df</span><span class="o">.</span><span class="n">beating_bookies_team</span><span class="p">)</span>
<span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span> <span class="p">(</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'longest_odds'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'D'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">==</span> <span class="kc">True</span> <span class="p">)</span> <span class="p">)</span> <span class="p">,</span> <span class="s1">'Draw'</span><span class="p">,</span> <span class="n">df</span><span class="o">.</span><span class="n">beating_bookies_team</span><span class="p">)</span>


<span class="c1">#This code will look at the 'beating_bookies_team' column above, and reassign the value</span>
<span class="c1">#if the Away team had the longest odds it will change to the Away team name</span>
<span class="c1">#if the Home team had the longest odds it will change to teh Home team</span>
<span class="c1">#if a Draw had the longest odds it will change to read 'Draw'</span>
<span class="c1">#if the 'longest_odds' did not match 'result', it wll read the boolean "False"</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [76]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="o">.</span><span class="n">tail</span><span class="p">(</span><span class="mi">100</span><span class="p">)</span> <span class="c1">#checking that this works - using 100 rows to check all versions of the above</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[76]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <div>
                <table class="dataframe" border="1">
                  <tr style="text-align:right;">
                    <th>
                    </th>
                    
                    <th>
                      country_name
                    </th>
                    
                    <th>
                      league_name
                    </th>
                    
                    <th>
                      season
                    </th>
                    
                    <th>
                      home_team_goal
                    </th>
                    
                    <th>
                      away_team_goal
                    </th>
                    
                    <th>
                      Bet365_Home
                    </th>
                    
                    <th>
                      Bet365_Draw
                    </th>
                    
                    <th>
                      Bet365_Away
                    </th>
                    
                    <th>
                      Ladbrokes_Home
                    </th>
                    
                    <th>
                      Ladbrokes_Draw
                    </th>
                    
                    <th>
                      &#8230;
                    </th>
                    
                    <th>
                      WilliamHill_Away
                    </th>
                    
                    <th>
                      home_team
                    </th>
                    
                    <th>
                      away_team
                    </th>
                    
                    <th>
                      total_goals
                    </th>
                    
                    <th>
                      result
                    </th>
                    
                    <th>
                      home_bet_average
                    </th>
                    
                    <th>
                      away_bet_average
                    </th>
                    
                    <th>
                      draw_bet_average
                    </th>
                    
                    <th>
                      longest_odds
                    </th>
                    
                    <th>
                      beating_bookies_team
                    </th>
                  </tr>
                  
                  <tr>
                    <th>
                      660
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      8.50
                    </td>
                    
                    <td>
                      5.50
                    </td>
                    
                    <td>
                      1.33
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      5.25
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.30
                    </td>
                    
                    <td>
                      Rayo Vallecano
                    </td>
                    
                    <td>
                      Real Madrid CF
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      8.166667
                    </td>
                    
                    <td>
                      1.330000
                    </td>
                    
                    <td>
                      5.416667
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      661
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.73
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      5.00
                    </td>
                    
                    <td>
                      1.75
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      4.50
                    </td>
                    
                    <td>
                      Villarreal CF
                    </td>
                    
                    <td>
                      Real Sociedad
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      1.776667
                    </td>
                    
                    <td>
                      4.666667
                    </td>
                    
                    <td>
                      3.583333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      662
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.00
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.40
                    </td>
                    
                    <td>
                      Getafe CF
                    </td>
                    
                    <td>
                      Valencia CF
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      3.100000
                    </td>
                    
                    <td>
                      2.333333
                    </td>
                    
                    <td>
                      3.266667
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      Draw
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      663
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      2.15
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      SD Eibar
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      2.233333
                    </td>
                    
                    <td>
                      3.300000
                    </td>
                    
                    <td>
                      3.233333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      664
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      6
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.04
                    </td>
                    
                    <td>
                      17.00
                    </td>
                    
                    <td>
                      34.00
                    </td>
                    
                    <td>
                      1.05
                    </td>
                    
                    <td>
                      15.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      41.00
                    </td>
                    
                    <td>
                      FC Barcelona
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                    
                    <td>
                      6
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.046667
                    </td>
                    
                    <td>
                      33.666667
                    </td>
                    
                    <td>
                      16.333333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      665
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.50
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      6.50
                    </td>
                    
                    <td>
                      1.50
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      Sevilla FC
                    </td>
                    
                    <td>
                      Real Betis Balompié
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.510000
                    </td>
                    
                    <td>
                      6.083333
                    </td>
                    
                    <td>
                      4.286667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      666
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      UD Las Palmas
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.216667
                    </td>
                    
                    <td>
                      3.300000
                    </td>
                    
                    <td>
                      3.300000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      667
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1.53
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      1.55
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      RC Celta de Vigo
                    </td>
                    
                    <td>
                      Granada CF
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.550000
                    </td>
                    
                    <td>
                      6.000000
                    </td>
                    
                    <td>
                      4.043333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      668
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                    
                    <td>
                      Athletic Club de Bilbao
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      3.300000
                    </td>
                    
                    <td>
                      2.233333
                    </td>
                    
                    <td>
                      3.250000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      669
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.33
                    </td>
                    
                    <td>
                      5.00
                    </td>
                    
                    <td>
                      11.00
                    </td>
                    
                    <td>
                      1.35
                    </td>
                    
                    <td>
                      4.50
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      11.00
                    </td>
                    
                    <td>
                      Atlético Madrid
                    </td>
                    
                    <td>
                      Málaga CF
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.336667
                    </td>
                    
                    <td>
                      10.666667
                    </td>
                    
                    <td>
                      4.666667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      670
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      5.00
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      1.67
                    </td>
                    
                    <td>
                      4.75
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.73
                    </td>
                    
                    <td>
                      Real Sociedad
                    </td>
                    
                    <td>
                      Real Madrid CF
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      4.916667
                    </td>
                    
                    <td>
                      1.690000
                    </td>
                    
                    <td>
                      3.833333
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      671
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      Valencia CF
                    </td>
                    
                    <td>
                      Villarreal CF
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.166667
                    </td>
                    
                    <td>
                      3.433333
                    </td>
                    
                    <td>
                      3.266667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      Villarreal CF
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      672
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                    
                    <td>
                      Getafe CF
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.266667
                    </td>
                    
                    <td>
                      3.200000
                    </td>
                    
                    <td>
                      3.266667
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      673
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.60
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      5.75
                    </td>
                    
                    <td>
                      1.62
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                    
                    <td>
                      SD Eibar
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.606667
                    </td>
                    
                    <td>
                      5.750000
                    </td>
                    
                    <td>
                      3.783333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      674
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      21.00
                    </td>
                    
                    <td>
                      9.00
                    </td>
                    
                    <td>
                      1.13
                    </td>
                    
                    <td>
                      19.00
                    </td>
                    
                    <td>
                      9.50
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.14
                    </td>
                    
                    <td>
                      Real Betis Balompié
                    </td>
                    
                    <td>
                      FC Barcelona
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      20.333333
                    </td>
                    
                    <td>
                      1.133333
                    </td>
                    
                    <td>
                      8.500000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      675
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.00
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                    
                    <td>
                      Sevilla FC
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.316667
                    </td>
                    
                    <td>
                      3.033333
                    </td>
                    
                    <td>
                      3.300000
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      676
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.60
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      1.57
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      5.50
                    </td>
                    
                    <td>
                      Granada CF
                    </td>
                    
                    <td>
                      UD Las Palmas
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.580000
                    </td>
                    
                    <td>
                      5.833333
                    </td>
                    
                    <td>
                      3.866667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      677
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1.85
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      1.83
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      Athletic Club de Bilbao
                    </td>
                    
                    <td>
                      RC Celta de Vigo
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.863333
                    </td>
                    
                    <td>
                      4.176667
                    </td>
                    
                    <td>
                      3.566667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      678
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      2.15
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      Málaga CF
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.183333
                    </td>
                    
                    <td>
                      3.400000
                    </td>
                    
                    <td>
                      3.233333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      679
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.33
                    </td>
                    
                    <td>
                      5.00
                    </td>
                    
                    <td>
                      10.00
                    </td>
                    
                    <td>
                      1.29
                    </td>
                    
                    <td>
                      5.50
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      9.00
                    </td>
                    
                    <td>
                      Atlético Madrid
                    </td>
                    
                    <td>
                      Rayo Vallecano
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.306667
                    </td>
                    
                    <td>
                      9.666667
                    </td>
                    
                    <td>
                      5.333333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      680
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      2.05
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      Real Sociedad
                    </td>
                    
                    <td>
                      Rayo Vallecano
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      3.500000
                    </td>
                    
                    <td>
                      2.050000
                    </td>
                    
                    <td>
                      3.466667
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      681
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.20
                    </td>
                    
                    <td>
                      7.50
                    </td>
                    
                    <td>
                      11.00
                    </td>
                    
                    <td>
                      1.22
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      12.00
                    </td>
                    
                    <td>
                      Real Madrid CF
                    </td>
                    
                    <td>
                      Valencia CF
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.213333
                    </td>
                    
                    <td>
                      11.333333
                    </td>
                    
                    <td>
                      7.000000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      682
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.45
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      2.40
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      Villarreal CF
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.416667
                    </td>
                    
                    <td>
                      3.066667
                    </td>
                    
                    <td>
                      3.100000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      683
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      Getafe CF
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      2.116667
                    </td>
                    
                    <td>
                      3.400000
                    </td>
                    
                    <td>
                      3.433333
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      Draw
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      684
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      SD Eibar
                    </td>
                    
                    <td>
                      Real Betis Balompié
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      2.133333
                    </td>
                    
                    <td>
                      3.366667
                    </td>
                    
                    <td>
                      3.433333
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      Draw
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      685
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.04
                    </td>
                    
                    <td>
                      17.00
                    </td>
                    
                    <td>
                      41.00
                    </td>
                    
                    <td>
                      1.05
                    </td>
                    
                    <td>
                      19.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      34.00
                    </td>
                    
                    <td>
                      FC Barcelona
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.046667
                    </td>
                    
                    <td>
                      42.000000
                    </td>
                    
                    <td>
                      16.333333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      686
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      2.88
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      2.75
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.40
                    </td>
                    
                    <td>
                      Sevilla FC
                    </td>
                    
                    <td>
                      Granada CF
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.810000
                    </td>
                    
                    <td>
                      2.366667
                    </td>
                    
                    <td>
                      3.583333
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      687
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      1.91
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      UD Las Palmas
                    </td>
                    
                    <td>
                      Athletic Club de Bilbao
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      3.933333
                    </td>
                    
                    <td>
                      1.903333
                    </td>
                    
                    <td>
                      3.500000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      688
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.50
                    </td>
                    
                    <td>
                      4.20
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      1.50
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      RC Celta de Vigo
                    </td>
                    
                    <td>
                      Málaga CF
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.480000
                    </td>
                    
                    <td>
                      6.666667
                    </td>
                    
                    <td>
                      4.286667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      689
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      17.00
                    </td>
                    
                    <td>
                      6.50
                    </td>
                    
                    <td>
                      1.20
                    </td>
                    
                    <td>
                      15.00
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.22
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                    
                    <td>
                      Atlético Madrid
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      15.666667
                    </td>
                    
                    <td>
                      1.213333
                    </td>
                    
                    <td>
                      6.000000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      &#8230;
                    </th>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      730
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      1.91
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      Sevilla FC
                    </td>
                    
                    <td>
                      FC Barcelona
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      4.043333
                    </td>
                    
                    <td>
                      1.903333
                    </td>
                    
                    <td>
                      3.500000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      Sevilla FC
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      731
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      UD Las Palmas
                    </td>
                    
                    <td>
                      SD Eibar
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.066667
                    </td>
                    
                    <td>
                      3.766667
                    </td>
                    
                    <td>
                      3.233333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      SD Eibar
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      732
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.44
                    </td>
                    
                    <td>
                      4.50
                    </td>
                    
                    <td>
                      7.50
                    </td>
                    
                    <td>
                      1.50
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      RC Celta de Vigo
                    </td>
                    
                    <td>
                      Getafe CF
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      1.480000
                    </td>
                    
                    <td>
                      7.000000
                    </td>
                    
                    <td>
                      4.276667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      733
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      1.91
                    </td>
                    
                    <td>
                      4.20
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                    
                    <td>
                      Villarreal CF
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      4.286667
                    </td>
                    
                    <td>
                      1.923333
                    </td>
                    
                    <td>
                      3.266667
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      734
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.00
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.50
                    </td>
                    
                    <td>
                      Atlético Madrid
                    </td>
                    
                    <td>
                      Real Madrid CF
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      3.033333
                    </td>
                    
                    <td>
                      2.366667
                    </td>
                    
                    <td>
                      3.216667
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      Draw
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      735
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.38
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      Málaga CF
                    </td>
                    
                    <td>
                      Real Sociedad
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.360000
                    </td>
                    
                    <td>
                      3.200000
                    </td>
                    
                    <td>
                      3.100000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      736
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      Athletic Club de Bilbao
                    </td>
                    
                    <td>
                      Valencia CF
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.333333
                    </td>
                    
                    <td>
                      3.133333
                    </td>
                    
                    <td>
                      3.200000
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      737
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.60
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.80
                    </td>
                    
                    <td>
                      2.50
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.80
                    </td>
                    
                    <td>
                      Granada CF
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      2.573333
                    </td>
                    
                    <td>
                      2.800000
                    </td>
                    
                    <td>
                      3.133333
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      Draw
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      738
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.000000
                    </td>
                    
                    <td>
                      4.000000
                    </td>
                    
                    <td>
                      3.216667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      739
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      Rayo Vallecano
                    </td>
                    
                    <td>
                      Real Betis Balompié
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.150000
                    </td>
                    
                    <td>
                      3.216667
                    </td>
                    
                    <td>
                      3.533333
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      740
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1.14
                    </td>
                    
                    <td>
                      9.00
                    </td>
                    
                    <td>
                      15.00
                    </td>
                    
                    <td>
                      1.14
                    </td>
                    
                    <td>
                      8.50
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      17.00
                    </td>
                    
                    <td>
                      FC Barcelona
                    </td>
                    
                    <td>
                      Rayo Vallecano
                    </td>
                    
                    <td>
                      7
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.150000
                    </td>
                    
                    <td>
                      16.333333
                    </td>
                    
                    <td>
                      8.166667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      741
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      SD Eibar
                    </td>
                    
                    <td>
                      Sevilla FC
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      3.533333
                    </td>
                    
                    <td>
                      2.116667
                    </td>
                    
                    <td>
                      3.266667
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      742
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2.15
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      Getafe CF
                    </td>
                    
                    <td>
                      UD Las Palmas
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.150000
                    </td>
                    
                    <td>
                      3.566667
                    </td>
                    
                    <td>
                      3.133333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      743
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      Villarreal CF
                    </td>
                    
                    <td>
                      RC Celta de Vigo
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.033333
                    </td>
                    
                    <td>
                      3.700000
                    </td>
                    
                    <td>
                      3.366667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      RC Celta de Vigo
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      744
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.08
                    </td>
                    
                    <td>
                      12.00
                    </td>
                    
                    <td>
                      23.00
                    </td>
                    
                    <td>
                      1.10
                    </td>
                    
                    <td>
                      10.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      26.00
                    </td>
                    
                    <td>
                      Real Madrid CF
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.093333
                    </td>
                    
                    <td>
                      25.000000
                    </td>
                    
                    <td>
                      10.333333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      745
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.05
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.05
                    </td>
                    
                    <td>
                      Real Sociedad
                    </td>
                    
                    <td>
                      Atlético Madrid
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      4.066667
                    </td>
                    
                    <td>
                      2.033333
                    </td>
                    
                    <td>
                      3.100000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      746
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.62
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      1.62
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      6.00
                    </td>
                    
                    <td>
                      Valencia CF
                    </td>
                    
                    <td>
                      Málaga CF
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.636667
                    </td>
                    
                    <td>
                      5.833333
                    </td>
                    
                    <td>
                      3.650000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      747
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      2.70
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      2.80
                    </td>
                    
                    <td>
                      2.62
                    </td>
                    
                    <td>
                      3.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.80
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                    
                    <td>
                      Athletic Club de Bilbao
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      2.673333
                    </td>
                    
                    <td>
                      2.783333
                    </td>
                    
                    <td>
                      3.033333
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      Draw
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      748
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      4.20
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                    
                    <td>
                      Granada CF
                    </td>
                    
                    <td>
                      6
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      2.000000
                    </td>
                    
                    <td>
                      4.066667
                    </td>
                    
                    <td>
                      3.183333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      749
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.30
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      2.00
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      Real Betis Balompié
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.033333
                    </td>
                    
                    <td>
                      3.850000
                    </td>
                    
                    <td>
                      3.250000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      750
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1.11
                    </td>
                    
                    <td>
                      10.00
                    </td>
                    
                    <td>
                      19.00
                    </td>
                    
                    <td>
                      1.11
                    </td>
                    
                    <td>
                      10.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      21.00
                    </td>
                    
                    <td>
                      FC Barcelona
                    </td>
                    
                    <td>
                      SD Eibar
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.120000
                    </td>
                    
                    <td>
                      20.333333
                    </td>
                    
                    <td>
                      9.000000
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      751
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.44
                    </td>
                    
                    <td>
                      4.33
                    </td>
                    
                    <td>
                      8.00
                    </td>
                    
                    <td>
                      1.44
                    </td>
                    
                    <td>
                      4.20
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      Sevilla FC
                    </td>
                    
                    <td>
                      Getafe CF
                    </td>
                    
                    <td>
                      5
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.460000
                    </td>
                    
                    <td>
                      7.333333
                    </td>
                    
                    <td>
                      4.176667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      752
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.50
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      UD Las Palmas
                    </td>
                    
                    <td>
                      Villarreal CF
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      3.500000
                    </td>
                    
                    <td>
                      2.166667
                    </td>
                    
                    <td>
                      3.200000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      753
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      1.91
                    </td>
                    
                    <td>
                      3.60
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      1.95
                    </td>
                    
                    <td>
                      RC Celta de Vigo
                    </td>
                    
                    <td>
                      Real Madrid CF
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      3.716667
                    </td>
                    
                    <td>
                      1.903333
                    </td>
                    
                    <td>
                      3.700000
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      754
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      2.63
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.80
                    </td>
                    
                    <td>
                      2.62
                    </td>
                    
                    <td>
                      2.90
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      2.70
                    </td>
                    
                    <td>
                      Levante UD
                    </td>
                    
                    <td>
                      Real Sociedad
                    </td>
                    
                    <td>
                      4
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      2.650000
                    </td>
                    
                    <td>
                      2.766667
                    </td>
                    
                    <td>
                      3.066667
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      755
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1.57
                    </td>
                    
                    <td>
                      3.80
                    </td>
                    
                    <td>
                      6.50
                    </td>
                    
                    <td>
                      1.57
                    </td>
                    
                    <td>
                      3.75
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      Atlético Madrid
                    </td>
                    
                    <td>
                      Valencia CF
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.586667
                    </td>
                    
                    <td>
                      6.666667
                    </td>
                    
                    <td>
                      3.616667
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      756
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      2.25
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      Málaga CF
                    </td>
                    
                    <td>
                      RC Deportivo de La Coruña
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.293333
                    </td>
                    
                    <td>
                      3.250000
                    </td>
                    
                    <td>
                      3.183333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      757
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      1.53
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      1.50
                    </td>
                    
                    <td>
                      4.00
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      7.00
                    </td>
                    
                    <td>
                      Athletic Club de Bilbao
                    </td>
                    
                    <td>
                      Real Sporting de Gijón
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      1.533333
                    </td>
                    
                    <td>
                      6.833333
                    </td>
                    
                    <td>
                      3.833333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      758
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      1
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      3.25
                    </td>
                    
                    <td>
                      2.30
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.10
                    </td>
                    
                    <td>
                      Granada CF
                    </td>
                    
                    <td>
                      Real Betis Balompié
                    </td>
                    
                    <td>
                      2
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      2.333333
                    </td>
                    
                    <td>
                      3.150000
                    </td>
                    
                    <td>
                      3.183333
                    </td>
                    
                    <td>
                      A
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                  
                  <tr>
                    <th>
                      759
                    </th>
                    
                    <td>
                      Spain
                    </td>
                    
                    <td>
                      Spain LIGA BBVA
                    </td>
                    
                    <td>
                      2015/2016
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                    </td>
                    
                    <td>
                      2.20
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      2.10
                    </td>
                    
                    <td>
                      3.40
                    </td>
                    
                    <td>
                      &#8230;
                    </td>
                    
                    <td>
                      3.20
                    </td>
                    
                    <td>
                      Rayo Vallecano
                    </td>
                    
                    <td>
                      RCD Espanyol
                    </td>
                    
                    <td>
                      3
                    </td>
                    
                    <td>
                      H
                    </td>
                    
                    <td>
                      2.166667
                    </td>
                    
                    <td>
                      3.233333
                    </td>
                    
                    <td>
                      3.400000
                    </td>
                    
                    <td>
                      D
                    </td>
                    
                    <td>
                      False
                    </td>
                  </tr>
                </table>
                
                <p>
                  100 rows × 23 columns
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [134]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[134]:
            </div>
            
            <div class="output_text output_subarea output_execute_result">
              <pre>False                        582
Draw                          63
West Ham United               10
Stoke City                     8
West Bromwich Albion           6
Real Sociedad                  5
Real Betis Balompié            5
Granada CF                     5
Swansea City                   5
Southampton                    4
Real Sporting de Gijón         4
Watford                        4
UD Las Palmas                  4
RCD Espanyol                   4
Sunderland                     3
SD Eibar                       3
RC Celta de Vigo               3
Valencia CF                    3
Newcastle United               3
Crystal Palace                 3
RC Deportivo de La Coruña      3
Levante UD                     3
Leicester City                 2
Bournemouth                    2
Getafe CF                      2
Liverpool                      2
Villarreal CF                  2
Athletic Club de Bilbao        2
Manchester United              2
Everton                        2
Málaga CF                      2
Norwich City                   2
Chelsea                        1
Tottenham Hotspur              1
Atlético Madrid                1
Rayo Vallecano                 1
Real Madrid CF                 1
Aston Villa                    1
Sevilla FC                     1
Name: beating_bookies_team, dtype: int64</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            The list above gives a full breakdown of the teams that have &#8216;beat the bookies&#8217;. It shows us that West Ham were the top, and the only team to beat the bookies in a double figure amount of games.
          </p>
          
          <p>
            Lets plot some graphs to make this easier to digest.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [149]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df2</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">beating_bookies_team</span> <span class="o">!=</span> <span class="kc">False</span><span class="p">]</span>
<span class="n">df2</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Which team beat the most?'</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            This removes all games where the bookmakers were not beaten, lets remove the draws too.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [150]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">df3</span> <span class="o">=</span> <span class="n">df2</span><span class="p">[</span><span class="n">df2</span><span class="o">.</span><span class="n">beating_bookies_team</span> <span class="o">!=</span> <span class="s1">'Draw'</span><span class="p">]</span>
<span class="n">df3</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Which team beat the bookies the most?'</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
               <img loading="lazy" class="alignnone size-full wp-image-1892" src="https://empiahanalysis.files.wordpress.com/2018/06/download-5.png?resize=372%2C389" alt="download (5)" width="372" height="389" data-recalc-dims="1" />
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            Here we go &#8211; this is much easier to see. We can see that West Ham were way out in front.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [78]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1">#the below will create a variable depending on a filter, then count how many values are in that variable</span>
<span class="n">win_beat_count</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">[(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="s1">'Draw'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="kc">False</span><span class="p">)])</span>
<span class="n">draw_beat_count</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'Draw'</span><span class="p">])</span>
<span class="n">not_beat_count</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">==</span> <span class="kc">False</span><span class="p">])</span>

<span class="nb">print</span><span class="p">(</span><span class="n">win_beat_count</span><span class="p">)</span> <span class="c1">#check we get an expected output</span>
<span class="nb">print</span><span class="p">(</span><span class="n">draw_beat_count</span><span class="p">)</span> <span class="c1">#check that we get an expected output, can compare to the data above</span>
<span class="nb">print</span><span class="p">(</span><span class="n">not_beat_count</span><span class="p">)</span> <span class="c1">#check that we get an expected output, can compare to the data above</span>
<span class="nb">print</span><span class="p">(</span><span class="n">win_beat_count</span> <span class="o">+</span> <span class="n">draw_beat_count</span> <span class="o">+</span> <span class="n">not_beat_count</span><span class="p">)</span> <span class="c1">#make sure they add up to the total, 760</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>115
63
582
760
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [79]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1">#now we have checked them, lets make them into percentages</span>
<span class="n">win_beat_prc</span> <span class="o">=</span> <span class="n">win_beat_count</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
<span class="n">draw_beat_prc</span> <span class="o">=</span> <span class="n">draw_beat_count</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
<span class="n">not_beat_prc</span> <span class="o">=</span> <span class="n">not_beat_count</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [80]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1">#creating a pie chart to easily see this data</span>
<span class="n">labels</span> <span class="o">=</span> <span class="s1">'Draw'</span><span class="p">,</span> <span class="s1">'Match Won'</span><span class="p">,</span> <span class="s1">'Not beaten'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">draw_beat_prc</span><span class="p">,</span> <span class="n">win_beat_prc</span><span class="p">,</span> <span class="n">not_beat_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mi"></span><span class="p">,</span><span class="mf">0.1</span><span class="p">,</span><span class="mf">0.1</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Beat the bookies!</span><span class="se">\n</span><span class="s1">Percentage of times Bet365 was beaten by match result'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
               <img loading="lazy" class="alignnone size-full wp-image-1902" src="https://empiahanalysis.files.wordpress.com/2018/06/output_56_0.png?resize=356%2C266" alt="output_56_0" width="356" height="266" data-recalc-dims="1" />
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            As we can see, it is not all too often that the bookies are beaten. The above suggests that the bookmakers would keep 77% of the money behind all bets, and would only pay out on 23% of bets. If, however, you do want to put that money on &#8211; it looks like bookmakers are most often beaten by a team winning and not draws.
          </p>
          
          <p>
            Let&#8217;s deep dive into that winning percentage of 23% to see how the bets are split.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [81]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">win_beat_count_home</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">[(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="s1">'Draw'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="kc">False</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'longest_odds'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'H'</span><span class="p">)])</span>
<span class="n">win_beat_count_away</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">[(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="s1">'Draw'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="kc">False</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'longest_odds'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'A'</span><span class="p">)])</span>
<span class="c1"># the aboev will look at what how many times the games were won by away or home teams</span>


<span class="nb">print</span><span class="p">(</span><span class="n">win_beat_count_home</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">win_beat_count_away</span><span class="p">)</span> <span class="c1">#just checking that these are sensible amounts</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>32
83
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [82]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">win_beat_home_prc</span> <span class="o">=</span> <span class="n">win_beat_count_home</span> <span class="o">/</span> <span class="p">(</span><span class="n">win_beat_count</span> <span class="o">+</span> <span class="n">draw_beat_count</span><span class="p">)</span>
<span class="n">win_beat_away_prc</span> <span class="o">=</span> <span class="n">win_beat_count_away</span> <span class="o">/</span> <span class="p">(</span><span class="n">win_beat_count</span> <span class="o">+</span> <span class="n">draw_beat_count</span><span class="p">)</span>
<span class="n">draw_beat_prc_win</span> <span class="o">=</span> <span class="n">draw_beat_count</span> <span class="o">/</span> <span class="p">(</span><span class="n">win_beat_count</span> <span class="o">+</span> <span class="n">draw_beat_count</span><span class="p">)</span>
<span class="c1">#these are to get some percentage amounts for a pie chart</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [83]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1">#creating a pie chart to easily see the breakdown of bookie beating scenarios</span>
<span class="n">labels</span> <span class="o">=</span> <span class="s1">'Draw'</span><span class="p">,</span> <span class="s1">'Match Won by Home Team'</span><span class="p">,</span> <span class="s1">'Match Won by Away Team'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">draw_beat_prc_win</span><span class="p">,</span> <span class="n">win_beat_home_prc</span><span class="p">,</span> <span class="n">win_beat_away_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mf">0.05</span><span class="p">,</span><span class="mf">0.05</span><span class="p">,</span><span class="mf">0.05</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Beat the bookies!</span><span class="se">\n</span><span class="s1">Percentage of bookie beating bets by match outcome'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
               <img loading="lazy" class="alignnone size-full wp-image-1903" src="https://empiahanalysis.files.wordpress.com/2018/06/output_60_0.png?resize=413%2C266" alt="output_60_0" width="413" height="266" data-recalc-dims="1" />
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            So, we can ascertain from the above that you are most likely to beat the bookies by betting on the away team to win. The above follows the analysis we saw right at the start, where the most likely result is a win to the home team &#8211; this is mirrored in the above, as it suggests that it is not often that the home team are underdogs and would present themselves as an opportunity to beat the bookies.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            I want to do some analysis by league to finish this off, to see if it can give us any additional insights
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [84]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">pl_beat_teams</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">beating_bookies_team</span><span class="p">[</span><span class="n">league_pl</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">())</span><span class="o">-</span><span class="mi">2</span> 
<span class="c1">#count of number of teams that have beaten bookies from PL, minus two to remove count of Draw and False</span>
<span class="n">bbva_beat_teams</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">beating_bookies_team</span><span class="p">[</span><span class="n">league_bbva</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">())</span><span class="o">-</span><span class="mi">2</span> 
<span class="c1">#count of number of teams that have beaten bookies from BBVA, minus two to remove count of Draw and False</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [85]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">pl_beat_teams_prc</span> <span class="o">=</span> <span class="n">pl_beat_teams</span> <span class="o">/</span> <span class="p">(</span><span class="n">pl_beat_teams</span> <span class="o">+</span> <span class="n">bbva_beat_teams</span><span class="p">)</span> <span class="c1">#getting some percentages for count of PL teams</span>
<span class="n">bbva_beat_teams_prc</span> <span class="o">=</span> <span class="n">bbva_beat_teams</span> <span class="o">/</span> <span class="p">(</span><span class="n">pl_beat_teams</span> <span class="o">+</span> <span class="n">bbva_beat_teams</span><span class="p">)</span> <span class="c1">#getting some percentages for count of BBVA teams</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [86]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1">#creating a pie chart to easily see this data</span>
<span class="n">labels</span> <span class="o">=</span> <span class="s1">'Premier League Team'</span><span class="p">,</span> <span class="s1">'BBVA Team'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">pl_beat_teams_prc</span><span class="p">,</span> <span class="n">bbva_beat_teams_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mf">0.05</span><span class="p">,</span><span class="mf">0.05</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Beat the bookies!</span><span class="se">\n</span><span class="s1">Percentage of teams beating the bookies by league'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div>
            </div>
            
            <div class="prompt">
              <img loading="lazy" class="alignnone size-full wp-image-1904" src="https://empiahanalysis.files.wordpress.com/2018/06/output_65_0.png?resize=356%2C266" alt="output_65_0" width="356" height="266" data-recalc-dims="1" />
            </div>
            
            <div class="output_png output_subarea ">
              <img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [87]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">pl_beats_count</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">[(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="s1">'Draw'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="kc">False</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'league_name'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'England Premier League'</span><span class="p">)])</span>
<span class="n">bbva_beats_count</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">[(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="s1">'Draw'</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'beating_bookies_team'</span><span class="p">]</span> <span class="o">!=</span> <span class="kc">False</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'league_name'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'Spain LIGA BBVA'</span><span class="p">)])</span>
<span class="c1">#creating a varibale to give us the total number of bookie beating matches that are associated with league</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [88]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="nb">print</span><span class="p">(</span><span class="n">pl_beats_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">bbva_beats_count</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">pl_beats_count</span> <span class="o">+</span> <span class="n">bbva_beats_count</span><span class="p">)</span> 
<span class="c1">#testing that this data is correct</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>61
54
115
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [89]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="n">pl_beats_prc</span> <span class="o">=</span> <span class="n">pl_beats_count</span> <span class="o">/</span> <span class="n">win_beat_count</span> <span class="c1">#creating some percentages for a  graph</span>
<span class="n">bbva_beats_prc</span> <span class="o">=</span> <span class="n">bbva_beats_count</span> <span class="o">/</span> <span class="n">win_beat_count</span> <span class="c1">#creating some percentages for a graph</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [90]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span class="c1">#creating a pie chart to easily see this data</span>
<span class="n">labels</span> <span class="o">=</span> <span class="s1">'Premier League Match'</span><span class="p">,</span> <span class="s1">'BBVA Match'</span>
<span class="n">fracs</span> <span class="o">=</span> <span class="p">[</span><span class="n">pl_beats_prc</span><span class="p">,</span> <span class="n">bbva_beats_prc</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mf">0.05</span><span class="p">,</span><span class="mf">0.05</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s2">"equal"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Beat the bookies!</span><span class="se">\n</span><span class="s1">Percentage of matches beating the bookies by league'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">fracs</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%.0f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">);</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img loading="lazy" class="alignnone size-full wp-image-1905" src="https://empiahanalysis.files.wordpress.com/2018/06/output_69_0.png?resize=356%2C266" alt="output_69_0" width="356" height="266" data-recalc-dims="1" /><img />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            We can see from these two pie charts that even though there are slightly more BBVA teams that have beat the bookies, if you look at amount of matches, the Premier League is on top &#8211; just.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            &nbsp;
          </p>
          
          <h2 id="Conclusions">
            Conclusions
          </h2>
          
          <p>
            In conclusion this analysis has helped us understand the best bookmakers to use depending on the outcome we are expecting and also which scenarios would most consistently give the longest odds.
          </p>
          
          <p>
            It was interesting to see that even though a draw is the most unlikely scenario &#8211; it was an away win that gave the longest odds on average.
          </p>
          
          <p>
            If we look at the league data there were just about more teams in the Spanish league (BBVA) that did beat the bookies, there were more games in the premier league in which the longest odds paid out. This may suggest slightly more volatility in the Spanish league, with more underdog teams winning, whilst the data suggesting that a smaller amount of underdog premier league teams caused upsets. West Ham for example, who beat the bookies the most, came 7th out of 20 teams. I would argue that this is far above where they were expected to place before the start of the season.
          </p>
          
          <p>
            Using this data, I would look to use William Hill is I was betting on a home team to win and Bet 365 for a draw or an away win. I would also turn to the Spanish league if I wanted to put on more varied bets on smaller teams causing an upset, whilst in the premier league I would maybe want to spend more time studying smaller teams which could beat the favourite.
          </p>
          
          <p>
            If I were to continue this analysis I would look at the betting odds trends between leagues to understand if the bookmakers who gave the best odds overall consistently did between leagues or if there were differences between the two.
          </p>
          
          <p>
            In regards to limitations, I would say that I would like to have carried out some predictive modelling using regression or something similar but I do not yet have the knowledge. If I had more time this is something I would have tried to research so that I could have implemented it. I would also say that it would have been good to have details on domestic cup competitions within the data set as this meant we could have perhaps analysed how a team was given odds in the league vs. domestic cups even if they played the same teams.
          </p>
        </div>
      </div>
    </div>
  </div>
</div>

&nbsp;

&nbsp;