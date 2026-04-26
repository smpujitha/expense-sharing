# expense-sharing
the goal of the project is about fair expense sharing amoung group of collage friends 
problem statement:
        In a friends group
# Expense Sharing App

## Overview
The Expense Sharing App is a Python-based application designed to manage and split expenses among friends. It calculates individual balances, determines settlement transactions, and generates expense reports using Pandas DataFrame.

## Features
- Add expenses with multiple participants
- Calculate individual balance sheets
- Determine settlement transactions between friends
- Process refunds
- Generate expense details in DataFrame format
- Track per-person costs and participant counts


### Initialize the App
```python
from expense_sharing import ExpenseSharing

friends = ["balamurugan", "kathiravan", "velmurugan", "Murugan", "karthikeyan", "kumaran"]
expense_sharing = ExpenseSharing(friends)
```

### Add Expenses
```python
expense_sharing.add_expense(
    payer="balamurugan",
    amount=1000,
    description="LUNCH",
    participants=["balamurugan", "kathiravan", "velmurugan"]
)
```

### Calculate Balances
```python
expense_sharing.calculate_balances()
for friend, balance in expense_sharing.balances.items():
    print(f"{friend}: ${balance:.2f}")
```

### Generate Settlement Transactions
```python
transactions = expense_sharing.calculate_settlements()
```

### Process Refunds
```python
refund = expense_sharing.refund(
    payer="balamurugan",
    amount=100,
    description="Extra payment",
    to_person="kathiravan"
)
```

### Generate Expense Report
```python
expense_df = expense_sharing.generate_expense_df()
print(expense_df)
```

## Methodology

### Expense Splitting - Equal Distribution
The application uses **equal splitting methodology** where each expense is divided equally among all participants:

```
Per Person Cost = Total Expense Amount / Number of Participants
```

For each participant in an expense:
- Participant owes: `split_amount` (calculated above)
- Payer receives: `full expense amount`

### Balance Calculation
For each friend in the system:
1. Initialize balance to 0
2. For each expense they paid: ADD the full amount
3. For each expense they participated in: SUBTRACT their share (split_amount)

**Example:**
- Friend pays $1000 for 3 people (including themselves)
- Split per person = $1000 / 3 = $333.33
- Friend's balance += $1000
- Friend's balance -= $333.33
- Net contribution = $666.67

### Settlement Algorithm
1. Categorize all friends into creditors (positive balance) and debtors (negative balance)
2. Sort creditors and debtors by amount in descending order
3. Match debtors with creditors and calculate settlement amounts:
   - Settlement Amount = Min(debtor_amount, creditor_amount)
   - Generate transaction: debtor pays creditor the settlement amount
4. Update remaining balances and repeat until all debts are settled

## Data Structure

### Friend Object
```python
{
    "name": str,
    "email": str,
    "phoneno": str
}
```

### Expense Object
```python
{
    "payer": str,
    "amount": float,
    "description": str,
    "participants": list
}
```

### Balance Dictionary
```python
{
    "friend_name": float  # Positive: owed money, Negative: owes money
}
```

### Transaction Object
```python
{
    "from": str,
    "to": str,
    "amount": float,
    "status": str  # "pending"
}
```

### Refund Object
```python
{
    "from_person": str,
    "to_person": str,
    "amount": float,
    "description": str,
    "status": str,  # "pending"
    "refund_date": pd.Timestamp
}
```

## Data Preprocessing

### Input Validation
- Friend names are stripped of whitespace
- Participant names are stripped of whitespace
- Amount is converted to float
- Participants list contains expense participants

### DataFrame Structure
Generated expense report contains:
- **Payer**: Name of the person who paid
- **Amount**: Total expense amount
- **Description**: Expense description
- **Num_Participants**: Count of participants in the expense
- **Per_Person_Cost**: Amount each participant owes (Amount / Num_Participants)

## Special Cases Handling

### Empty Participants List
If an expense has 0 participants, per-person cost is set to 0:
```python
Per_Person_Cost = 0 if len(participants) == 0 else amount / len(participants)
```

### Refunds
Refunds are tracked separately with:
- Timestamp using `pd.Timestamp.now()`
- Status marked as "pending"
- Both from_person and to_person information

### Settlement Precision
All settlement amounts are formatted to 2 decimal places for currency representation

## Key Methods

### `__init__(friends)`
Initializes the ExpenseSharing object with a list of friend names. Creates expense tracking dictionaries.

### `add_expense(payer, amount, description, participants)`
Adds an expense record and appends it to the payer's expense list.
- **Returns**: Expense dictionary

### `calculate_balances()`
Computes final balance for each friend by summing all paid amounts and subtracting their shares.
- **Updates**: self.balances dictionary
- **Returns**: None

### `calculate_settlements()`
Determines optimal settlement transactions between creditors and debtors.
- **Returns**: List of transaction dictionaries
- **Prints**: Settlement details to console

### `refund(payer, amount, description, to_person)`
Creates a refund record with timestamp.
- **Returns**: Refund dictionary

### `generate_expense_df()`
Converts all expenses into a Pandas DataFrame.
- **Returns**: DataFrame with columns: Payer, Amount, Description, Num_Participants, Per_Person_Cost

## Sample Execution

### Input
```
Friends: balamurugan, kathiravan, velmurugan, Murugan, karthikeyan, kumaran
so my input is about expense among friends when we hang out with frineds we mostly forget to pay or 

Expenses:
- balamurugan pays 1000 for LUNCH (balamurugan, kathiravan, velmurugan)
- kathiravan pays 3500 for PRINTOUT (balamurugan, kathiravan, velmurugan, Murugan)
- velmurugan pays 800 for MOVIE TICKETS (balamurugan, kathiravan, velmurugan, Murugan, karthikeyan, kumaran)
simmilarly goes on 
```

### Output - Balances
```
balamurugan: $333.33
kathiravan: -$1166.67
velmurugan: $266.67
Murugan: -$316.67
karthikeyan: -$133.33
kumaran: -$133.33
```

### Output - Settlement Transactions
```
kathiravan pays balamurugan $333.33
velmurugan pays kathiravan $1166.67
...
```

### Output - DataFrame
```
       Payer  Amount Description  Num_Participants  Per_Person_Cost
0  balamurugan    1000      LUNCH                 3           333.33
1   kathiravan    3500    PRINTOUT                 4           875.00
2   velmurugan     800   MOVIE TICKETS             6           133.33
```

## Challenges and Improvements
##challenges 
the major chanllenge was making the logic run correctly 
and debug issues like
Bugs:Settlement Amount Not Persisting---wrong amount  Tuple Immutability Breaking ,.pop() Removing Critic, Wrong Transaction Data Types
One of the main challenges I faced was debugging logical errors, especially in balance calculation and settlement logic. Small issues like incorrect indentation 
key-value error also occured mainly in user-input phase 
Input validation is basic, so incorrect or unexpected inputs may not always be handled perfectly.
### Current Implementation
- Simple equal split methodology
- In-memory data storage
- Console-based output
- Basic transaction tracking

### Potential Improvements
1.created a dataframe to see all the expenses clearly which is easy to understand
2.created a refund class which handles the refunds ,like missing payments
3.It handles both predefined and user-entered names dynamically.
