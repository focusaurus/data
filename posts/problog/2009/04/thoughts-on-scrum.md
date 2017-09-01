So I had a chance to work in the [Scrum](http://en.wikipedia.org/wiki/Scrum_(development)) methodology for about six months recently. I thought I'd write up some of my thoughts on the experience and the process. Please note that first, this is my first experience working in the Scrum process. I am sure as I use it more these opinions will change. Second, these are strictly my personal thoughts and opinions and in no way represent the experience of my team or anyone else. Third, my project had a specific set of tasks and particulars. On a different project, with more sprints or shorter tasks or other relevant variations, I might have drawn (and may well draw in the future) different conclusions.

Overall, agile and Scrum are a vast improvement over the [waterfall model](http://en.wikipedia.org/wiki/Waterfall_model) traditionally used at large companies. Some of the specifics benefits:

*   Far less time wasted doing detailed design and estimates for huge amounts of work that will take a long time to build, or very often might not get built at all
*   Overall a very steady and metered workload. We did hit a few days of mad dash toward the end of one or two sprints preparing for the demo, but much more stable than the wild variances and unpredictability of waterfall
*   The focus on build and test automation really does enable better agility in the code and prevent regressions
*   Having something demoable every month is just all around good for all parties involved. I think perhaps this is the single most important piece of the methodology. Ignore this and I bet a substantial amount of the benefit of Scrum would be lost.
*   Similar to demoable, the notion of "potentially shippable product" really rings true for me and forces you to deal with the issues that often lurk in the shadows in the waterfall model only to jump out at the last minute: installation, upgrade, documentation, fit and finish, etc.

So the remainder of this will mostly comment on things I found to be problematic or confusing, but I want it to be clear that I am a huge proponent of agile and Scrum and this is not meant to be an argument that the status quo is better. Quite the contrary.

### The Backlog and User Stories

I want to opine a bit about this notion of "User Stories". Conceptually, this feels like a perfectly healthy way to constantly remind the team to be focused on the important things that will be valuable to the end users. I think this works best for user interfaces and web development where the ratio of engineering effort to visible, tangible change in the end user interface or experience is high. However, I think in many other areas of software development, such as embedded systems, and in our case complex enterprise software, one user story can generate a boatload of tasks and there end up being a lot of backlog items that are just engineering internal stepping stones to functionality. In our team, we were able to bridge this gap and refer to the work items in the backlog just as general "backlog items", but I still felt a bit guilty adding more raw engineering items to the backlog even though it would be a bit of a stretch to tie them closely to a user story. I think we managed to get beyond this eventually and I don't think we strayed off into the woods of unimportant engineering diversions. However, in many if not most backlog items, we were not able to apply the "As a $USER_ROLE, I want to $ACTION so I can $BENEFIT" user story template.

I was just browsing around [www.openagile.com](http://www.openagile.com) and noticed they call the backlog the "Work Queue". I like this name better because it more easily allows the notion of "anything that requires work" can go in there and I dislike the word "backlog" because it connotes a buildup of work debt that for me has negative motivational effects.

Secondly, I found some problems trying to implement this idea that a user story should fit on a "story card" the size of an index card and be fleshed out through face to face conversation. The software I develop at work tends to have a high complexity level and attention to detail. It's more complex than web development. Our work items often can't be clearly expressed with something straightforward like "As a shopper, I want to see the total cost of the items in my shopping cart in the page header". The problem with discussion is A) our team was in three cities with no more than two people in any single location B) we wanted something in writing that could be referred to over and over again throughout and after the sprint and C) no one could remember the details otherwise. Due to C), if you asked the product owner (1/2 me) to clarify a user story through conversation on sprint day 2, 12, and 16, you were liable to get three variations. Our stories ended up being usually at least a few paragraphs worth of detail plus a smattering of acceptance tests, and I think that is OK and worked better for us.

Also, it turns out that populating and maintaining the product backlog is actually a large amount of work. Keeping the backlog items detailed enough, in the right order, with good acceptance tests takes an awful lot of time. Normally the product owner is not on the scrum team. However, at my company we're not adopting that aspect at this time (for several reasons), and in this project myself and one other scrum team member acted as the product owner role. Basically after working hard to get the sprint review demo up and working, my co-product-owner and I would have about 2 hours Friday afternoon while we were completely fried and 1 hour Monday morning to try to whip the backlog into shape for the next sprint planning meeting Monday morning. In retrospect, we should have allocated about two full days per sprint just for care and feeding of the product backlog. For the early sprints, this number might be larger - like a week, and then as the effort congeals, the amount of time the product owner needs to allocate to backlog care and feeding will probably grow shorter, unless a major change of requirements comes down the pike.

One final point about the backlog or work queue. After several sprints, we ended up having a fairly enormous work queue with hundreds of items. This became really unwieldy to deal with as a flat list ordered by priority. We ended up wanting to leave the items in the sprint ordered by priority, and about a sprint or two's worth of work items ordered by priority in the backlog, but for all the stuff further down the road, it was much easier to group those into folders based on functionality. I guess each product owner's mileage may vary here, but my point is do whatever it is you need to do as a product owner to be able to comprehend and manipulate your work queue with facility.

#### User Stories and Product Backlog summary and suggestions:

*   Use the terms "Work Queue" and "Work Item" instead
*   Don't feel obligated to use the "As an X, I want to Y, so I can Z" template if it is unnatural (But do stick with it when it is appropriate)
*   Put how ever much detail is needed into your Work Items
*   Allocate sufficient Product Owner time to keep the work queue healthy
*   Do what's needed to organize large work queues for easy manipulation by the product owner

### Sprint Planning, Estimation, and Time Tracking

