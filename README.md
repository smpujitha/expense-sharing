

## 📌 Project Overview

The Expense Sharing Application is a Python-based project designed to simplify the process of **splitting shared expenses among friends or groups**.

When multiple people share expenses such as food, travel, shopping, or other activities, manually calculating who owes money to whom can become confusing.

This project provides a simple solution where users can:

- Add friends to a group
- Record expenses
- Specify who paid for each expense
- Specify the participants involved in each expense
- Calculate the cost per person
- Calculate the net balance of every participant
- Identify who should pay and who should receive money
- Generate payment settlement transactions
- Display expense details in a Pandas DataFrame

The application is implemented using **Python, Object-Oriented Programming (OOP), dictionaries, lists, and Pandas**. :contentReference[oaicite:1]{index=1}

---

# Project Objectives

The main objectives of this project are:

1. Simplify expense sharing among groups of people.
2. Record individual expenses and their participants.
3. Calculate each participant's share of an expense.
4. Maintain the history of expenses.
5. Calculate the net balance for every participant.
6. Identify people who need to pay or receive money.
7. Generate simplified settlement transactions.
8. Present expense information in a structured DataFrame.
9. Reduce manual calculations and settlement confusion.
10. Provide a foundation for a simple expense-management application.

---

#  Problem Statement

When friends or groups share expenses, different people may pay for different activities.

For example:

- One person pays for lunch.
- Another person pays for dinner.
- Someone else pays for snacks.
- All three people participate in these expenses.

Manually calculating the total amount each person owes can become difficult, especially when there are many expenses and participants.

### Problem:

> **To develop an expense-sharing system that records group expenses, calculates each participant's share, determines the net balance, and generates simplified payment settlement transactions.**

The system aims to answer:

- Who paid for an expense?
- How much was paid?
- Who participated in the expense?
- How much does each participant owe?
- Who should receive money?
- Who should pay money?
- What transactions are required to settle the expenses?

---

# Approach / Methodology

The project follows the workflow below:

```text
Enter Friends
      ↓
Create Expense Sharing Object
      ↓
Add Expense
      ↓
Store Payer & Participants
      ↓
Calculate Per-Person Cost
      ↓
Calculate Net Balances
      ↓
Separate Debtors & Creditors
      ↓
Generate Settlement Transactions
      ↓
Display Expense DataFrame
      ↓
Final Payment Settlement
````

---

#  Object-Oriented Approach

The application uses a Python class called:

```python
ExpenseSharing
```

The class manages the friends, expenses, balances, and settlement calculations.

The constructor initializes the friends and expense records. Each friend is stored with fields such as:

* Name
* Email
* Phone number

The application also creates an expense dictionary for each friend. 

---

#  Adding Friends

Users can enter multiple friend names separated by commas.

Example:

```text
Enter the names of friends (comma-separated):
amu,rina,ram
```

The names are processed and stored as members of the expense-sharing group. 

---

#  Adding Expenses

The application allows users to enter:

* Payer
* Amount
* Description
* Participants

Example:

```text
Payer: amu
Amount: 2000
Description: lunch
Participants: amu,rina,ram
```

The expense is stored with the payer, amount, description, and participants. 

---

#  Expense Splitting

The application calculates the expense share based on the number of participants.

The formula used is:

```text
Per Person Cost = Total Expense / Number of Participants
```

For example:

```text
Lunch = ₹2000
Participants = 3

₹2000 / 3 = ₹666.67 per person
```

The project handles the case where there are no participants by assigning a split amount of zero. 

---

#  Expense DataFrame

The application converts the stored expense information into a Pandas DataFrame.

The generated DataFrame contains:

| Column             | Description                       |
| ------------------ | --------------------------------- |
| `Payer`            | Person who paid                   |
| `Amount`           | Total amount paid                 |
| `Description`      | Description of the expense        |
| `Num_Participants` | Number of participants            |
| `Per_Person_Cost`  | Cost assigned to each participant |

This provides a structured view of all recorded expenses. 

---

#  Net Balance Calculation

The application calculates the net balance for every friend.

For each expense:

1. The expense is divided among the participants.
2. Each participant's share is deducted from their balance.
3. The person who paid receives credit for the full amount paid.

The resulting balance determines whether a person should:

* Receive money
* Pay money
* Has already settled

The application displays results such as:

```text
amu should receive ₹833.33
rina should pay ₹166.67
ram should pay ₹666.67
```



---

#  Payment Settlement

After calculating the balances, the application separates participants into:

### Creditors

People with a positive balance who should receive money.

### Debtors

People with a negative balance who need to pay money.

The application then matches debtors with creditors and calculates the settlement amount using the smaller of the outstanding amounts. 

Example:

```text
rina pays amu ₹166.67
ram pays amu ₹666.67
```

This provides a simplified set of transactions required to settle the group's expenses. 

---

# Application Workflow

```text
                 ┌─────────────────────┐
                 │   Enter Friends     │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │    Add Expenses     │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ Split Each Expense  │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ Calculate Balances  │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ Find Debtors &      │
                 │ Creditors           │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ Generate Settlement │
                 │ Transactions        │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ Display Final       │
                 │ Expense Details     │
                 └─────────────────────┘
