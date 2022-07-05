---

title: API Rate Limits
excerpt: Explanation of the rate limits to understand what is an expected API volume to send to Stardust
category: STARDUST_APIS_ID
slug: api-rate-limits
order: 3

---

The Stardust API has limits for multiple reasons. One, being to make sure we can provide performance up to a certain threshold. Two, to make sure that a malicious user can not DDoS the API by spamming the API with traffic and knock out other users. The limits are as follows:

### API Limits by Chain

| Limit Type                | ImmutableX  | Polygon     | Solana      |
| ------------------------- | ----------- | ----------- | ----------- |
| RPS (Requests per Second) | 5 RPS       | 10 RPS      | 10 RPS      |
| Bursting queue cap        | 10 Requests | 30 Requests | 30 Requests |
| Monthly Request Limit     | 10 Million  | 10 Million  | 10 Million  | 


#### Need more performance?
If you've completed you development and your ready to start testing the API, but are realizing the API limits are below your forecasted demand, please reach out to our Customer Success team and they can help you at : https://www.stardust.gg/get-started