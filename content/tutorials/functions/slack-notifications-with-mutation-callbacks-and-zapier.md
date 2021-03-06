---
alias: dah6aifoce
path: /docs/tutorials/slack-notifications-with-mutation-callbacks
layout: TUTORIAL
preview: slack-zapier-notification-mutation-callback.png
title: 'Sending Slack Notifications with GraphQL & Zapier'
description: Use Zapier to create a Slack integration for your GraphQL server and get Slack notifications whenever a certain mutation is executed.
tags:
  - mutation-callbacks
  - functions
  - slack
  - zapier
  - open-source
related:
  further:
    - uh8shohxie
    - ahlohd8ohn
  more:
    - saigai7cha
    - soiyaquah7
---

# Sending Slack Notifications with GraphQL & Zapier

[Slack](https://slack.com/) is very popular to handle the internal communication for teams. Slack notifications help to easily stay uptodate with things like successful or failing builds. In this guide we will focus on another use case: tracking business related events like when a new user signs up or a purchase is made.

We will use Mutation Callbacks to trigger the Slack plugin offered by [Zapier](https://zapier.com/)'s webhook feature.

## 1. Preparation

We need to setup the individual parts before we can wire everything up.

### 1.1 Setting up Slack

You'll need a new Slack team you administrate - unless your team members don't mind a few notifications in the `random` channel... [Create a free Slack team](https://slack.com/create) and you're good!

### 1.2 Setting up Zapier

If you don't use Zapier yet, [sign up for free](https://zapier.com/sign-up/).

### 1.3 Setting up Graphcool

You can create a new Graphcool project so you can freely experiment. If you have no Graphcool account yet, [create a free account here](https://graph.cool).

Head over to your Graphcool project and add a new required `name` field of type String to the `User` type. We will print a user's name in the Slack channel whenever a new one signs up.

## 2. Creating a new mutation callback to a Zapier webhook

Next we will add a new mutation callback to a Zapier webhook, so that whenever a new user is created the Zapier webhook will be notified.

### 2.1 Creating a new Zapier webhook

Head over to your Zapier account and create a new Zap. Choose `Webhooks by Zapier` for the trigger and select `Catch Hook`. When you are being prompted to test the webhook, switch back to your Graphcool project to setup a new mutation callback.

### 2.2 Setup the mutation callback

* Choose `User is created` as the trigger mutation
* For the payload, enter this query:

    ```graphql
    query {
      createdNode {
        id
        name
      }
    }
    ```
* Paste the webhook url obtained from Zapier into the handler url field.

To progress further with Zapier, we will execute a test mutation.

### 2.3 Run test mutation

Run this mutation in your Graphcool playground for the Simple API:

```graphql
mutation {
  createUser(name: "Nilan") {
    id
  }
}
```

Back in your new Zap trigger, you should shortly see the incoming data. After you confirmed that everything is correct, now you can move on to creating the Slack notification action

### 2.4 Creating a Zapier action

As the Zapier action, we can now add a new Slack notification. Choose the `Slack` action and select `Send Channel Message`. Link your Slack account to your Zapier account and you should be good to go. Pick your channel, and create a message like `User <name> signed up (<id>)` where `<name>` and `<id>` have to be replaced by selecting the fields provided by Zapier.

## 3. Firing mutation callbacks

At this point you are good to go - if you want, you can run the mutation from above again (you can be creative and use your name this time!) and confirm that the Slack notification appears.

## 4. Next Steps

You just setup a mutation callback that eventually notifies you whenever a new user signs up, neat!

 If you want to read more about mutation callbacks, head over to the [reference documentation](!alias-ahlohd8ohn) or read [this guide on email notifications with mutation callbacks and Mailgun](!alias-saigai7cha).
