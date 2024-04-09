---
title: "Experimental protection from identity theft"
date: "2013-09-23"
tags: 
  - "security"
  - "experimental"
  - "identitytheft"
coverImage: "the_hat.jpg"
---

I have no idea how many accounts I've signed up for. As such, there are bits of my data all over the web. I understand why forums and shops want to know who I am, or at least connect some information to a pseudonym. This also helps me: I can set up email notifications and save my shipping address, and maintain a recognizable identity in online discussions. All commendable goals without which, life online could become anything from tedious to impossible. Nevertheless, I can't help but feel wary about having usernames, passwords, email addresses, shipping addresses, preferences, age etc. sprinkled all over.

[

\>

![Image by Katie](https://images.squarespace-cdn.com/content/v1/52375b95e4b030ffaec4c1f9/1379968402652-NSXU8QEJD5GOVEMPH2MW/2677247505_2c730354ab_b.jpg)



](http://www.flickr.com/photos/eightk/2677247505/)

[](http://www.flickr.com/photos/eightk/2677247505/)

<figcaption>



Image by Katie





</figcaption>

One way to deal with this is to use fake identities, but this approach brings with it multiple problems. Using a single fake identity makes this identity important to you. Losing control of it would not be as bad as having your real identity stolen, but it would have an effect anyhow. You could use a different fake identity for every site, but this requires a lot of work. It's also worth mentioning that using fake names is often a violation of ToS. Perhaps the biggest issue with the fake account approach is that you can't build online reputation that way. At least not reputation you can use on your resume.

Every site that thinks about setting up registration needs to ask some basic questions before taking the leap:

1. **Does registration really create value for you?** Registration should not be required only if it's one of the cool features provided by the platform you're using. I've seen forums that require registration before you can search the contents! Such "users" mean nothing for the site.
2. **Is there any value for the user?** If prior to registering, you're unable to demonstrate benefits from signing up, you will lose users.
3. **Are you up for the task of keeping your users data safe?** Will you stay up to date on news regarding vulnerabilities? Will you perform timely security updates? Will you stand up for your users if asked for data by powerful governmental entities?

I know what you're thinking. Hasn't sign in via Facebook, Twitter, Google+, etc. already solved this issue? Apps that choose this authentication strategy do not need to store your credentials. This is a great first step. But I'm talking about something quite else.

## What if your account could be stored outside of the service? 

There is no rule that says that a website must store user account information in the website's own database. Barring some exceptions, some of which I attempt to tackle a bit later, account information is usually only needed when the user is actually on the site. This means that in the majority of cases, the users themselves could supply their account information when logging into a service.

There would be multiple benefits:

- Not storing account information on a website makes that site less of an target for identity thieves. The payoff from hacking an individual site would be reduced close to zero.
- Login may no longer be required as the account information you provide essentially identifies the user.
- It would be easier for the user to keep track of their accounts.
- Deleting accounts would be much easier due to users controlling their own data. Of course we would have to trust that the merchant would not be keeping a copy.

The user could choose to use a cloud provider to store the account data, or use a local disk if so inclined. Cloud storage would be preferred as that would keep accounts accessible regardless what device or from where we were accessing a service.

## How would this work?

A merchant typically trusts in their database; the owner of the software has full control of what goes into the database. This is why merchants can trust the account data they save today. Data coming from the outside needs to be somehow verified. And verification becomes key If the account information would reside outside the merchant's service.

Thankfully cryptographers have already given us great tools to do just this. A basic verifiable object could be something like this:

- Account information is stored in an object which is signed with the merchant's private key. This signature can be validated using the merchant's public key. This means both parties know the signature and thus the data is created by the merchant.
- Signed account information would be encrypted with the public key of the user. This means only the user can read the account information. This makes it possible to store the account information on a third party service without making that service an enormous honeypot: all the honey is strongly encrypted!
- The merchant will store the signature and the OAuth user id it belongs to. With this information, the merchant may check that the account data it receives from the user is in fact the newest version.
- When the user supplies the account information, the information needs to be decrypted. The merchant knows it has received the data from the user because the user is the only one holding the private key which decrypts the data.

With this verification process, the user may store the account data instead of the merchant and yet the merchant can be sure of the integrity of the data. In fact, one might argue that data integrity is better than when storing the account in the merchant's database. It's more likely that someone breaks into the merchant's database and meddles with the data, than someone hacking the digital signature of the account information. Breaking into the database would most likely result in the merchant's signing key to be exposed though.

## Reality check

There are of course cases when the account information is required outside the typical usage. For example all background processes that operate on the user's information require some data about the user.

Let's approach this through an example. Imagine a typical web based store front. An account for such a site usually contains:

1. Name, nickname, address, phone number, credit card details
2. Settings
3. Order history
4. Items last viewed
5. Preferences (both filled in by the user and analyzed from the her behavior)

A typical use-case for such a site is: a user opens the website, browses the selection and decides to order something. After the order has been processed, the user will want to track it's progress. After receiving the product, the user will come back and give a review of the item.

1.  **Login:** the user's browser automatically downloads the correct account from the third party storage service of choice and provides the data to the store. No action required by the user.
2. **Browsing:** browsing a huge selection of items in the store requires filtering and recommendations. The user's profile contains preference information and information about previous purchases. The store can use this information in addition to anonymized data stored on the server to show the user relevant products.
3. **Ordering:** placing the order requires the store to pass parts of the account information to the payment service it's using. Once the payment has been processed, the information may be stored in the user account information. The merchant needs a copy of transaction identifiers and other metadata, but that may also be stored outside of the store front. This place may be a separate back-end system or it may be part of the payment service they are using.
4. **Sales statistics:** this process happens unbeknownst to the user. After the order has been processed, the store uses the user's preference data and order history to create ranking data. This may happen in-line with the purchase, but most often it will be a background process. The ranking data should of course be anonymized, but determining it requires transient access to the user's account data. This can be performed via a queueing mechanism where the required account data is copied into the analysis request message, but will ultimately vanish after the task is completed.
5. **Shipping:** this is by definition a long running background process where the user of the website is not present. But the store is not participating here either. The parcel service will need to keep a copy of the user's address and contact information, but it's out of the website's scope. And the parcel service works like the queue in the previous example: there is little need to store the user's data much after the package has been delivered.
6. **Tracking:** while the parcel is in transit, the user may use the tracking code provided by the parcel service via the website to track the parcel. Piece of cake, nothing special here.
7. **Reviewing:** the user comes to the website and gives a review of the order purchased. When on the website, the store knows again who the user is and can then supplement the review with account information. The combination of the information is fed into the statistics algorithm which will anonymize the data after which the copy of the user's information is no longer required.

In order for the above to work, the only customer specific account information the store website needs to store, is a number of transaction records and a way to link the review text to the user's username (or whatever else is shown besides reviews). If the user identifier is not a globally known name (email address for example), this data can not be traced back to the user without the account information. Which only the user holds.

The moral of the story: the less background processes a service runs, the less of the user's data the service needs to persist. Background processes may be designed in ways that only parts of the account information are needed for the processing and so the data is stored only for the duration of the background task.

In such a system as the one described above, surprisingly little user data needs to be available at all times! A full break-in to this system would reveal very little of value for the hacker.

## Thoughts?

This article was written as a way to figure out whether this oddball idea could actually work. I'm not fully satisfied that this makes sense to do on a grander scale, but I am truly surprised of how well this idea has stood my preliminary test. Practical implementations would naturally require extensive browser and server support.
