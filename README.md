# oa-beta-landing-page-arch-issue
this OA's time requirement is 15 mins

### Problem Description - Debugging a system issue

Background
> As a beta offering for our product, we are trying out a new third-party recommendation service that uses ML to suggest a next action for users. We surface those next actions are part of the user's landing page when they sign in - maybe it's sending an important message, checking off an important todo, etc.
> The beta service has been running for a couple of weeks without problems. 3% of users are feature-flagged into the beta.

Alerts!
> You're settling in at your desk after a delicious and energizing team lunch when you receive a performance alert from the monitoring system.
> - Rendering the beta landing page for a user is taking around 10 seconds, up from the normal average of 800ms
> - About 10% of the users in the beta are even triggering the dreaded 504 Gateway Timeout error

Architecture
> Here's a highly simplified diagram of the components used for rendering the Beta Landing Page:
![image](https://github.com/jayyu1/oa-beta-landing-page-arch-issue/assets/55224276/8f990e4e-ae21-474b-ab46-361b27ee3851)

> And here's a sequence diagram showing the flow of the request through the main components of the architecture involved in the beta:
![image](https://github.com/jayyu1/oa-beta-landing-page-arch-issue/assets/55224276/cf79509f-2073-40c4-b4ce-1adf8bdd1299)


Investigation Findings
> After some initial investigation, you've learned:

> - No frontend changes have been deployed recently touching that page
> - Only the beta landing page for users in the beta appears to be impacted
> - The status page for the 3rd party recommendation service doesn't show an outage


Your colleague has now temporarily removed all users from the beta, so the alert is over.

The Staff Engineer leading the investigation wants to use the "think alone, together" technique to brainstorm potential cuases for this performance problem without groupthink. They've asked you and a couple other engineers to help.

Write a short document that will be part of a pre-read before a working session together that starts soon.

Guidance from your co-worker

- list as many causes as you can think of for the observed behavior
- Focus on potential causes rather than debugging steps
- Consider the entire stack
- Both breadth and depth are helpful
- Note your judgement of relative likelihood, including a brief justification, where not obvious


---------------------------------------------------------------------------------------------------------
### My answer (maybe wrong, please comment, even my English)

Problem may happen when fetching user data from DB. As beta users become more and more, DB storage will be larger and larger, which might slow down DB's performance. Meanwhile, DB QPS will also increase as users are increasing, normal QPS of RDBMS is 1000.
1. for DB storage we can use sharding to overcome.
2. for DB QPS limitation, we can use Redis cache to handle most of user data request.


------------------------------------------------------------------------------------------------------------
### Feedback from this OA provider

Architecture debugging - brainstorming

Potential areas for improvement
1. Some top solutions provided more ideas about what could be causing slow recommendations and described them in detail.
2. We liked solutions that explained why the ideas they provided would cause the the endpoint to slow down.
