---
layout: post
title: Why metrics are hard (and what to do about it)
---

Being metrics driven is a great way to build a software engineering culture that is empowers engineers and rewards for impact, while also helping teams remain aligned with organizational goals. Engineers with the autonomy to pick projects and settle debates using data and metrics are implicitly motivated to work on the most impactful projects. For this culture to work effectively, though, it’s important to pick the right metrics.

Unfortunately, this is surprisingly difficult to do. All metrics are proxies for real progress, and all proxies have inherent flaws and tradeoffs. Improving the process for choosing and iterating on metrics requires that we first understand some of these pitfalls:

### Core value proposition is usually hard to measure quantitatively
Metrics that reflect user experience are often focused on variables that are easy to track (e.g., number of clicks to an action, crash counts, response times). However, high-level user satisfaction, utility and overall quality of the experience (e.g. what fraction of my closest real-world friends are on this platform, how many matches in a dating app got into relationships) can be uncorrelated with these variables and may be difficult or impossible to measure.

With popular consumer products it is usually possible to attribute the impact of UX changes on broad areas such as engagement, revenue or utility using techniques like A/B testing, cohort analysis or NPS surveys. However, the vast majority of software does not have the luxury of large, active, and reachable user bases that can be constantly experimented upon or polled for opinions. Tracking user perception via surveys or interviews can also be an unreliable indicator of feature impact; it’s difficult to get longtime users to change their first (or worst) impressions of a system, and ‘anecdata’ can be misleading and skewed towards the loudest users.

### It’s tempting to optimize metrics in isolation
Being metrics-driven, by definition, narrows the focus of the organization to the metrics it deems the most important. It is sometimes possible to have projects that improve one metric and have no impact on the rest of the software product, but this is the exception rather than the rule. Software engineering is all about tradeoffs, and focusing on a metric is very likely to produce engineering decisions that trade off other metrics for the one you picked. One way to get around this is to have ‘counter’ metrics that will show you when you’ve gone too far in one direction. For example, when adding features to a product to improve engagement, it may be useful to also track metrics that would suffer if the product became too bloated or complex (e.g., app download size). Unfortunately, having too many metrics can be confusing and make metric design even more resource intensive.

### Metrics must be carefully presented
It’s essential to be detail oriented when presenting metrics. Small decisions such as the axis of a graph, the smoothing applied, or the choice to use raw numbers or instead of percentages or rates of change can dramatically impact how people perceive the metric, or measure progress on it. Cognitive biases cause people to look at numbers and charts and walk away with the perception that they understand the real story — after all, numbers don’t lie. The problem is that even if the numbers are real, you are almost always seeing only one thread of a complex story. It takes relevant experience to consider all the other, more complicated questions that a metric does not address.

It can also be tempting to add capabilities to slice and dice metrics to help attribute progress to features. For example, filtering to a subset of users or workloads can make changes to the metric more pronounced. This can be dangerous, since small statistical samples are likely to be noisy and indicate real change even when there is none. It’s almost always the right call to have people with knowledge and expertise to design opinionated and single-purpose dashboards and then trust them to interpret the data accurately.

### Flat metrics aren't sexy
One of the key negative externalities of being metrics focused is that it becomes difficult to recognize engineering that prioritizes quality and good system design upfront. It’s worth considering whether teams are being implicitly incentivized to quickly ship a system that has poor metrics in areas such as performance or reliability and then work to improve those metrics. In some cases this may be the right choice, but in others you might prefer that teams are slower or more thoughtful and ship a higher quality product or feature in one go.

The Occam’s razor explanation for a flat metric is usually that the projects the team chose did not have the desired impact. This may well be true, but warrants closer examination. Consider what would have happened had the team not worked on those projects at all. What are all the other metrics that moved while the high-level metric remained flat? For example, if the total usage for a backend service doubles (perhaps due to usability improvements) while the system overall reliability remains constant it’s probably fair to assume that without the team’s work the metrics would have been down instead of flat.

### Entire classes of engineering projects are never captured by high-level metrics
To demonstrate this effect, consider an engineering project you're familiar with that was well-represented by a key organizational metric. Chances are that this project moved a metric with a clear pre-existing trend line quickly and decisively in the direction it should go. This is also precisely the problem - many important engineering projects do not have this particular impact characteristic on high-level metrics. Some examples that I've seen are:

* Adding missing features or simplifying functionality when existing users have already worked around the lack of these (by building their own hacks/tools or by developing a deeper understanding of system internals than should be required).
* Opt-in features that take time to be adopted or are designed for a small set of power users.
* Projects that reduce operational overhead or improve developer productivity, which can be hard to measure unless they can be instrumented and compared with the status quo.
* Common-sense projects that are clearly a step forward, but are not recognized because it is too difficult to attribute their impact on a high-level metric (especially a noisy one).
* Fixes to edge-case, hard-to-reproduce bugs that in aggregate could move user perception of product quality and reliability

### One solution: Iterate on metrics cheaply
It’s extremely time-consuming to develop metrics that have made all the right trade-offs, build consensus around them with engineers and other stakeholders (especially if there are many), and then track and manage them such that changes in the metric can be root-caused quickly. What I’ve found to be useful is to have a process that lets me iterate on metric design as cheaply as possible while still ending up with an acceptable solution:

Pick the best high-level metric you can think of, and then try to attribute changes in the metric to a few key engineering projects. You will likely need to tweak it — remove outliers, correct for temporal patterns, focus on a subset of users, or consider narrower parts of the system. Engineers can help, and are more willing to do so if you approach with curiosity the question of why their projects don’t appear to have the impact they predicted or expected. When you have evolved the metric to the point where you can quickly attribute changes to these projects, stop.

This process is likely to get you to the point where you end up with the most meaningful high-level metric that is [operational](https://medium.com/@Pinterest_Engineering/4-steps-to-better-goals-and-metrics-dfe7ad7b2c9c) (one your team can affect). This addresses the most common criticisms of a metric — that it is either too high level to be operational, or too low-level to be meaningful. It’s much more straightforward to get all stakeholders to buy in and agree to use this kind of metric to evaluate future projects. It also helps to build consensus when communications about metrics are accompanied with language that recognizes the tradeoffs that have been made, and continually reiterates that the metric is just one of the many ways to measure progress.

*Thanks to Jeff Marcus, Rohan Katyal, Koulick Ghosh, Vedashree Bankar and several others who provided feedback and suggestions on earlier drafts of this post.*
