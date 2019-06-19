# getpass
 Getpass is open source cross-platform stateless password manager (generator). 
 No internet connection or other type of communication is required.
# platforms
 * [[repo](https://github.com/stellarbear/getpass-spa)] Web service (for quick access): [getpass.io]()
 * [[repo](https://github.com/stellarbear/getpass-extension)] Browser extension: [chrome](), [safari]()
 * [[repo](https://github.com/stellarbear/getpass-mobile)] Mobile version: [android](), [ios]()
 * TBD: Desktop version
# how does it work
 * Password is generated based on the following input: 1 - login, 2 - website, 3 - secret keyword, 4 - app preferences. 
 * 1, 2, 4 are stored locally (i.e. on your mobile or in browser local storage). We insist that login and website is not sensitive piece of information and could be obtained easily (most of the time it is your phone number or mail address that are used as login, but you can use whatever you want inside this app). 
 * Input is processed by [scrypt kdf](https://en.wikipedia.org/wiki/Scrypt) with the default parameters set to N = 12, r = 4, p = 1 (this could be easily changed inside app preferences, but you must remain this settings consistent between web / mobile or desktop version of your app in order to generate same passwords)
 * In order to support password changing for chosen website without changing secret keyword or altering website name, increment counter value
 * Your app preferences could be imported and exported (as a string that is encrypted with [aes](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)
 
schematic representation:
(alg.png)
# technology stack
 * [React + ts](https://reactjs.org/) for web service
 * [Vue + js](https://vuejs.org/) for browser extension
 * [Flutter + dart](https://flutter.dev/) for mobile version
 * [Avalonia (WPF)](http://avaloniaui.net/) for desktop version (planning)
 
 Additional libraries:
 * [jdenticon](https://jdenticon.com/)
 
 # license
 This project is licensed under the terms of the GNU GPLv3.
