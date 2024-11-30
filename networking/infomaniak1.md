# Infomaniak.com Swiss Cloud Provider Technical Support for SMTP problem

One fine day, when I am retired, and will have more time at hand to "have fun" than I do these days, I'll switch my personal email to [being fully decentralized self-hosting](https://github.com/vorburger/awesome-decentralized-internet-web3-blockchain-p2p-security-world-cloud).

But these days fully running [your own MTA](https://en.wikipedia.org/wiki/Message_transfer_agent) properly requires more time than I personally am currently willing to give it.

In the meantime, I run my personal email in an admittedly somewhat weird set-up, like this:

## Incoming

1. The domain registrar is **[Infomaniak.com](https://www.infomaniak.com)** a great Swiss Cloud Provider, which I can recommend - read on!

1. The [DNS NS](https://en.wikipedia.org/wiki/Name_server#Authoritative_name_server) for it is a [Cloud DNS on GCP](https://cloud.google.com/dns).
   (This doesn't really make all that much sense, as it would be much simpler to just use Infomaniak's DNS; other than being "historical", and a tiny little bit cheaper instead of paying them extra for Anycast . But hey, maybe we'll [throw some generative AI](https://www.youtube.com/watch?v=-P-ein58laA) at DNS, too? 😼)

1. The [`MX`](https://en.wikipedia.org/wiki/MX_record) on that is `mta-gw.infomaniak.ch`. And I've configured that to forward my email to Gmail.

1. The Email _Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM)_ and _[Domain-based Message Authentication, Reporting and Conformance](https://dmarc.org) (DMARC; see [DMARC on Wikipedia](https://en.wikipedia.org/wiki/DMARC))_ related DNS records have also been set-up. (One day when I have nothing more fun to do I'll also add one for _[Brand Indicators for Message Identification (BIMI)](https://bimigroup.org)._

## Outgoing

1. In Gmail, to reply, or write new email, I have configured it to [treat as an alias](https://support.google.com/a/answer/1710338) and to [send emails from a different address or alias](https://support.google.com/mail/answer/22370) using SMTP `mail.infomaniak.com` as per [Infomaniak's FAQ #468](https://faq.infomaniak.com/468).

This worked great through another set-up, which I had for many years before switching to Infomaniak, and at first seemed to "mostly" work fine with them as well - until it sometimes didn't, and "bounced" from Mail Delivery Subsystem `<mailer-daemon@googlemail.com>` with: _"You're sending this from a different address or alias using the 'Send mail as' feature. The settings for your 'Send mail as' account are misconfigured or out of date. The response from the remote server was: 535 5.7.0 Too many authentication failures"._

So I opened a Support Ticket with Infomaniak, describing the problem - actually not really hoping for much of a real reply, to be honest... but to my surprise, they actually properly debugged it! And replied: "The error you have encountered is due to the fact that the IP address used by Google services has been flagged as having a bad reputation in a public blacklist. This blacklist is used to protect our users from potential threats. We have taken steps to adapt our system accordingly and hope that this will resolve the problem."

**Wow. Cool. Serious real technical support is getting rarer these days than it naturally just should be. I'll let some friends know about this positive experience with Infomaniak!**

## PS: On Email Security...

I cannot write about Email without a PS about this: Email is not private. Sending e.g. your tax documents and medical information (or what not) by email is pretty dumb actually - but fairly common, of course. While Email nowadays is at least encrypted in-transit, it will definitely be in clear-text at reception, and depending on where you have your Inbox, may well also be in clear-text when stored at rest. But email's (in)security is "by old Internet design", and very difficult to change comprehensively, at scale. [Proton Mail tries](https://proton.me/blog/what-is-end-to-end-encryption), but that of course only really works between Proton Mail users, as well as to and from the 0.0000000001% of _[geeks or nerds](https://www.youtube.com/watch?v=tg7EZCM7IlY) 🤣_ who actually [have a PGP key](https://www.vorburger.ch/gpg/vorburger.pgp.key.asc). (And yes, [Proton Mail's "Password-protected" Emails](https://proton.me/support/password-protected-emails) are a "fun" idea, but I suspect that the "usability barrier" is just too high for recipients... I doubt the required out-of-band secret sharing really makes sense to most common mortals? But perhaps I should migrate my personal email setup to [Proton Mail with custom domain](https://proton.me/support/custom-domain) anyway, they even nicely directly support [SPF, DKIM, and DMARC](https://proton.me/support/anti-spoofing-custom-domain)...)

This is fundamentally wrong in 2024, and actually makes Email less secure than e.g. most of whatever-if-your-favourite-instant-messenger ([mine is Threema](https://threema.ch); of the "big" ones, only Telegram does not encrypt, by default). Perhaps I should just use email less...

<!-- PS: I briefly considered whether this post reveals anything "secret" which I shouldn't write about, but concluded that the information contained herein is de-facto public for anyone technical anyway. Please let me know if I missed something! -->
