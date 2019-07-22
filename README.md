# <img src="logo/logo.ico" width="32" height="32"> getpass
 Getpass is open source cross-platform stateless password manager (generator). 
 No internet connection or other type of communication is required.
# platforms
 * [[repo](https://github.com/stellarbear/getpass-spa)] Web service (for quick access): [getpass.io]()
 * [[repo](https://github.com/stellarbear/getpass-extension)] Browser extension: [chrome](), [safari]()
 * [[repo](https://github.com/stellarbear/getpass-mobile)] Mobile version: [android](), [ios]()
 * TBD: Desktop version
# how does it work

**1.** Password is generated based on the following input:

    1 - login  
    2 - website  
    3 - secret keyword  
    4 - app preferences  
    
**2.**   Login, website and app preferences (1, 2, 4) are stored locally (i.e. on your mobile or in browser local storage). We insist that login and website is not a sensitive piece of information and could be obtained easily (most of the time it is your phone number or mail address that are used as login, but you can use whatever you want inside this app, this is just a piece of data that identifies website and login for you).  
**3.**   Input is processed by [scrypt kdf](https://en.wikipedia.org/wiki/Scrypt) with the default parameters set to N = 12, r = 4, p = 1 (this could be easily changed inside app preferences, but you must remain this settings consistent between web / mobile or desktop version of your app in order to generate same passwords)  
**4.**   In order to support password changing for chosen website without changing secret keyword or altering website name, increment counter value  
**5.**   Your app preferences, login and website list could be imported and exported (as a string that is encrypted with [aes](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)  
 
schematic representation:
![](alg/alg.png?raw=true)

# faq
Same information is located at [getpass.io](https://getpass.io/faq)  

**1. What is Getpass?**

Getpass is a stateless cross-platform password manager (generator).  
This tool allows users to generate cryptographically strong passwords based on some input data.  

In a nutshell, Getpass uses a hash-like key derivation function (scrypt), that produces the same output password for the same input which contains **Login**, **Website** and a **Secret Keyword**.  

This function can not be reversed to retrieve input data given the output.  
For advanced users: check out the settings tab for more features.

**2. How does Getpass work?**

Based on users input and some customizable preferences, scrypt key derivation function produces cryptographically strong password.  
Example:  

* Login: **andromeda**    
* Website: **milkyway.com**    
* Secret Keyword: **2,52m light years away**   
      
Produces password: **3q_q(MFWaMGeao+[CX**
 
 **3. Generation options**
 
 Mostly you **do not need** to configure them and may use default values. (you may find each option explanation in the *What are the advanced settings section*)  
* Password alphabet: numbers, A-Z, a-z, symbols  
* Password length: 18  
* Counter: 0  
* Scrypt parameters: N: 4096, r: 4, p: 1  

Note: for desktop or mobile, or web extension version all preferences can be exported / imported (with your logins and websites) when you decide to transfer your data from one device to another, so there is no need to do the same job, adding same information.
    
**4. What is a Login?**

Login is something that identifies user's account on a specific website.  
It can be user's real login for this website or mail, mobile phone number or anything else.  

For most cases we recommend using real logins for this field as Getpass was designed in a way to generate secure passwords even if Login and Website fields are public.    
Note: “andromeda” and “Andromeda” are different login values (i.e. case sensitive)

 **5. What is a Website?**
 
Website is the name of the website/service user wants to generate password for.  
It can be a real website name (e.g. milkyway.com).  

For most cases we recommend using real website names for the same reasons as mentioned in Login section.  
Note: “milkyway.com”, “milkyway”, “milkyway com” are different website values
    
**6. What is a Secret Keyword?**

Secret Keyword is a keyword we use to generate cryptographically strong passwords. Think of it as a master password you use to get all the other passwords you need. It can be (and actually, we insist that it must be) any combination of letters, numbers and symbols.  

Note: there is no way to retrieve you Secret Keyword even if you know the login, website and the generated password. This is the most important piece of information and as it’s title says, you must keep it as private as possible
    
**7. What are the advanced settings?**

* Password length and alphabet. Binds to website. Sometimes there are some restrictions when we speak about generating passwords for specific services. We give users an ability not only to change default password generation preferences, but also (on local versions only) we store this data locally so there is no need to set them each time you need a to generate a password and thus, no need to remember them.  
* Counter. Binds to website. Some service policies require you to change your password once a month, a year and so on. As we've said earlier at Getpass the same input produces the same output. So we implemented a counter variable. Just increase it when you need to change your password without altering website name or changing the secret keyword. This is stored locally like options above.  
* Scrypt parameters. Binds to entire application (i.e. affects everything). Well, you must know what you are doing if you decided to change them. Changing them may not only increase or decrease a complexity, but directly affect password generation time. You must also remember that it takes more time for mobile devices to perform these computations.  
You can read about scrypt parameters on [wikipedia](https://en.wikipedia.org/wiki/Scrypt).  

Note: all of these options can be exported / imported (with your logins and websites) when you decided to migrate your data from one device to another, so there is no need to add them on more than one device.
    
**8. What is this image for, that changes when I enter my Secret Keyword?**

Did you notice that secret keyword is obscured? If yes, than this is a way to visually represent a hash of your Secret Keyword, based on jdenticon library. This is the way to ensure that your Secret Keyword is typed correctly, without revealing the actual letters you have typed.
    
**9. A note about security**

First of all, Getpass (every platform or service implementation) doesn’t use ANY of your data. Not a single POST request to the hosting or arbitrary server is done. No internet required at all to work with our product. All of the computations are done on  client devices, such as desktop, mobile or web browser (both, extension and getpass.io website). The source code for every platform is available (links in the download section).  

Secondly, there is a small difference between how the local version (mobile, desktop, browser extension) and service version (website getpass.io) treat your data:  
* Service version doesn't store anything at all, but at the same time it doesn't provide some of the local version features. Main use case for the service version: one-time password generation or when you do not have access to any of your local app version.  
* Local version stores locally login and website list (and all the preferences). We insist that login and website are not sensitive pieces of information and could be obtained easily (most of the time it is your phone number or mail address that are used as login, but you can use whatever you want inside this app). The reason that we store this is to give our users better experience when they need to generate a password – just 4 single taps to select login and website. This convenience does not reduce users safety, because, we give users the ability to obscure these values and / or you may use your own way to alias these pieces of data (for example, you may use “git repos” instead of “github” or “google mail” instead of ”gmail”)  

Secret keyword is **never** stored anywhere. That is a crucial piece of information and as it’s title says, you must keep it as private as possible  

Note every input IS case sensitive! Changing a letter in website or login or secret keyword leads to totally different password.
    
**10. General security advice**    

There are some more and less important services where you want to authenticate from the data safety perspective. No one restricts you from using different secret keywords for different websites (but you must remember which one binds to which one).  

For example, for everyday not important service usage, you may use simple secret keyword, for example: “.NETdev2019”, but for others, maybe your bank account, you could use something more complex like “WhatAGre@t8267TimeToBeA%Developer%!”  
In a nutshell, Getpass uses a hash-like key derivation function (scrypt), that produces the same output password for the same input which contains **Login**, **Website** and a **Secret Keyword**.
    
**11. What are the advantages and disadvantages of using Getpass?**    

Advantages:  
* App generates different cryptographically strong passwords for every account you want to protect  
* You don’t have to remember anything but your secret keyword  
* Getpass service is available 24/7 on every device at getpass.io  
* None of your data is transferred anywhere (not a single POST request to third party servers is send). You secret keyword is not stored (even locally)  
* You don’t have to trust some proprietary software to protect your critical data (you can examine our source codes and help us to improve Getpass as well)  

Disadvantages:  
* It takes some time to change your old passwords to Getpass ones (this is every password manager issue, to be honest)  
* Speaking of local policies when you are forced to change your password in some period of time, we can't say that counter solution is an elegant way to do this, but we think that this is the least inconvenient way to implement this functionality
    
# technology stack
 * [React + ts](https://reactjs.org/) for web service
 * [Vue + js](https://vuejs.org/) for browser extension
 * [Flutter + dart](https://flutter.dev/) for mobile version
 * [Avalonia (WPF)](http://avaloniaui.net/) for desktop version (planning)
 
 Additional libraries:
 * [jdenticon](https://jdenticon.com/)
 
 # license
 This project is licensed under the terms of the GNU GPLv3.