In terms of planning and estimating, even with the shorter four week sprints, there are still some difficulties built into the Scrum process in my experience. We used story points, a somewhat abstract relative unit of measurement designed to express relative difficulties between two stories, not necessarily any absolute measure of time, effort, or difficulty. For me personally, this just does not feel natural or come easily. First, I don't think about estimates in relative comparison normally. I don't think task A is easy, and task B is four times as hard as task A. As a general rule, I think most people don't think accurately in terms of multiplicative values. Conceptualizing the idea that 13 story points is 6.5 times more effort than 2 story points doesn't come naturally for me. Given any two stories, I can tell you which one is harder, and I could probably use that basic operation to sort a list of tasks by difficulty, but computing the relative sizes of two along the Fibonacci scale is awkward for me. Secondly, the seemingly arbitrary and perhaps a bit weird use of the Fibonacci sequence just sticks out a bit to me as obtuse. Here's my suggested improvements. When it comes to story points, I really believe you need three and only three values: small, medium, large. Fibonacci gives us 1 2 3 5 8 13 21, but 1s and 2s were not particularly common in our backlog, and when we saw a 13 we generally panicked and broke it into smaller pieces. That's what I suggest. If you have three or four stories that are truly super easy (1 or 2 in Fibonacci story points), just stick them all into one story and call it small. If you have something that seems very hard, like it's going to take one developer half the sprint to do it, break it up into a large and a few mediums. I think the "small, medium, large" terminology has another benefit of being obvious even when discussing with someone non-technical or not familiar with Scrum or Story Points. No explanation is required. Story Points using Fibonacci are subtle enough to require explanation, and perhaps they don't add enough value to justify their subtlety.

OK, so now onto the sprint planning meeting. The default scrum schedule has a single marathon sprint planning meeting at the beginning of each sprint. For our team of five developers with four week sprints, we are looking to estimate somewhere around 600 hours worth of tasks ranging in granularity from 4-30 hours. It's just too much to focus on in a single session (again, my opinion). After two and a half hours of this, I'm bleary-eyed and fried and unable to motivate myself to do the kind of careful thinking required to make the task lists complete and accurate. I start falling into wanting to list the same three tasks for every story: 1\. Figure it out 2\. Code it 3\. Test it. My suggestion is that this be done for one hour a week as many as four times during the sprint if needed (probably 3 of these will get the job done) just to break it up into manageable chunks.

Now, another point on the sprint planning meetings. Our goal was to take user stories that had story points and acceptance criteria and define a full set of tasks and estimates for five developer-months worth of time in a single session, and then try not to have to add/remove/change during the sprint. (Note, the try not to have to add/remove/change is my own understanding, although my editor pointed out that Scrum itself has no such restriction and allows for task adjustments - focusing only on remaining work. However, it seems the goal is to define the tasks to whatever degree possible at the beginning or we wouldn't bother doing it in the first place, but then adjustments are accomodated). In any case, I wonder whether this is a realistic, achievable goal. Or let me say that in my experience at least about 10% churn in the tasks as development progresses (regardless of what overall methodology I am working within) seems to be my limit and I can't get it more accurate than that up front. So if the team is OK with somewhere around 10% task churn mid-sprint, then all is well.

When it comes to estimating in hours an individual task in the backlog, our team was developing a new product from scratch with a team of all highly experienced engineers. So we actually ended up having pretty good interchangeability between developers where several different people could complete a task and generally take about the same amount of time to do it. However, when working on an big existing code base, it can be an order of magnitude difference in the estimate between when someone who has already learned a complex subsystem and implemented a similar change does a task verses someone else doing it for the first time. I think if we want real accuracy we need some way to model this more accurately. I'm not sure how best to do this. Maybe one task for learning curve that gets skipped if it's not needed because the person who completes the task didn't need it? I don't have a good suggestion to improve this yet. Also, along similar lines, in general I always get nervous when one person (or a team) creates estimates for work that will be completed by another person. I think there's just a lot of risk there. Again, I don't have an alternative to propose at this time.

With regard to ordering the work queue items in the queue, and thus determining which ones get into the sprint, I think in general the scrum notion that the product owner does this and it's based on business value to the product owner is reasonable and beneficial for the most part. However, we also tried to adhere to this order for the order in which items were implemented during the sprint, and I think in many cases this didn't work out as well as it could have. Even in the backlog, I feel that a certain amount of the time, a logical or technical dependency will suggest a different backlog item order than strict product owner importance. But for now I'm OK with the product owner importance ordering for the backlog. However, inside the sprint, I think it might work out better to allow the scrum team a certain amount of discretion and control of the order of implementation on any technical or logistical grounds they feel will help. Within a sprint, we bumped up against a fair number of interdependencies where two people would need to heavily edit the same source code file on the same day, or one person was blocking waiting for another person to complete some code needed to build their feature. I can understand that taking the most important item and implementing it last is probably not acceptable, but I think some well-reasoned adjustment should be allowed. Ultimately, I think more stories will get completed due to the efficiency gains. I think a good guideline would be just to discuss these proposed changes to implementation order with the product owner during the daily Scrum call, and based on the status of the burn down chart and how things seem to be going, the product owner may permit or veto a re-ordering.

#### Sprint Planning, Estimation, and Time Tracking summary and suggestions:

*   Use small, medium, large instead of Fibonacci story points
*   Divide the sprint planning across several meetings throughout the sprint, never exceeding the motivation/attention span threshold for this somewhat tedious endeavor
*   Define criteria under which it is OK for developers to add/remove/change tasks during the sprint
*   May need some way to estimate tasks differently depending on who implements them
*   Within a single sprint, team should be allowed to make implementation order changes that will help with efficiency with consent of the product owner