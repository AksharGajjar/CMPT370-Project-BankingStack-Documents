# Due Oct 19th

# Storyboards

Storyboard for Use Case 1.0 - 1.3:
- 1.0 - Check balance in bank
- 1.1 - Check transactions in bank
- 1.2 - Check the balance in PayPal
- 1.3 - Create Financial Plan/Access news articles and financial literacy material

![20201017_163748](uploads/afd4a43d511e2b36865b84cf19f2a9ac/20201017_163748.jpg)

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

Below are some examples of what the JSON files used to store the persistent data will look like:
;;;
{
  "users":[
    {
      "username": "Steve105",
      "path": "C:\Programs\bankecon\data\10928324\"
    },
    {
      "username": "tempuser360",
      "path": "C:\Programs\bankecon\data\34937823\"
    },
    {
      "username": "Carl55",
      "path": "C:\Programs\bankecon\data\95936728\"
    }
  ]
}
;;;

