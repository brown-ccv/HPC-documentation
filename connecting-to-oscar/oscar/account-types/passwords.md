# Passwords

## What username and password should I be using?

* If you are at Brown and have requested a regular CCV account, your Oscar login can be authenticated using your Brown credentials itself, i.e. the same username and password that you use to login to any Brown service such as "canvas". 
* If it is a temporary guest account \(e.g. as part of a class\), you should have been provided with a username of the format "guestxxx" along with a password.
* If you are an external user, you will have to get a sponsored ID at Brown through the department with which you are associated, before requesting an account on Oscar. Once you have the sponsored ID at Brown, you can [request an account](http://pccvwebcit.services.brown.edu/secure/account/) on Oscar and use your Brown username and password to login.

{% hint style="info" %}
We have seen login problems with the Brown credentials for some users so accounts moved to the Red Hat 7 system after September 1st 2018 can also log in to Red Hat 7 with their CCV password.
{% endhint %}

## Changing Passwords

To change your Oscar login password, use the command:

```text
$ passwd
```

You will be asked to enter your old password, then your new password twice.

Password reset rules:

* minimum length: 8 characters
* should have characters from all 4 classes: upper-case letters, lower-case letters, numbers and special characters
* a character cannot appear more than twice in a row
* cannot have more than 3 upper-case, lower-case, or number characters in a row
* at least 3 characters should be different from the previous password
* cannot be the same as username
* should not include any of the words in the user's "full name"

