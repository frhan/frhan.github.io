---
layout: post
title: What I learned about software developers in Bangladesh from the 2019 StackOverflow survey
excerpt: Analyzing the StackOverflow developer survey data of Bangladesh
keywords: bangladesh, stack overflow, developers, programmers, survey, data, statistics, 2019
---

<div class="spacer"></div>

# Introduction 
I have been playing with [this year's StackOverflow developer survey data](https://insights.stackoverflow.com/), after they made it publicly available. And was trying to learn more about the developer community of Bangladesh. In this post I present
what I've learned from analyzing the data. 

In the survey, there were __605__ entries from Bangladesh. On average the survey took __25 minutes__
to complete. And I think those who participated in the survey are more or less representatives of the Bangladeshi developer community.

<div class="spacer"></div>

# Key points
If you don't feel like looking into lots of charts right now, here is the gist for you. 

- *Lack of support from management is one of the key productivity challenges in Bangladesh.*
- *There is little relationship between developer's salary and experience.*
- *The approval rate of the managers is surprisingly high compared to some other countries.*
- *Majority of the developers want to become manager in future, a trend that we don't see in the IT-developed countries.*
- *We are aware of our abilities; majority of us don't think we are above average. (Are we really? Read on for details.)*
- *Majority of the developers are satisfied with their current job, and overall career.* 
- *Those who are actively seeking jobs, switched their last job not more than 2 years ago.* 
- *Opportuniteis for professional growth, and company culture is the most imporant factors for job seekers*
- *Developers are self learners, most of them are teaching themselves languages, frameworks, participating in MOOCs etc.*
- *Javascript is the most loved, Python is the most wanted language; and React is the most wanted framework.*
- *Majority of the companies don't employ unit tests.*
- *Majority of the developers do code reviews as they see value in doing so.*

That was the summary, now if you are like me, who believes **data is beautiful**, read on. 

<div class="spacer"></div>

# Basic information about the respondents 

### Developer types 

<div id="fig1" class="chart">
    <img src="/public/so-survey-2019/devtype.jpg" /> 
    <div class="caption">Figure-1.1: Developer types</div>
</div>

Two thirds of the participants are professional developers.

### Years coding professionally

<div id="fig2" class="chart">
    <img src="/public/so-survey-2019/yearscodepro.jpg" /> 
    <div class="caption">Figure-1.2: Years coding professionally</div>
</div>

About half of the respondents are professionals with 2-5 years of experience. And about a quareter are with more than 5 years of experience. 

### Years since learning to code

<div id="fig3" class="chart">
    <img src="/public/so-survey-2019/yearslearncode.jpg" /> 
    <div class="caption">Figure-1.3: Years since learning to code</div>
</div>

### Writing that first line of code 

Comparison of the average age of writing that first line of code across some countries. 

<div id="fig4" class="chart">
    <img src="/public/so-survey-2019/meanage.jpg" /> 
    <div class="caption">Figure-1.4: Average age of writing that first line of code </div>
</div>

As we see, we are pretty late when it comes to writing that first line of code. Most of us haven't written `Hello World!` before 
we finish higher secondary. 

### Coding as hobby 
Let's now compare how much we consider coding as our hobby with some other countries. 

<div id="fig5" class="chart">
    <img src="/public/so-survey-2019/hobbycoding.jpg" /> 
    <div class="caption">Figure-1.5: Comparison of coding as a hobby across different countries</div>
</div>

Ok, so majority of us spend our leisure time on coding, like many other countries. Although, I think it doesn't 
indicate anything regarding how good or bad the developer is. I believe one can be a good developer __without__ having coding as a hobby. 

### Contributing to open source softwares 

<div id="fig6" class="chart">
    <img src="/public/so-survey-2019/opensourcer.jpg" /> 
    <div class="caption">Figure-1.6: How often do you contribute to open source</div>
</div>

I find this __pleasantly__ surprising. I never thought I would find 22% of the respondents from Bangladesh contribute to some open source software once a month or more often. As a developer with more than a decade of professional experience, I feel guilty of not doing so. More because  
**I am using open source software every single day**. I want to contribute, but find it difficult to start. 
Kudos to you if you are a opensource contributor!


### Non-degree education and learning 
Although I don't show it here, majority of the developers in Bangladesh have a B.Sc. with CS related major. Let's see here 
what non-academic type learning we involve in. 

<div id="fig7" class="chart">
    <img src="/public/so-survey-2019/eduother.jpg" /> 
    <div class="caption">Figure-1.7: Non academic education and learning</div>
</div>

This confirms my belief that we, the developers, are **lifelong learners**. We enjoy learning new things. And we continue the learning process by ourselves, whether it is a new language/framework, or whether by participating in a MOOC. 

<div class="spacer"></div>


# Feeling of competence 
In the survey there was a question,

> For the specific work you do, and the years of experience you have, how do you rate your own level of competence?

Statistically, it is impossible that majority of any group are above average. Let's see how we answered that. 

<div id="fig8" class="chart">
    <img src="/public/so-survey-2019/abvavg.jpg" /> 
    <div class="caption">Figure-2.1: Are you above average</div>
</div>

Ok, so around half of us think we are above average, which is not so bad. If we compare this across some other countries we can see surprising result! 

<div id="fig9" class="chart">
    <img src="/public/so-survey-2019/average-cr.jpg" /> 
    <div class="caption">Figure-2.2: Thinking of above average across countries</div>
</div>

Wow! We seem to have a good idea about our abiliteis. I find it a bit hard to believe though. So I dig deeper, and plot the data 
a bit differently. This time comparing the thought of being above average vs the developer's experience. 

<div id="fig10" class="chart">
    <img src="/public/so-survey-2019/abvavg-exp.jpg" /> 
    <div class="caption">Figure-2.3: Thinking of above average vs professional experience</div>
</div>

Yes, now I find what I was seeking. **As we get more experience, we tend to inflate our abilities.** We probably forget that, it's not only me, other developers are also getting more experience. The developers in the group of 11-20 years experience in Bangladesh believe 84% of them are better than average! Are you aware of [Illusory superiority](https://en.wikipedia.org/wiki/Illusory_superiority) and [Dunning–Kruger effect](https://en.wikipedia.org/wiki/Dunning%E2%80%93Kruger_effect)?


<div class="spacer"></div>

# Salary
The first chart I want to show about salary is by plotting individual salary data vs experience in a scatter plot. (3% from the top and bottom part of the data is removed here.)

<div id="fig11" class="chart">
    <img src="/public/so-survey-2019/salary.jpg" /> 
    <div class="caption">Figure-3.1: Individual salary vs experience</div>
</div>

Ok, it's all over the place. There is no structure at all, and there is no direct relationship between one's 
experience and salary. It is not unique to Bangladesh, I've seen similar chart for other countries as well. 

But wait, all is not lost. If we plot the data by grouping the experience, and taking the median salary we can see the median salary is somewhat rising with experience, upto a certain point. 

<div id="fig12" class="chart">
    <img src="/public/so-survey-2019/salarygroupped.jpg" /> 
    <div class="caption">Figure-3.2: Median salary vs experience</div>
</div>

Software development is a competitive field. Most of the companies don't want to limit themselves when hiring, by imposing some structure on the salary vs the candidate's experience. So there is a strong chance that even if you are junior, you can make more than some seniors, if you are productive, and can produce value for your company. And we should not take it for granted that our salary will rise as we get more experience. It probably will, but not automatically, __you'll have to earn it__. 

As there seems to be a lack of structure, here's one tip for developers who are seeking jobs. `If possible refrain from mentioning your current and expected salary when asked. Instead request the employer to take your interview first, and come up with their best offer once you passed.`

<div class="spacer"></div>

# Development practices and productivity
Let's see how we are doing in terms of development practices, and also what hinders our productivity. 

### Code review 
<div id="fig13" class="chart">
    <img src="/public/so-survey-2019/codereview.jpg" /> 
    <div class="caption">Figure-4.1: Code review as part of your process</div>
</div>

So most of us are doing code reviews as part of our work, and we also see the value of it.

### Unit tests 
<div id="fig14" class="chart">
    <img src="/public/so-survey-2019/unittest.jpg" /> 
    <div class="caption">Figure-4.2: Unit test practice in the company</div>
</div>

Unfortunately, less than one third of the companies employ unit tests as part of their process. I am personally not a huge fan of unit tests myself, although I see the value in it, especially when refactoring some part of the code. 

### Greatest challenge to productivity 
When asked what are the greatest challenges to developer's productivity, we see the following. 

<div id="fig15" class="chart">
    <img src="/public/so-survey-2019/workchallenge.jpg" /> 
    <div class="caption">Figure-4.3: Greatest challenge to productivity</div>
</div>

Distracting work environment is the main culprit here. This is similar for most other countries as well. 
`Open office plan is killing developer's productivity.`
If you don't believe me, [ask DHH.](https://m.signalvnoise.com/the-open-plan-office-is-a-terrible-horrible-no-good-very-bad-idea/)
If you are the key decision maker in your company, you should seriously evaluate this. You don't have to do it just because [Facebook did it](https://www.inc.com/tanner-christensen/how-facebook-keeps-employees-happy-in-the-worlds-largest-open-office.html), maybe you copied half of the things and forgot the rest. 

What about the next one? Lack of support from management is also a greatest challenge to productivity in Bangladesh. Seriously? I thought the managers are there to help us be our best? Why should their support be __lacking__? Who's benefit they are considering when they are not supporting the developers properly? The company's? This is sad. 

When I compare the __lack of management support__ with other countries I see this. 

<div id="fig16" class="chart">
    <img src="/public/so-survey-2019/lacksupport.jpg" /> 
    <div class="caption">Figure-4.3: Lack of management support across companies</div>
</div>

This is unfortunate. Most of our managers are __lacking considerably__ when it comes to support the developers, compared to the countries which have more mature software industry.

To all the managers who are reading this post, please evaluate yourself in terms of how you are supporting your developers. Talk to them openly, about how can you improve. Talk to managers from other companies that you know are doing good. I am sure you will find there are cetain things __you can change__ to support your developers more. None of us is perfect. Finding out one's shortcomings and continuous improvement is the key to success. 

<div class="spacer"></div>

# Career values 
The survey asked about the current job satisfaction, and overall career satisfaction.

### Job satisfaction 

<div id="fig17" class="chart">
    <img src="/public/so-survey-2019/jobsat.jpg" /> 
    <div class="caption">Figure-5.1: Job satisfaction</div>
</div>

It seems about half of us are satisfied with our current job. 

### Career satisfaction 

<div id="fig18" class="chart">
    <img src="/public/so-survey-2019/careersat.jpg" /> 
    <div class="caption">Figure-5.2: Career satisfaction</div>
</div>

And around 60% of us are satisfied with our overall career. Let's compare career satisfaction across different 
countries. 

<div id="fig19" class="chart">
    <img src="/public/so-survey-2019/careersat-cr.jpg" /> 
    <div class="caption">Figure-5.3: Comapring career satisfaction</div>
</div>

Ok, developers from other countries may be a bit more satisfied about their career. But we are not that much 
behind. 

<div class="spacer"></div>

# Management
The survey asked some questions about whether the respondent approves of his manager, or in future whether we want to 
become manager or not.

### Manager acceptance 
The survey asked, 
> How confident are you that your manager knows what they’re doing? 

<div id="fig20" class="chart">
    <img src="/public/so-survey-2019/mgr-acceptance.jpg" /> 
    <div class="caption">Figure-6.1: Manager acceptance</div>
</div>

Surprisingly, it seems majority of us think our mangers know what they are doing. (Is this a bit contradictory with the lack of support point that was made earlier? Maybe, maybe not, I don't know.)

*Fun fact, in the stack overflow data this column is called __MgrIdiot__.*

### Need to become manager to make more 

<div id="fig21" class="chart">
    <img src="/public/so-survey-2019/mgr-money.jpg" /> 
    <div class="caption">Figure-6.2: Need to become manager to make more</div>
</div>

This is not surprising, half of us think we need to become manager to make more. 

### Wanting to become manager 

<div id="fig22" class="chart">
    <img src="/public/so-survey-2019/mgr-want.jpg" /> 
    <div class="caption">Figure-6.3: Do you want to become manager in future</div>
</div>

And almost two thirds of the respondents want  to become manager in future. Let's compare this with some other countries.

<div id="fig23" class="chart">
    <img src="/public/so-survey-2019/mgrwant-cr.jpg" /> 
    <div class="caption">Figure-6.4: Comparing wanting to become manager</div>
</div>

I want to believe the majority of those who want to become managers are passionate about management. I know that would be a fallacy though. I think the majority of them want to become manager because **they will get better salary and benefits**. Sad, but that's how it is in Bangladesh. 

I think companies should create technical positions for developers, who do not manage project or people directly, but takes key decision in technical implementations. And also evaluate them appropriately. So that, developers who are not really passionate about management, have alternative career path. 

And my request to these two third of the developers who want to become manager, when you do become manager, please support the developers to become their best. So that we can see **lack of support from management** is no longer a challenge to productivity in Bangladesh. 

<div class="spacer"></div>

# Technology stack
### Most commonly used language 

<div id="fig24" class="chart">
    <img src="/public/so-survey-2019/lang-common.jpg" /> 
    <div class="caption">Figure-7.1: Most commonly used language</div>
</div>

Yes, __Javascript__ rules!

### Most loved language 

<div id="fig25" class="chart">
    <img src="/public/so-survey-2019/lang-loved.jpg" /> 
    <div class="caption">Figure-7.2: Most loved language</div>
</div>

Again, we love __Javascript__! 

### Most wanted language 

<div id="fig26" class="chart">
    <img src="/public/so-survey-2019/lang-want.jpg" /> 
    <div class="caption">Figure-7.3: Most wanted language</div>
</div>

But if it was upto us to chose, on which language we like to work next year, majority would chose __Python__ or __Go__. 

### Most dreaded language 

<div id="fig27" class="chart">
    <img src="/public/so-survey-2019/lang-dread.jpg" /> 
    <div class="caption">Figure-7.4: Most dreaded language</div>
</div>

And HTML/CSS is most dreaded closely followed by PHP, not at all surprising. 

### Most commonly used Web frameworks 

<div id="fig25" class="chart">
    <img src="/public/so-survey-2019/web-common.jpg" /> 
    <div class="caption">Figure-7.5: Most commonly used Web frameworks</div>
</div>

### Most loved Web frameworks 

<div id="fig26" class="chart">
    <img src="/public/so-survey-2019/frame-loved.jpg" /> 
    <div class="caption">Figure-7.6: Most loved web frameworks</div>
</div>

### Most dreaded Web frameworks 

<div id="fig27" class="chart">
    <img src="/public/so-survey-2019/frame-dread.jpg" /> 
    <div class="caption">Figure-7.7: Most dreaded web frameworks</div>
</div>

### Most wanted Web frameworks 

<div id="fig28" class="chart">
    <img src="/public/so-survey-2019/frame-wanted.jpg" /> 
    <div class="caption">Figure-7.8: Most wanted web frameworks</div>
</div>

So jQuery can be, at the same time, the most used, loved, and dreaded web framework in Bangladesh.  But the crown for most wanted web framework goes to React! 

### Other tech stats 
I omitted some other statistics about technology, if you are interested please [check the charts here](https://so-survey-bd.glitch.me/loved-tech.html). 

<div class="spacer"></div>

# Job search

### Current job seeking status 

<div id="fig29" class="chart">
    <img src="/public/so-survey-2019/jobseeking.jpg" /> 
    <div class="caption">Figure-8.1: Job seeking status</div>
</div>

### Most important job factors while seeking jobs  

<div id="fig30" class="chart">
    <img src="/public/so-survey-2019/jobfactors.jpg" /> 
    <div class="caption">Figure-8.2: Most important job factors</div>
</div>

So it seems, apart from technology choice, most developers are concerned about the company culture, and 
opportunities for professional growth. 

### Job seeker's stability

<div id="fig31" class="chart">
    <img src="/public/so-survey-2019/stability.jpg" /> 
    <div class="caption">Figure-8.3: Job seekers stability</div>
</div>

Among active job seekers, half of them switched their job not more than 2 years ago. Maybe they haven't found their dream company yet, or maybe job seeking is also a hobby for some, who knows.

<div class="spacer"></div>

# Miscellaneous stats

## Social media use 

<div id="fig32" class="chart">
    <img src="/public/so-survey-2019/socialnetwork.jpg" /> 
    <div class="caption">Figure-9.1: Which social media you use most</div>
</div>

As expected, Facebook is the social media most developers use in Bangladesh. Although, [Reddit is the most 
popular social media among the developer communities worldwide](https://insights.stackoverflow.com/survey/2019#developer-profile-_-social-media-use). 

## Sexual orientation 

<div id="fig33" class="chart">
    <img src="/public/so-survey-2019/sexuality.jpg" /> 
    <div class="caption">Figure-9.2: Sexual orientation</div>
</div>

Hmmm.... 

## Better life 

I would like to conclude the stats with this one. 

<div id="fig34" class="chart">
    <img src="/public/so-survey-2019/betterlife.jpg" /> 
    <div class="caption">Figure-9.3: Optimism about future</div>
</div>

I love this result. Even with so many challenges in Bangladesh, two third of us believe that people born today will have a better life than their parents. This fills my heart with joy. I know it will not happen magically, __we have to__ make it better, but believing is the first step. 

<div class="spacer"></div>

# Conclusion 
If you have read this far, thank you very much for your time. I feel the time I spent analyzing the data, and writing this post is well spent. As a part of the developer community of Bangladesh, I hope you will do your best to move the industry forward. 

Lastly, 
- *I hope our local industry grows, in such a way that, developers don't have to become managers just for the sake of better benefits. Rather, they become managers because they are passionate about management.*
- *If you are a manager now, identify how you can help your developers become more productive.*
- *If you are a developer who want to become manager in future, keep in mind all the challenges that you face now, and make sure those are not repeated for the developers working under you.*
- *Participate in the next Stack Overflow survey when that happens, so that we can learn more about our profession.*

<div class="spacer"></div>

# Appendix
If you haven't already, check out [the main survey results](https://insights.stackoverflow.com/survey/2019).
And if you want to customize/play with the data yourself, you can find [my project, including the code here](https://so-survey-bd.glitch.me/).
