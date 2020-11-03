# Due Oct 30th
## Quality Assurance Strategies
Technical quality assurance focus will be on largely correctness, reliability, and capability, secondary focus will be on making sure that performance is within the acceptable bounds set in the system requirements. The tertiary focus will be on ensuring that the system has a reasonable degree of maintainability for ease of development.

Tests will start with unit tests on the most basic functions such as createJsonFile or createBankAccount. All of the low-level functions which will be called by higher-level functions will be unit tested to ensure code correctness and capability. Any low-level functions that pass data to one another will then go through integration testing before being implemented together in the higher-level function, That function will then be integration tested to ensure that the data is passed properly.

Avoid nesting functions to increase to better facilitate unit test and integration test, an example being, functions like userJsonCreation should have their data passed to the create jsonFile instead of calling it 

## Testing Outline/Plan
**Test Strategy**

Our testing strategy closely resembles the layered architecture approach which we chose for designing the system. Essentially, there are three main layers to our system, and each function is categorized based on these levels. The top-level roughly includes functions like register, login, GUI interfaces, add/remove account credentials, subscriptions, add/remove notes, creating user JSON files, and news filter functions. All of these functions don't directly connect to the APIs and do connect with the GUI so these are considered top-level functions. Similarly, there are mid-level and low-level functions that do communicate with APIs and do handle much of the back-end functionalities. 

*Build the test cases first*

One of the key aspects of our strategy is that we plan on building all of our test cases before we start coding the system. This will ensure that we don't get feature creep in our development cycle as we will know exactly what we need to build to make sure our test cases pass.

*Skeleton structures*

While the top layer functions are being tested, one important factor to consider is the fact that these functions depend on the lid level functions, and to address this issue we will be using mid-level skeleton functions that will connect to top-level functions and mimic some behavior to ensure that the top-level functions can be tested appropriately. We will also use mocks to test certain functions to ensure faster testing and to ensure that our API call traffic is minimized.

*Testing Tools*

- pytest
- pytest-mock 

**Test Plan**

NOTE: This document for Milestone 3 only consists of testing that relates to the minimum viable product (MVP). In other words, most of the test cases presented here are only relating to the must-have features. It's extremely difficult to outline a completely accurate test plan since there will be changes that might occur when building the project. Our main goal here is to showcase a thorough understanding of testing principles and to showcase that a concrete plan has been put in place to execute successful testing. There might be some test cases missing and there might be some functions that get added or removed during the building process. The newly added functions will be tested using the testing methodologies outlined in this document.

*Testing Environment*

Our testing environment will be pytest and pytest-mock. We are using python for our programming language and we found that the pytest fits our needs the best and also many group members are already familiar with the pytest functionality.

*Testing Order*

The order of testing will be based on the implementation process. Because we will be following a top-down approach the unit tests for the top-level functions will be the first to be implemented followed by integration tests for top-level functions such as subscription functions. Lastly, we will test the end-to-end functions. 

*End to End Testing*

Our system will mostly consist of unit tests and integration tests. There will be very few end-to-end tests that will essentially test the key user flows that a typical user will take in our system. The end-to-end tests will run through several components of our system to achieve some end goal. Some examples of end-to-end tests that our system will contain are:

- Flow #1: Register, log in, connect a bank account, view transactions, add a note to a transaction.
- Flow #2: Log in, open bank account, view account balance, view overdraft limit.
- Flow #3: Log in, access subscriptions, add a subscription, edit a subscription, delete a subscription
- Flow #4: Log in, access financial plan, add a new note to a financial plan, edit an existing note, delete a note, and edit news filters.

*Integration Testing*

Similarly, the Integration tests will consist of testing subsystems. Our integration test will be classified based on the functionalities of the functions. For instance functions such as createClient(), getBalance(), getTransactions(), getInstitutions(), getAccesstoken(), and getLinkToken() all relate to the plaid API and so these functions will be grouped together in the following manner:

- Integration Test #1: API auxiliary functions testing. createClient(), getLinkToken() and getInstitutions() will be tested in conjunction since getLinkToken and getInstitutions will utilize the createClient function from the Plain API python library.
- Integration Test #2: Account Testing. addAccount(), getBalance(), getTransactions(), and getAccessToken() will be tested in conjunction because the access token obtained form API will be required for both getBalance(), and getTransactions().
- Integration Test #3: User login and register testing. login(), register(), and createUserJson() will be tested together since all three depend on each other. 
- Integration Test #4: Subscriptions testing. createSubscription(), editSubscription(), deleteSubscription().
- Integration Test #5: Financial plan testing. createNote(), editNote(), deleteNote(), addNewFilter(), editNewsFilters().

*Unit Testing*

For unit testing, our plan is to essentially test each and every function in our system. The sample test cases we have provided in the repository are unit tests and will give you some indication as to how we plan on doing our unit tests. One important thing to keep in mind is that the example tests don't use any mocks or any harnesses because they are just a sample. Our actual test cases will be much more in-depth and will have more in-depth testing. Here are some examples of unit tests.

