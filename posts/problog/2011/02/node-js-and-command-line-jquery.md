node.js combined with the [new query utility](https://github.com/visionmedia/query) which makes jQuery-like functionality available from the command line. This type of thing used to take a 30-line script. Brilliant!

<div class="code">

<pre>for N in {1..10}; do curl --silent http://news.ycombinator.com | query td.title a get "${N}"; done

YC Partner Harjeet Taggar Gives Insights [Interview]
Update your timezone defs: Russia abolishes winter time (DST)
Want to be a leader? Wash the Dishes When Nobody Else Will. 
How to be 100% sure your startup idea is good
Introducing the Google Translate app for iPhone
In China, alpha males carry designer purses
How To Get Your First 1,000 Users
How Much Money I Made From Side Projects In 2010
Facebook Buys Old Sun Campus in Menlo Park
Government investigation: No evidence Toyota electronic throttles malfunctioned
</pre>

</div>