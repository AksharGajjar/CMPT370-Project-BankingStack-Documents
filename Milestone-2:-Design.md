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

The persistent storage for the  finance tracker program is based on a hierarchy of encrypted and unencrypted json files. The encrypted files can be broken down into two categories, general encryption and user specific encryption. Files with general encryption contain less sensitive or administrative data and are encrypted/ decrypted using a general key that is known by the application. User specific encryption is for any file containing sensitive user information such as an API access token, this data is encrypted with a user specific key which can only be accessed with the general application key. The structure in the json files is that the "users.json" file which contains all the users and their specific keys and their associated directories will be generally encrypted. Once this data has been retireved

Persistent file storage hierarchy diagram:
![cmpt370PersistantStorage2](uploads/b014efad12413868038584de0e46591d/cmpt370PersistantStorage2.png)

Below are some examples of what the JSON files used to store the persistent data will look like.

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