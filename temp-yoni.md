## ⚪ ️ 3.5. Watch how the content is served over the network

:white_check_mark: **Do:** Apply some active monitor that ensures the page load under real network is optimized - this includes any UX concern like slow page load or unminified bundle. The inspection tools market is no short: basic tools like [pingdom](https://www.pingdom.com/), AWS cloudwatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) can be easily configured to watch whether the server is alive and response under a reasonable SLA. This only scratches the surface of what might get wrong, hence it's preferable to opt for tools that specializes in frontend (e.g. [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) and perform richer analysis. The focus should be on symptoms, metrics that directly affects the UX, like page load time, [meaningful paint](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [time until the page gets interactive (TTI)](https://calibreapp.com/blog/time-to-interactive/). On top of that, one may also watch for technical causes like ensuring the content is compressed, time to first byte, optimize images, ensuring reasonable DOM size, SSL and many others. It's advisable to have these rich monitors both during development, as part of the CI and most important - 24x7 over the production's servers/CDN

<br/>

:negative_squared_cross_mark: **Otherwise:** It must be disappointing to realize that after such a great care for crafting an UI, 100% functional tests passing and and sophisiticated bundling - the UX is horrible and slow due to CDN misconfiguration

<br/>

### :clap: Doing It Right Example: Lighthouse page load inspection report

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

<br/>