- unit test #1: register() (key feature)
- unit test #2: login() (key feature)
- unit test #3: userJsonCreation (storage system testing. Test to see if a file is created properly by checking the categories stored in the file.)
- unit test #4: addAccount() (key feature. Works by checking Plaid API JSON response)
- unit test #5: removeAccount()
- unit test #6: accountJsonCreation (storage system testing. Verifies proper account information is stored)
- unit test #7: getTransaction() (key feature, Test by verifying the json response from API)
- unit test #8: getBalance() (key feature, Test by verifying the json response from API)
- unit test #9: addNewsFilters() (key feature, test by checking news API response and verifying the filters are yielding valid responses)
- unit test #10: createNote() (key feature)

**Test Case Design**

In this section, we will discuss specifics regarding how specific implementations will be tested. We will discuss both positive and negative testing for test cases where it's applicable. 

| Test Case ID | Test Type | Test Scenario | Test Steps | Test Data | Expected Results |
| ------ | ------ | ------ | ------ | ------ | ------ |
| E2E#1 | End-to-End | Registering to viewing transactions | Register user by providing necessary credentials, log in with those credentials, go to accounts page, add a new account, provide account details, once the account is connected to, view transactions, add a note to a specific transaction. | username, name, password, email, bank account id and password, access_token   | User can successfully register, login, add an account, and attach a note to a transaction. Also, proper exceptions and errors are thrown when the negative inputs for each specified variable are inputted. |
| E2E#2 | End-to-End | Login to viewing balance | login with user credentials, go to accounts page, add a new account, provide account details, once the account is connected to, view balance and overdraft limit | username, password, bank account id and password, access_token | User can successfully log in, add account and view account balance and overdraft limit. Also, proper exceptions and errors are thrown when the negative inputs for each specified variable are inputted. |
| E2E#3 | End-to-End | Login to managing subscriptions | login with user credentials, go to the subscriptions page, add a subscription by providing payment frequency, start date, subscription amount, edit an existing subscription, delete a subscription | username, password, subscription amount, start date, payment frequency | User can successfully log in, add subscription, edit and delete subscriptions. Also, proper exceptions and errors are thrown when the negative inputs for each specified variable are inputted. |
| E2E#4 | End-to-End | Login to managing financial plan | login with user credentials, go to the financial plans page, add a new note by providing title and note body, edit an existing note, delete a note, add a new news filter, and edit the existing filters | username, password, note content, note title, news filter options  | User can successfully log in, add a new note, edit and delete existing notes, add news filters from a selection, and edit existing filters. Also, proper exceptions and errors are thrown when the negative inputs for each specified variable are inputted. |
| IT#1 | Integration Test | Plaid API auxiliary function testing | create a client using createClient() and by providing client_id and secret. Then once the client is created, utilize the client to obtains a link token by providing the necessary config variables. Next use the client once again to query the institutions and verify that the four Canadian institutes that our program should support are available | client_id, secret, environment, config variables such as products, country_name, country_codes, language, and account_filters. institutions require query string that will be used to query for institutes | Successful if able to create a client and successfully obtain link token and verify institution support while successfully handling erroneous inputs by throwing the correct exceptions |
| IT#2 | Integration Test | Plaid API Account Testing | Able to obtain an access_token and connect a bank account and obtain bank transactions and account balance along with overdraft limit. Once an access_token is obtained use that to obtain transactions and balance. To obtain transactions and balance you will need to provide start date and end date to specify range of transactions.  | access_token, client_id, secret, start_date, end_date | Successful if able to obtains an access_token corresponding to a bank account and successfully obtain transactions within specified range along with balance and overdraft limit. Also able to successfully handle exceptions and errors caused by faulty inputs.|
| IT#3   | Integration Test | User login and register testing  | Pass the user data to the Register function, register will create the user json which will be passed to a create user file function then call the login function with the login information.  Once a successful login occurs display the system homepage. | username, password, email, name, user_id  | On a successful test login will return the user_id which will be used to access that user's data profile. It will also be successful if it successfully handles faulty inputs accordingly.  |
| IT#4   | Integration Test | Subscriptions testing | Call the addSubscription function, then pass the data json data to the fileCreation function. Once the subscription is created edit the subscription to ensure the stored data is modified and then delete the subscription to ensure proper deletion occurs. | subscription amount, start date, payment frequency, company, list of subscriptions | addSubscription function should return a subscription json and pass it to the create subscription json function. Once that's done the edit and delete should do their corresponding jobs and as long all of the functions are working and handling errors successfully then the test case will pass. |
| IT#5   | Integration Test | Financial plan testing  | access the create note function and successfully create a note using note title and content and date, next step is to edit that particular note and once that is done lastly delete the note. After this add a new news filter from the available options and once the news feed updates edit the news filters and also delete a filter.| note content, note title, news filter options | If create a note passes a json to the create note file and successfully stores the note, if edit and delete note does their respective functionality and also if the add/editing/deleting of news filter is successful then this test case will be considered successful.|
| UT#1 | Unit Test | register() | This function takes in username, email, name, and password. It then uses that to create a user profile json which is sent to a createUserFile() function which stores the json in a file | username, email, name, and password | Successful if it is able to handle all possible invalid inputs safely and if valid inputs are provided it creates a json object |
| UT#2 | Unit Test | login() | The login function takes in username and password and once the login button is clicked the function will login user and in the back end the function will provide the user_id which will be used by other functions to access that users data | username, password | Successful if it shows proper errors messages when invalid inputs are entered. And if valid inputs are entered it provides the correct user_id |
| UT#3 | Unit Test | userJsonCreation() |
| UT#4 | Unit Test | addAccount() |
| UT#5 | Unit Test | removeAccount() |
| UT#7 | Unit Test | getTransaction() |
| UT#8 | Unit Test | getBalance() |
| UT#9 | Unit Test | addNewsFilters() |


