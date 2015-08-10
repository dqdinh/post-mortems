A list of post mortems!

[Knight Capital](http://pythonsweetness.tumblr.com/post/64740079543/how-to-lose-172222-a-second-for-45-minutes). A combination of conflicting deployed versions and re-using a previously used bit caused a $460M loss.

[Etsy](https://codeascraft.com/2012/01/23/solr-bittorrent-index-replication/). Sending multicast traffic without properly configuring switches caused an Etsy global outage.

[Healthcare.gov](https://plus.google.com/+AndreasSchou/posts/FhWtABz7ew9).

[Sweden](http://www.pri.org/stories/2012-02-23/new-clues-emerge-centuries-old-swedish-shipwreck). Use of different rulers by builders caused the _Vasa_ to be more heavily built on its port side and the ship's designer, not having built a ship with two gun decks before, overbuilt the upper decks, leading to a design that was top heavy. Twenty minutes into its maiden voyage in 1628, the ship heeled to port and sank.

[NASA](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter). Use of different units of measurement (metric vs. English) caused Mars Climate Orbiter to fail. This is basically the same issue Sweden ran into in 1628 with its ship.

[Stack Overflow](http://stackstatus.net/post/96025967369/outage-post-mortem-august-25th-2014). A bad firewall config blocked stackexchange/stackoverflow.

[Microsoft](http://azure.microsoft.com/blog/2014/11/19/update-on-azure-storage-service-interruption/). A bad config took down Azure storage.

[Cloudflare](https://blog.cloudflare.com/todays-outage-post-mortem-82515/). A bad config (router rule) caused all of their edge routers to crash, taking down all of Cloudflare.

[Google](http://googleblog.blogspot.com/2014/01/todays-outage-for-several-google.html). A bad config (autogenerated) took down most Google services.

[Google](https://code.google.com/p/chromium/issues/detail?id=165171#c27). A bad config caused a quota service to fail, which caused multiple services to fail (including gmail).

[Facebook](https://blog.thousandeyes.com/facebook-outage-deep-dive/). A bad config took down both Facebook and Instagram.

[Amazon](http://aws.amazon.com/message/680587/). Elastic Load Balancer ran into problems when "a maintenance process that was inadvertently run against the production ELB state data". 

[Valve](https://blog.thousandeyes.com/steam-outage-monitor-data-center-connectivity/). Although there's no official postmortem, it looks like a bad BGP config severed Valve's connection to Level 3, Telia, and Abovenet/Zayo, which resulted in a global Steam outage.

[GPS/GLONASS](http://www.gps.gov/governance/advisory/meetings/2014-06/beutler1.pdf). A bad update that caused incorrect orbital mechanics calculations caused GPS satellites that use GLONASS to broadcast incorrect positions for 10 hours. The bug was noticed and rolled back almost immediately due to (?) this didn't fix the issue.

[Gitlab](https://docs.google.com/document/d/1ScqXAdb6BjhsDzCo3qdPYbt1uULzgZqPO8zHeHHarS0/preview?sle=true&hl=en&forcehl=1#heading=h.dfbilqgnc5sf). After the primary locked up and was restarted, it was brought back up with the wrong filesystem, causing a global outage.

[Heroku](https://status.heroku.com/incidents/642?postmortem). Having a system that requires scheduled manual updates inevitably resulted in an error which caused US customers to be unable to scale, stop or restart dynos, or route HTTP traffic, and also prevented all customers from being able to deploy.

[Bitly](http://blog.bitly.com/post/85260908544/more-detail). Hosted source code repo contained credentials granting access to bitly backups, including hashed passwords.

Sun/Oracle. Sun famously didn't include ECC in a couple generations of server parts. This resulted in data corruption and crashing. Following Sun's typical MO, they made customers that reported a bug sign an NDA before explaining the issue.

[Kickstarter](https://www.kickstarter.com/backing-and-hacking/the-day-the-replication-died). Primary DB became inconsistent with all replicas, which wasn't detected until a query failed. This was caused by a MySQL bug which sometimes caused `order by` to be ignored.

[AppNexus](http://techblog.appnexus.com/2013/2013-09-17-outage-postmortem/). A double free revealed by a database update caused all "impression bus" servers to crash simultaneously. This wasn't caught in staging and made it into production because a time delay is required to trigger the bug, and the staging period didn't have a built-in delay.

[Google](https://code.google.com/p/nativeclient/issues/detail?id=2508). Checking the vendor string instead of feature flags renders NaCl unusable on otherwise compatible non-mainstream hardware platforms.

[Etsy](https://blog.etsy.com/news/2012/demystifying-site-outages/). First, a deploy that was supposed to be a small bugfix deploy also caused live databases to get upgraded on running production machines. To make sure that this didn't cause any corruption, Etsy stopped serving traffic to run integrity checks. Second, an overflow in ids (signed 32-bit ints) caused some database operations to fail. Etsy didn't trust that this wouldn't result in data corruption and took down the site while the upgrade got pushed.

[Dropbox](https://blogs.dropbox.com/tech/2014/01/outage-post-mortem/). This postmortem is pretty thin and I'm not sure what happened. It sounds like, maybe, a scheduled OS upgrade somehow caused some machines to get wiped out, which took out some databases.

[Joyent](https://www.joyent.com/blog/manta-postmortem-7-27-2015). Operations on Manta were blocked because a lock couldn't be obtained on their PostgreSQL metadata servers. This was due to a combination of PostgreSQL's transaction wraparound maintence taking a lock on something, and a Joyent query that unecessarily tried to take a global lock.

[CircleCI](http://status.circleci.com/incidents/hr0mm9xmm3x6). A GitHub outage and recovery caused an unexpectedly large incoming load. For reasons that aren't specified, a large load causes CircleCI's queue system to slow down, in this case to handling one transaction per minute.

[GoCardless](https://gocardless.com/blog/zero-downtime-postgres-migrations-the-hard-parts/). All queries on a critical PostgreSQL table were blocked by the combination of an extremely fast database migration and a long-running read query, causing 15 seconds of downtime.

[CCP Games](http://community.eveonline.com/news/dev-blogs/behind-the-scenes-of-a-long-eve-online-downtime/). A problematic logging channel results in cluster nodes dying off during the cluster start sequence after rolling out a new game patch, resulting in a day's worth of troubleshooting and extended downtime.

[CCP Games](http://community.eveonline.com/news/dev-blogs/about-the-boot.ini-issue/) In 2007, a typo and a name conflict caused the installer to sometimes delete the *boot.ini* file on installation of an expansion for *EVE Online* - with [consequences.](https://www.youtube.com/watch?v=msXRFJ2ar_E)

[Amazon](https://aws.amazon.com/message/65648/). Major Amazon EC2/RDS outage in US East Region, April 21 - 24, 2011. Human error during a routine networking upgrade led to a resource crunch, exacerbated by software bugs, that ultimately resulted in an outage across all US East Availability Zones, affecting many popular websites, as well as a loss of 0.07% of volumes.

[Netflix](http://techblog.netflix.com/2012/10/post-mortem-of-october-222012-aws.html). Netflix's extensive preparations enable them to gracefully handle a degradation of Amazon EBS service.

[Medium](https://medium.com/medium-eng/the-curious-case-of-disappearing-polish-s-fa398313d4df). Due to a series of unfortunate events, Polish users were unable to use their "Ś" key on Medium.

[Valve](https://github.com/valvesoftware/steam-for-linux/issues/3671). Steam's desktop client deleted all local files and directories. The thing I find most interesting about this is that, after this blew up on social media, there were widespread reports that this was reported to Vavle months earlier. But Valve doesn't triage most bugs, resulting in an extremely long time-to-mitigate, despite having multiple bugreports on this issue.

[Amazon](http://aws.amazon.com/message/2329B7/). An unknown event caused a transformer to fail. One of the PLCs that checks that generator power is in phase failed for an unknown reason, which prevented a set of backup generators from coming online. This affected EC2, EBS, and RDS in EU West.

[Amazon](https://aws.amazon.com/message/67457/). Bad weather caued power failures throughout AWS US East. A single backup generator failed to deliver stable power when power switched over to backup and the generator was loaded. This is despite having passed a load tests two months earlier, and passing weekly power-on tests.

[Sentry](http://blog.getsentry.com/2015/07/23/transaction-id-wraparound-in-postgres.html). On Monday, July 20th, Sentry was down for most of the US working day due transaction ID Wraparound in Postgres.

[Spotify](https://labs.spotify.com/2013/06/04/incident-management-at-spotify/). Lack of exponential backoff in a microservice caused a cascading failure, leading to notable service degradation.

Unfortunately, most of the interesting post-mortems I know about are locked inside confidential pages at Google and Microsoft. Please add more links if you know of any interesting public post mortems!  is a pretty good resource; other links to collections of post mortems are also appreciated.

## Other lists of postmortems

[Ed S's postmortem collection](https://plus.google.com/communities/115136140203018391796).

[John Daily's list of postmortems (in json)](https://github.com/macintux/Service-postmortems).

[Jeff Hammerbacher's list of postmortems](http://www.quora.com/Jeff-Hammerbacher/Post-mortems).

[Wikimedia's postmortems](https://wikitech.wikimedia.org/wiki/Incident_documentation).



## Contributors

* Dan Luu
* Julia Hansbrough
* Nat Welch
* James Graham
* Grey Baker
* Amber Yust
* Connor Shea
* Matt Day
* Raul Ochoa
* John Daily
* Kunal Mehta
* Ahmet Alp Balkan
* Jason Dusek