```

---

#  Sample Execution

Example group:

```text
amu
rina
ram
```

Expenses:

| Payer | Amount | Description | Participants |
| ----- | -----: | ----------- | -----------: |
| amu   |  ₹2000 | Lunch       |            3 |
| rina  |  ₹1000 | Dinner      |            3 |
| ram   |   ₹500 | Snacks      |            3 |

The application calculates:

```text
amu → should receive ₹833.33
rina → should pay ₹166.67
ram → should pay ₹666.67
```

Settlement:

```text
rina pays amu ₹166.67
ram pays amu ₹666.67
```

This example is produced by the application's execution. 

---

#  Business Solution

The Expense Sharing Application can be used as a simple financial-management solution for groups where expenses are shared.

The proposed business solution is:

```text
Group Members
      ↓
Record Shared Expenses
      ↓
Automatically Split Expenses
      ↓
Calculate Individual Balances
      ↓
Identify Debtors & Creditors
      ↓
Generate Settlement Transactions
      ↓
Complete Payment Settlement
```

Instead of manually maintaining calculations in notebooks, messages, or spreadsheets, the application provides a structured method for recording and settling shared expenses.

---

#  Practical Applications

The concept can be useful for:

### 1. Friends

Friends can split:

* Restaurant bills
* Movie expenses
* Shopping expenses
* Snacks
* Entertainment

### 2. Travel Groups

Travel groups can manage:

* Hotel expenses
* Food
* Transportation
* Tickets
* Other trip expenses

### 3. Roommates

Roommates can track:

* Rent
* Electricity
* Internet
* Groceries
* Household expenses

### 4. College Students

Students can share:

* Food expenses
* Events
* Group purchases
* Travel expenses
* Project-related costs

### 5. Small Teams

Teams can use a similar system to track shared team expenses and reimbursements.

---

#  Key Features

The application provides:

*  Friend management
*  Expense recording
*  Expense descriptions
*  Participant selection
*  Automatic expense splitting
*  Pandas DataFrame generation
*  Net balance calculation
* Payment settlement
* Multiple expense support
* Object-Oriented Python implementation

These features are implemented through the `ExpenseSharing` class and its methods. 

---

#  Technologies Used

* Python
* Object-Oriented Programming (OOP)
* Pandas
* Lists
* Dictionaries
* Loops
* Conditional Statements
* Functions / Methods


#  Future Enhancements

The current project provides the core expense-sharing functionality.

Possible future improvements include:

* Add email and phone-number validation
* Add user authentication
* Store expenses permanently in a database
* Add a graphical user interface
* Add a web application using Flask
* Add payment-status tracking such as:

  * Pending
  * Partial
  * Completed
* Add custom split percentages
* Support unequal expense splitting
* Add expense history
* Add monthly expense summaries
* Add charts for spending analysis
* Add online payment integration

---

#  Project Outcome

This project demonstrates how Python and Object-Oriented Programming can be used to solve a practical real-world problem.

The application successfully:

* Accepts multiple group members
* Records expenses
* Calculates per-person costs
* Maintains expense history
* Calculates net balances
* Identifies who should pay and receive money
* Generates settlement transactions
* Displays expenses in a structured Pandas DataFrame

The sample execution demonstrates the complete flow from entering expenses to generating final settlement transactions. 

---

#  Conclusion

The Expense Sharing Application provides a simple and practical way to manage shared expenses among groups.

By automating **expense recording, cost splitting, balance calculation, and payment settlement**, the project reduces manual calculations and makes group expense management easier.

The project also demonstrates practical usage of:

* Python
* OOP
* Data structures
* Pandas
* Conditional logic
* Expense calculation algorithms

Overall, this project provides a strong foundation for developing a more advanced **expense-management application or web-based expense-sharing platform**.


