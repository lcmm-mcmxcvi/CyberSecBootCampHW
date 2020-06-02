### Submission Answers:

**Deliverable 1:** As future security professionals that may be involved with setting company security guidelines and policy, many considerations need to be taken when developing an account lockout policy.

A few questions to ask are: do we want to employ a stricter account lockout policy that requires us to also be prepared for more frequent user lockouts? The problem with overly restrictive lockout policy is that you'll likely deal with many more user requests to unlock accounts.

However, the main purpose of this task was to introduce you to understanding how account lockout policy is developed and enforced, so using the default Microsoft baselines can work here:

  `Account lockout duration 15 minutes.`

  `Account lockout threshold 10 invalid logon attempts.`

  `Reset account lockout counter after 15 minutes.`