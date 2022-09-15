---
layout: post
title:  Integrate Stripe Checkout in Rails application
date:   2021-12-21 15:05:55 +0300
image:  /assets/images/blog/post_2.png
author: Jacky
tags:   Rails, Stripe, Payment Gateway
---

Checkout creates a secure, Stripe-hosted payment page that lets you collect payments quickly. It works across devices and can help increase your conversion. Checkout makes it easy to build a first-class payments experience:

- Designed to remove friction—Real-time card validation with built-in error messaging
- Mobile-ready—Fully responsive design with Apple Pay and Google Pay
- International—Supports over 25 languages and multiple payment methods
- Customization and branding—Customizable buttons and background-color
- Fraud and compliance—Simplified PCI compliance, SCA-ready, and CAPTCHAs to mitigate card testing attacks
- Additional features—Apply discounts, collect taxes, send email receipts, and more

We can try to check how Stripe Checkout work at the demo page [link](https://checkout.stripe.dev)
 

Stripe Checkout API
To integrate with the Stripe Checkout, we need to init the Session object first, then it will be redirected to Stripe hosted page. Check Session API at [link](https://stripe.com/docs/api/checkout/sessions/create?lang=ruby)

```ruby

  require 'stripe'
  Stripe.api_key = 'sk_test_Ky9Bh3nPYW9sMLWHS0X3QfTx'

  Stripe::Checkout::Session.create({
    success_url: 'https://example.com/success',
    cancel_url: 'https://example.com/cancel',
    line_items: [
      {price: 'price_H5ggYwtDq4fbrJ', quantity: 2},
    ],
    mode: 'payment',
  })

```

After the payment success or canceled, it will redirect back to the success_url and cancel_url. At this step, we can check and set the subscription or one-time payment to paid or not. Subscription API is at [link](https://stripe.com/docs/api/subscriptions/retrieve?lang=ruby)

```ruby

  checkout_session = Stripe::Checkout::Session.retrieve(params[:session_id])
  subscription_id = checkout_session['subscription']
  subscription = Stripe::Subscription.retrieve(subscription_id)

```

How to integrate into Rails system
It's easy to inegrate into the Rails system with steps

#### 1 - Add subscriptions controller, in the create action, init the Stripe::Session object. then redirect to the session.url and go to Stripe checkout page

```ruby

  session = Stripe::Checkout::Session.create(
    payment_method_types: ['card'],
    customer_email: ''<email>',
    subscription_data: {
      items: [{ plan.stripe_id }],
    },
    success_url: success_url(callback_url),
    cancel_url: callback_url
  ) 
  redirect_to session.url

```

#### 2 - In the subscription show page, check the session_id params and update the subscription status

```ruby

  checkout_session = Stripe::Checkout::Session.retrieve(params[:session_id])
  subscription_id = checkout_session['subscription']
  subscription.update stripe_id: subscription_id, is_paid: true

```

#### 3 - Add the Webhooks to listen to events when the subscription is canceled, paused or charged failed

```ruby

  Stripe::WebhookEndpoint.create({
    url: 'https://example.com/my/webhook/endpoint',
    enabled_events: [
      'charge.failed',
      'charge.succeeded',
    ],
  })

```