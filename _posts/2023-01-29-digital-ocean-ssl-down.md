Oddly, my SSL cert on https://ding.so stopped working with a complaint of an invalid date. From what I could tell it was in fact still valid.

This is for my Mastodon instance hosted on a DigitalOcean droplet. The fix was a forced manual renewal, targeting the domain name specifically (despite being the only domain on the account).

For whoever needs it (probably me at a later date), this was the doc that resolved it: https://docs.digitalocean.com/support/how-can-i-renew-lets-encrypt-certificates/

---
5 minutes later...
---

I also just had a warning on the SSL for this site (https://ramone.co), and restarting my computer seemed to work - could have been a local issue..?
Although [Ding.so](https://ding.so) did appear to be down yesterday as well when accessed from mobile, so I'm not convinced. Some kind of global SSL conspiracy? Sure, must be.

