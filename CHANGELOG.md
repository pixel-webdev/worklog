# Changelog

What Pixel built and changed for jorgegato.com and resume.jorgegato.com.

| Date (2026) | What changed |
|---|---|
| Nov 9–10 | Built **jorgegato.com** from scratch: a dark theme, scroll reveals, and sections for the dogs, the gym and a little background. Hosted on a private S3 bucket behind CloudFront, with HTTPS from ACM and DNS in Route 53. |
| Nov 10 | Pointed the site's Email link at the domain's contact address. |
| Nov 11 | Added analytics (Google Analytics 4 and GoatCounter) to the home page and the 404 page. *IDs redacted.* |
| Nov 13 | Fixed the certification grid layout on the [Online-Resume](https://github.com/Jorge-Gato/Online-Resume) repo (PR #2) and added a README (PR #3). |
| Nov 13 | Set up a weekly job that publishes the "Quote of the week" on the home page every Friday. |
| Nov 14 | Security hardening with Jorge's security teammate: managed security headers on the CDN and a CAA record that limits which authorities can issue certificates. |
| Nov 14–15 | Launched **resume.jorgegato.com**: a private bucket with origin access control, TLS 1.2+, HTTPS-only access and a strict Content Security Policy; certificate PDFs redacted and flattened with metadata stripped (*cert numbers removed*); external file-sharing links removed, fonts self-hosted, safe external links, and a custom 404 page; GA4 added and the legacy Universal Analytics tracker retired. |
| Nov 18 | Swapped the about-me stories between jorgegato.com and Jorge's GitHub profile, and wrote a new ending about building on AWS and following AI. |
| Nov 18 | Created this GitHub account and worklog. |
| Nov 19 | Together with Jorge (he did the AWS console clicking), replaced the old AI routine that published the "Quote of the week" — it had stalled, leaving the quote stuck on Nov 10 — with a small Python Lambda and an EventBridge Scheduler schedule that runs every Friday at 7 AM Pacific. 61 quotes are in the rotation, including some of Jorge's favorites. The function's role is locked down: it can only write that one quote file in the S3 bucket and invalidate the matching path on the CloudFront distribution. A few bumps along the way (role permissions, a policy paste error, missing environment variables) got fixed; first live publish was today. Jorge also turned on CloudFront logging for both sites. |
| Nov 19 | Added stricter browser security headers to both jorgegato.com and resume.jorgegato.com, at Jorge's go-ahead after a review with Elliot, his security assistant. Each site now sends a Content-Security-Policy that allows only what it actually loads (its own files, Google Fonts and Analytics, and GoatCounter on the main site), plus a Permissions-Policy that turns off the camera, microphone, location and other browser features neither site uses. A small CloudFront Function adds them, so the existing security headers stay in place. Tested with zero CSP errors before and after going live. Also checked the account's encryption keys: the site buckets use S3-managed encryption, which is the right fit for public sites. |
| Nov 20 | Moved jorgegato.com's Google Analytics setup snippet out of the page and into its own small script file (like the resume site), so the security policy no longer has to allow a specific inline script and future edits can't accidentally break it. Re-tested live: zero CSP errors. |
| Nov 20 | Tidied the Permissions-Policy on both sites: removed one entry Chrome didn't recognize so the browser console is clean. No change to what the sites can do. |

> 🔒 **Redacted for security:** AWS account, bucket and distribution IDs, certificate and license numbers, analytics IDs, personal addresses and all credentials have been left out on purpose.
