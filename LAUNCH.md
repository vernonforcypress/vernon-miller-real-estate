# Launch guide

This is a review branch, not a deployed website. Business details were confirmed by the owner on October 24, 2026. The initial repository contained only README.md; it is preserved. No campaign repository or DNS settings were changed.

## Required before publication

The owner supplied DRE #01968262, phone, email, brokerage/team wording, REALTOR membership, bio facts and commercial specialty. These are now in site.json and the pages. Confirm final advertising wording and commercial engagement scope with the brokerage before running the manual deployment. approved=true records owner confirmation of the supplied business facts; it is not independent DRE verification or a legal compliance certification.

The current visible affiliations are supplied by the owner. Update both occurrences of the brokerage/team labels in scripts/build.mjs if their approved wording differs. Ensure the licensed brokerage is at least as prominent as the team. The footer uses 16px disclosure text, no smaller than other footer copy. Do not treat this template as legal certification.

The bio is limited to supplied positioning; it makes no claims about experience, sales, credentials, awards, or testimonials. The architectural illustration is decorative, not a property listing. No listing feed or contact-form delivery is represented as working. RealEstateAgent schema is emitted only after the launch gate passes, and contains only supplied identity, service area, URL and verified contact fields. Do not add a fictional office, reviews, ratings or hours.

Review: https://www.dre.ca.gov/files/pdf/re27.pdf and https://www.dre.ca.gov/files/pdf/forms/re559.pdf

## Preview and deploy

Requires Node 22 or newer; no packages needed.

- Run `node scripts/build.mjs` to build the review version in dist.
- Serve dist with any local static server.
- Run `node scripts/build.mjs --production` to verify the publication gate.
- Merge the reviewed pull request.
- In repository Settings → Pages choose GitHub Actions. Enable Pages if necessary.
- Configure the custom domain only as part of the confirmed domain cutover below.
- Run the “Publish verified website” workflow manually. It will refuse deployment while verification is incomplete.

Internal links use relative paths so the project-URL preview works. Production canonical URLs use https://vernmillerhomes.com. Launch at that domain before requesting indexing. Submit https://vernmillerhomes.com/sitemap.xml to Search Console after launch.

## DNS plan — do not apply until owner confirms

First identify the registrar/DNS provider and preserve all mail-related MX, SPF, DKIM and DMARC records. Verify the domain in GitHub account settings using the exact TXT record GitHub supplies. Do not invent the verification token. Protect existing campaign domains and repositories.

Once authorized, set repository Settings → Pages → Custom domain to vernmillerhomes.com. For Actions deployments the setting is necessary; a CNAME file in an artifact is not a substitute.

Primary domain DNS proposal:

| Type | Host | Value |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | vernonforcypress.github.io |

Check for conflicting A/AAAA/CNAME records before cutover. Do not create wildcard records. Allow DNS propagation, confirm the Pages DNS check and certificate, then enable Enforce HTTPS. Test apex and www, every page, sitemap, phone/email links and mobile navigation.

Secondary domain vernonmillerhomes.com requires an HTTP redirect service at the registrar or edge host; DNS alone cannot send a 301. After owner confirmation, configure both apex and www to return a permanent HTTP 301 to https://vernmillerhomes.com, preserving path and query. The redirect service must have valid HTTPS certificates for both secondary hostnames. Do not point the secondary domain at GitHub and assume it will redirect. Test response status, path preservation, query preservation and TLS before considering the cutover complete.

Official DNS reference: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

## Ongoing maintenance

Keep the public identity, license, affiliations, contact and service scope current. Review community resources periodically. If adding analytics, forms, IDX or third-party media, update privacy disclosures and verify accessibility and provider permissions first.
