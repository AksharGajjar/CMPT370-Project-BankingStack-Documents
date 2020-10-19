# Due Oct 19th

# Storyboards

Storyboard for Use Case 1.0 - 1.3:
- 1.0 - Check balance in bank
- 1.1 - Check transactions in bank
- 1.2 - Check the balance in PayPal
- 1.3 - Create Financial Plan/Access news articles and financial literacy material

![20201018_195311](uploads/d106884d421ac0b4c526084a17f2f15a/20201018_195311.jpg)

# Domain Models

# System Architecture Details

System Architecture
-Layered architecture style

# Interaction Diagrams

**Sequence Diagrams**

![SequnceDiagramAddBankV1](uploads/07f5297a61d8b8ab7f2eee746140548f/SequnceDiagramAddBankV1.jpg)

![SequnceDiagramCheckBalanceV2](uploads/9ffa80cb9445394e9b19eaba57e8bbb2/SequnceDiagramCheckBalanceV2.jpg)

![SequnceDiagramGetTransactionHistoryV1](uploads/75bacf3c8ea7ab622749b5de44a5a97f/SequnceDiagramGetTransactionHistoryV1.jpg)

![SequnceDiagramMakeAccounteV1](uploads/fd21543f524aec935ef81136c63ff98f/SequnceDiagramMakeAccounteV1.jpg)

![SequnceDiagramNewsV1](uploads/844281b0bab67e340b3b546e28814ed2/SequnceDiagramNewsV1.jpg)


# Persistent Storage Details

Persistent Storage details
-one database one application setup

The persistent storage for the  finance tracker program is based on a hierarchy of encrypted and unencrypted json files. The encrypted files can be broken down into two categories, general encryption and user specific encryption. Files with general encryption contain less sensitive or administrative data and are encrypted/ decrypted using a general key that is known by the application. User specific encryption is for any file containing sensitive user information such as an API access token, this data is encrypted with a user specific key which can only be accessed with the general application key. The structure in the json files is that the "users.json" file which contains all the users and their onetime randomly generated associated directories will be generally encrypted.

In each user's directory are a series of json files containing data specific to that user as well as txt files containing user notes created through the programs provided interface. The json files are, "userCredentials.json", "accountData.json", "userData.json" and "userSubscriptions.json" in addition there is a directory for the txt files called notes. The "userCredentials" is a generally encrypted file containing the users name, password, email, their specific encryption key and any other administrative data that might be needed. After successfully checking the users password the program retrieves the key and uses it for encrypting and decrypting all of the other files contained in the user's directory. Next "accountData" is used to store the information for all of the users associated accounts. This information includes bank name, account id, account owner, API access token and the account type. This data is primarily used with the PLAID and PayPal APIs. The "userSubscription" file simply contains a list of subscriptions and their specific costs, payment intervals, subscription period and start date for use in the programs subscription tracking service. The "userData" file is simply used to keep track of the users selected news filters and point to the location of the txt files containing their notes so that the program can open them for the user to access. The final encrypted json file is "transactionNotes" This file stores an association between a specific transaction and it's pinned note and provides the path to that note so the program can open it for the user and display its association.

The only unencrypted file is the "institutions" json file which simply contains the information on each institution that the plaid API needs in order to set up its tokens, This file will be updated at run time to check if the institutions initially provided for by the program are still supported as well as to check if any of the PLAID connection data has been changed.

**Persistent file storage hierarchy diagram:**

![cmpt370PersistantStorage2](uploads/b014efad12413868038584de0e46591d/cmpt370PersistantStorage2.png)

**JSON file examples:**

users.json:
```json
{
  "users":[
    {
      "username": "Steve105",
      "path": "C:\Programs\fintracker\data\10928324\"
    },
    {
      "username": "tempuser360",
      "path": "C:\Programs\fintracker\data\34937823\"
    },

  ]
}
```

institutions.json:
```json
{
    "institutions": [
        {
            "country_codes": [
                "CA"
            ],
            "has_mfa": true,
            "input_spec": "fixed",
            "institution_id": "ins_39",
            "mfa": [
                "code",
                "list",
                "questions",
                "selections"
            ],
            "mfa_code_type": "numeric",
            "name": "RBC Royal Bank",
            "oauth": false,
            "products": [
                "assets",
                "auth",
                "balance",
                "transactions",
                "income",
                "identity"
            ],
            "routing_numbers": []
        },

    ],
    "request_id": "xxxxxxxxxxxxx"
}
```
userCredentials.json:
```json
{
      "username": "Steve",
      "name": " John Smith",
      "email": "jsmith@mail.com",
      "password": "hellowworld",
      "validation": TRUE,
      "creationDate": "15/10/2020",
      "secretKey": "6EB29Z7",
  }
```

accountData.json:
```json
{
  "accounts": [
  {
    "accountID": 123456,
    "accountOwner": "John Smith",
    "bankName": "name",
    "accountType": "Chequing",
    "accessToken": "TEMP1",
  },
  {
    "accountID": 654321,
    "accountOwner": "John Smith",
    "bankName": "RBC Royal Bank",
    "accountType": "TFSA",
    "accessToken": "TEMP2",
  }
]
}
```

userData.json:
```json
{
  "countryfilter": ["Canada","USA","Germany"],
  "topicfilter":["technology","agriculture"],
  "financialnNotes":["C:/path-to-fnote1","C:/path-to-fnote2","C:/path-to-fnote3"],
}
```

transactionNotes.json:
```json
{
  "transactions: "[
    {
      "accountID": 123456
      "data": [
        {
          "tID": "transaction1"
          "noteFile": "path-to-tnote1"
        },
        {
          "tID": "transaction2"
          "noteFile": "path-to-tnote2"
        },
      ]
    },
  ]
}
```

userSubscriptions.json:
```json
{
  "subscriptions": [
    {
      "company": "tempcompany1",
      "dollarAmount": 15,
      "interval": "Monthly",
      "subscriptionPeriod": 10,
      "startDate": "10/09/2020"
    },

  ]
}
```