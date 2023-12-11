# Week 0 — Billing and Architecture


Budget Creation Using CLI:
    aws budgets create-budget \
        --account-id 405121720975 \
        --budget file://aws/json/budget.json \
        --notifications-with-subscribers file://aws/json/budget-notification-with-subscribers.json


Create SNS Topic
    1. We need an SNS topic before we create an alarm.
    2. The SNS topic is what will delivery us an alert when we get overbilled
    3. aws sns create-topic

We'll create a SNS Topic
    aws sns create-topic --name billing-alarm

which will return a TopicARN

We'll create a subscription supply the TopicARN and our Email

aws sns subscribe \
    --topic-arn="arn:aws:sns:us-east-1:405121720975:billing-alarm" \
    --protocol=email \
    --notification-endpoint=kaviarasu_ns@icloud.com

Check you email and confirm the subscription