**Test Procedures**

Since we will mainly be using pytest and pytest-mock as our testing tools. We decided against using any hooks or any other harnesses because the scope of our project not being too large. We believe the time spent configuring commit hooks and harnesses would be better utilized in testing and building the system. In order to ensure that the code being pushed onto the repo is safe, we have instead devised a custom harness that we will all utilize. We have decided that before a group member wishes to push code onto the repo they must run all unit tests and if the member wishes they can also run the integration tests related to their subsystem. They must append the resulting log along with their merge request. This log and the code being merged will then be verified by at least two other members before it is approved for the merge. The reason behind doing this decision is because not having commit hooks gives us some flexibility. 

## Proof of concept
**Introduction**

To demonstrate our testing methodologies and approach we decided to provide unit testing code for three separate functions that will be part of our system. These are trivial functions and the sole purpose of this is to demonstrate our general approach. 

**Function Description**

The three functions we decided to test were register, encryption, and institutionCheck. 
- The register function essentially collects user credentials, verifies them and stores them into a json file.
- The encryption function takes in data and a key and uses fernet encryption along with the key to encrypt the data.
- The institution function takes in a string query and checks whether the particular institution is available via the plaid API.

**Instructions**

The code for the three functions can be found in the exampleTests branch of the repository. A readme is also included outlining steps required to run the test cases. Running the test cases will generate a log that will include the results of the tests.




## Code Convention
**Language**

Our group has all agreed on using Python 3.8.5 to work on this project. 

**Docstring**

Our group will be following PEP 257 for docstrings throughout the whole project. The reason why we pick PEP 257 is because most of us are familiar with this docstring convention, so it is easier for us to follow and understand as well. As for the format, we will be following google format.

Here is some example for the google format : 

    """
    This is an example of Google style.

    Arguments:
        param1: This is the first param.
        param2: This is a second param.

    Returns:
        This is a description of what is returned.

    Raises:
        KeyError: Raises an exception.

    """

**Comments**

- Group members can add comments if they think that part is too complex or abstract.
- Limit the length of the comment line to 80 characters, after 80 words programmers have to continue in the newline.
- Start with # and leave white space in between the # and the starting character.

    **1.Above line Comments**

    - Above line comments is better for explaining a single line of code.
    - Comment line have to be above the line of code.

    Example: 

        # sum the param with 5
        new_param = param + 5


    **2.Block Comments**

    - When docstring is not used in that function, block comments will be used.
    - Leave a blank comment line in between two comments, making comments easier to read.
    - Block comments are better to use to explain a section of code. They help to let others understand that certain parts of the 
      function.

    Example:
    
        Def squareRoot(param):
            # Calculating the square root of the given param without using
            # any built-in function
            #
            # a print out will be called and print out the solution
 
            param = param**(1/2)
            print(param)

**Naming**

- Function name will be separate via capitalization, e.g. sampleFunction().
- Variable name will be separated via underscore without any capitalization, e.g. sample_variable.

**If-else statement Formatting**

- No more than or equal 5 logical symbols inside the if-else statement, if so switch to nested loop.

**Constant**

- Use uppercase for the whole variable name, and will use the underscore to do the separation.

Example:

    Single-word variable name. (CONSTANT)
    Variable with more than one word. (SOME_CONSTANT)

**Bracket Format**

- There will be a single whitespace between the parameters or variables.

Example:

    #example 1
    Def sampleFunction(param1, param2, param3, param4):
        …

    #example 2
    sample_list = [1, 2, 3, 4, 5,]

**Space and Tab**

- Space will be used to create whitespace most of the time.
- Only use Tab to create the whitespace for the function gap.
- Four spaces will be used for indentation.

Example:

    Def sampleFunction(param1, param2, param3, param4):
        # single whitespace between the symbols and parameters.
        # Tab was used to create the whitespace in front of sum_result.
        sum_result = param1 + param2 + param3 + param4 