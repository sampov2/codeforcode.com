---
title: "Password age is the new strength"
date: "2014-05-05"
background: "/images/the_old_padlock____by_anggiehutagalung-d4gcl1r.jpg"
layout: post
---

Lance James wrote an [interesting piece](https://securityledger.com/2014/05/is-pavlovian-password-management-the-answer/) on how to train users to use better passwords. His idea of setting password expiration based on the complexity of the password is a very good one. This not only educates users but also negates the need for organizations to have a single static password policy. Password policies tend to be problematic, since others like to litter their passwords with special characters (!#?) while others prefer using longer, but [more easily remembered](http://xkcd.com/936/) passwords. It's difficult to create sane policy which covers all cases.

![Image by&nbsp;AnggieHutagalung](https://images.squarespace-cdn.com/content/v1/52375b95e4b030ffaec4c1f9/1399280149933-KUJPGVZW8Q8741B27N7S/Image+by+AnggieHutagalung){: width="100%" }
Source: [image](http://anggiehutagalung.deviantart.com/art/The-Old-Padlock-269325711) by [AnggieHutagalung](http://anggiehutagalung.deviantart.com/)

I would however argue that for pavlovian training to happen, the users need instant feedback based on their actions. If the user is not warned beforehand about the consequences of their new password's quality, they will only get frustrated if they're required the change the password after just a few days. As they should.

How about we just switch strength indicators to expiry indicators?

![The user has entered a short, simple password.](/images/simple-short-password.png){: width="100%" }
The user has entered a short, simple password.


![A more complex, more difficult to hack password has been entered.](/images/not-so-simple-password.png){: width="100%" }
A more complex, more difficult to hack password has been entered.

So instead of telling the user they chose a bad password _after_ they've changed it, we could give them direct feedback to how long they can use the new password for. This gives the user the chance to optimize their behavior between easy-to-remember vs difficult and fast expiry vs stable. We would no longer need to train the user: this mechanism would make the effect of password complexity immediately clear to the user.

 “... we don’t really provide an incentive or an understanding of why we tell them to do this”
— Lance James

The above quote on how developers fail to teach the users hits the nail on the head. The failure of most password policies is that they've been opaque and people have wanted to pass that hurdle with as little effort as possible. Switching away from static policies and abstract strength indicators to tangible variables in a language the user can understand should push us to the right direction.
