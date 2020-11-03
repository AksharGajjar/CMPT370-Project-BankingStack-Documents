# Due Oct 30th
## Quality Assurance Strategies
Technical quality assurance focus will be on largely correctness, reliability, and capability, secondary focus will be on making sure that performance is within the acceptable bounds set in the system requirements. The tertiary focus will be on ensuring that the system has a reasonable degree of maintainability for ease of development.

Tests will start with unit tests on the most basic functions such as createJsonFile or createBankAccount. All of the low-level functions which will be called by higher-level functions will be unit tested to ensure code correctness and capability. Any low-level functions that pass data to one another will then go through integration testing before being implemented together in the higher-level function, That function will then be integration tested to ensure that the data is passed properly.

Avoid nesting functions to increase to better facilitate unit test and integration test, an example being, functions like userJsonCreation should have their data passed to the create jsonFile instead of calling it 

## Testing Outline/Plan
**Test Strategy**

**Test Plan**
- End to End Testing
- Integration Testing
- Unit Testing

**Test Case Design**

**Test Procedures**


## Proof of concept
**Introduction**

To demonstrate our testing methodologies and approach we decided to provide unit testing code for three separate functions that will be part of our system. These are trivial functions and the sole purpose of this is to demonstrate our general approach. 

**Function Description**

The three functions we decided to test were register, encryption, and institutionCheck. 
- The register function essentially collects user credentials, verifies them and stores them into a json file.
- The encryption function takes in data and a key and uses fernet encryption along with the key to encrypt the data.
- The institution function takes in a string query and checks whether the particular institution is available via the plaid API.

**Instructions**

The code for the three functions can be found in the exampleTests branch of the repository. A readme is also included outlining steps required to run the test cases. Running the test cases will generate a log which will include the results of the tests.




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