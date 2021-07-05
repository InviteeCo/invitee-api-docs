## Setting up webhooks

Webhooks are in place to let you know when a referral has been completed. The webhook will contain information about the referrer, referee & what reward, if any, is owed.

You can setup a new webhook configuration at: https://app.invitee.co/account/webhooks

The webhook request will contain a secret key in the header, which is generated when going through setup in the web dashboard. This is used to ensure that the request is coming from Invitee.

You must return a 200 response in your webhook handler. If a non 200 response is receieved, the request will be retried, with exponential back off of up to 5 minutes.

The request you receive will contain the following information:

```markdown
POST <Your Webhook URL>

Headers {
	  "x-webhook-secret-key": String
}

Body {
    "referrerCustomerId": String,
    "refereeCustomerId": String,
    "rewardType": String? (MONEY, PERCENTAGE, CREDIT),
    "referrerRewardAmount": Decimal?
    "refereeRewardAmount": Decimal?
}
```

## Tracking referral steps

In order for Invitee to process referrals, you need to let us know when key 'steps' have been completed. These steps are configured when you setup a campaign & are used to indicate a completed referral. Eg. Sign up + make purchase = referral reward.
  
There are two ways to track these steps, either via our REST api or through the SDK itself. If you choose to use the REST api then the following can be used as a reference for tracking.

```markdown
POST https://api.invitee.co/referral/referee/step
x-api-key: <YOUR API KEY>
Content-Type: application/json

Body {
    "customerId": String,
    "phoneNumber": String,
    "step": String
}
```
