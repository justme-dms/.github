# Security Policy

JustMe Digital Marketing Services builds and operates multi-tenant business
platforms that hold operational and commercial data on behalf of the businesses
that run on them. We take reports seriously and we would rather hear from you.

## Reporting a vulnerability

Email **it.support@justmedms.com** with `SECURITY` in the subject line.

Please include, as far as you are able:

- What the issue is and roughly how severe you believe it to be
- The steps to reproduce it, or a proof of concept
- Which host, endpoint, or component is affected
- Anything you think we would otherwise miss

You do not need a formal write-up. A short, clear email beats a delayed report.

**Please report privately.** Do not open a public issue, post the details
publicly, or disclose to a third party before we have had a chance to fix it.

## What to expect

| Stage | Target |
|---|---|
| Acknowledgement that we received your report | within 3 business days |
| An initial assessment and a severity judgement | within 10 business days |
| Progress updates while we work on a fix | at least every 10 business days |

If a report affects data belonging to one of our clients, we will notify that
client according to our agreement with them. We will tell you when a fix has
shipped, and we are happy to credit you publicly if you would like that — just
say so in your email.

## Scope

**In scope for unsolicited testing:** this organization's public website and the
public content published in these repositories. Test those freely within the
limits below.

**Everything else requires written authorization first.** Our platforms are
private systems holding commercial, payroll, and personnel data belonging to the
businesses that run on them. We cannot consent on their behalf, and we are not
willing to have live operations probed by surprise — our own rate limiting and
account lockout would lock real staff out of their jobs while you worked.

If you believe you have found something affecting a platform, **email us a
description first and stop there.** We will come back to you with a test
environment, credentials, and written authorization defining what you may touch.
That is a real offer, not a brush-off — we would rather run a scoped engagement
than have you guess where the line is.

Out of scope, and please do not attempt them:

- Denial of service, load testing, or anything that degrades service for real users
- Social engineering of our staff, our clients, or our clients' customers
- Physical attacks against offices or personnel
- Automated scanner output submitted without a demonstrated, exploitable impact
- Findings in third-party services we consume — report those to the vendor
- Accessing, modifying, exfiltrating, or retaining data that is not your own

If you encounter client or personal data while testing, **stop, do not retain a
copy, and tell us immediately** in your report.

## Safe harbour

If you make a good-faith effort to follow this policy **and stay inside the scope
above**, we will not pursue legal action against you for your research, and we
will say so to anyone who asks. Act in good faith, avoid privacy violations and
service disruption, and give us a reasonable window to remediate before
disclosing.

This protection does not extend to testing a platform without the written
authorization described above. We cannot waive rights that belong to the
businesses whose data those systems hold.

We do not currently operate a paid bug bounty.

## A note on this organization's repositories

The platform repositories here are **private commercial software**. The public
repositories in this organization contain documentation and the organization's
website only — no application source, no credentials, and no configuration.
Reports about the public content are welcome all the same.
