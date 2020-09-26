# Due Oct 2nd

## Product Description

Our product is a personal finance application that allows users to securely access several bank accounts and PayPal all in one place. After creating an account with our platform, users can link their bank accounts and their PayPal account. The users will also be given an option to auto-login in which case the login info to their financial institutions will be securely stored for easy login so they never have to worry about separately logging into their respective financial institutions ever again.

Once connected with a bank account users will be able to filter and view their transaction data going back 12 months. In addition to this, the system will also provide users an easy way to keep track of available funds to help users avoid overdraft fees. In addition to bank accounts, users can also keep track of their PayPal account. Our current plan is to provide users with a centralized hub to track all of their finances. In the future, we plan on implementing functionality to allow users to pay bills, and transfer funds between accounts through our service.

In addition to the ability to check account balance and up to 12 months of transaction data, our application also allows users to create a custom financial plan. Users can use this feature to create monthly/yearly budgets and keep track of their long term or short term financial goals. Future plans include providing users with financial education resources and news. To help users come up with a solid plan the notes section will offer financial information from reputable financial educational websites such as Investopedia. Users will also have access to a customizable news feed where they read the latest articles on topics such as personal finance, real estate, business, and investing.

Since financial management includes more than just bank accounts and money we also have plans in place to implement a stock portfolio tracker and a tracker for other assets such as gold, real estate, and crypto. This is a fairly long term goal which might be incorporated if the aforementioned features are successfully implemented. 

Our target audience for this product is the general public. More specifically we believe we can really help young people manage their finances in a meaningful way. Financial literacy is an essential skill and our application aims to help you lead a more financially conscious life. This tool can also be very helpful for the elderly as it allows users to combine all their bank accounts in one place. This quality of life improvement is especially beneficial for the elderly because they are most likely to have more than one bank account. Once we add our stock portfolio and assets tracker, our application would also be a great tool for new and veteran investors. The ability to manage finances, stock investments, and other assets all in one place is extremely powerful and can be utilized by everyone.

In order to achieve all of the aforementioned functionalities, we will be using several different technologies in conjunction. Our application will be programmed using python. One of the main features of connecting bank accounts to our platform will be facilitated by the Plaid API. Plaid API allows us to securely connect to several Canadian Financial institutions. Additionally, to implement the financial planner we will use NEWS API to get meaningful news articles to display to the user. To implement the stock portfolio and assets tracker, we will make use of APIs such as IEX Cloud and WealthSimple API. IEX cloud provides real-time stock market data and quotes for stocks along with a plethora of other useful information. Wealthsimple API would be utilized to connect to the user WealthSimple trade account so they can view their stock portfolio through our application. Along with all of this, we will use several other python libraries to help us build the system. For instance, we will utilize TKinter to develop the GUI for our application.


## List of Requirements

**Must Have Features**

- Login and Account Creation capabilities.
- Ability to connect to the top 4 Canadian banks (RBC, Scotia, TD, CIBC).
- Ability to check account balance.
- Encryption to store and manage sensitive user credentials.
- Ability to view the last 12 months of transaction activity for connected accounts.
- Ability to connect to and manage PayPal account.
- User should only have to log in to each of their bank accounts once using the application
- Transaction and balance data should update when the user logs in and allow on-demand refreshes afterward
- APIs should be obfuscated from user
- 

**Should Have Features**

- Alert the user if overdraft has occurred
- Ability to track all user subscriptions.
- A notes area to save and manage ideas, finance goals, and personal finance strategies.
- Users can attach notes to transactions
- Should provide a workspace for users to plan out financial strategies

**Could Have Features**

- Stock Portfolio manager.
- Ability to track additional assets such as gold, real estate, vehicle(s), Crypto, etc.
- Ability to pay bills and transfer money.
- Add messaging functionality between users that share bank accounts.
- Displays user-customized news feed

## List of Actors, Scenarios, and Use Cases

**primary actors:**
- online-user
- system 
- bank
- PayPal

**precondition:** 
- The network connection is active.
- Bank account to connect.

**use case:** 

online-user:
- log in.
- connect to their bank account.
- connect to their PayPal account.
system:
- send a validation request
- gather information from either 
- shows linked bank account balance.
- shows linked PayPal account balance.
- encrypt the user's information.
- keep the information updated every 5 minutes.
-
 
bank:
- receiving a validation request from the application.
- check validation from the user.
- allowing users to link and access their bank account. 
- send information to the application 

Paypal:
- receiving a validation request from our application.
- check validation from the user.
- allowing users to link and access their PayPal. 
- send the user's PayPal information to the application.

**The basic flow of event:**
- user create an account 
- user logs in to their account to the application.
- connecting their bank account or PayPal account to the application.
- application will send validation to the bank/PayPal and verify the user.
- The user gets validated.
- system will get the information from the bank/Paypal.
- system will show the balance of the user's bank/PayPal account.

## UML Standard Diagrams
