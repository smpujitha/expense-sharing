print("Welcome to the Expense Sharing App")
import pandas as pd
class ExpenseSharing:
    def __init__(self,friends):
        self.friends = [{"name": name, "email": "", "phoneno": ""} for name in friends]
        self.expenses = {friend['name']: [] for friend in self.friends}


    def add_expense(self,payer,amount,description,participants):
        expense={
            "payer": payer,
            "amount": amount,
            "description": description,
            "participants": participants
        }
        self.expenses[payer].append(expense)

        return expense
    def calculate_balances(self):
        self.balances = {friend['name']: 0 for friend in self.friends}
        for payer, expense_list in self.expenses.items():
            for expense in expense_list:
                participants = expense['participants']
                amount=expense['amount']
                if len(expense['participants']) == 0:
                    split_amount = 0
                else:
                    split_amount = expense['amount'] / len(expense['participants'])
                for participant in expense['participants']:
                   self.balances[participant] -= split_amount
                self.balances[payer] += expense['amount']
    def calculate_settlements(self):
        creditors=[]
        debtors=[]
        transactions=[]

        for friend, balance in self.balances.items():
            if balance > 0:
                creditors.append((friend, balance))
            elif balance < 0:
                debtors.append((friend, -balance))
        creditors.sort(key=lambda x: x[1], reverse=True)
        debtors.sort(key=lambda x: x[1], reverse=True)
        while debtors and creditors:
            debtor , debt_amount = debtors.pop()
            creditor, credit_amount = creditors.pop()
            settlement_amount = min(debt_amount, credit_amount)
            print(f"{debtor} pays {creditor} ${settlement_amount:.2f}")
            if debt_amount > credit_amount:
                debtors.append((debtor, debt_amount - settlement_amount))
                debtors.sort(key=lambda x: x[1])
            elif credit_amount > debt_amount:
                creditors.append((creditor, credit_amount - settlement_amount))
                creditors.sort(key=lambda x: x[1])
        transactions.append({
            "from": creditor,
            "to": debtor,
            "amount": settlement_amount,
            "status": "pending"})
        return transactions
    def refund(self, payer, amount, description, to_person,):
        refund_expense ={
            "from_person": payer,
            "to_person": to_person ,
            "amount": amount,
            "description": description,
            "status": "pending",
            "refund_date":pd.Timestamp.now()
        }
        return refund_expense

    def generate_expense_df(self):
        all_expenses = []

        for payer, expenses_list in self.expenses.items():
            for exp in expenses_list:
                all_expenses.append({
                    "Payer": payer,
                    "Amount": exp["amount"],
                    "Description": exp["description"],
                    "Num_Participants": len(exp["participants"]),
                    "Per_Person_Cost": exp["amount"] / len(exp["participants"])
                    if len(exp["participants"]) > 0 else 0
                })

        expense_df = pd.DataFrame(all_expenses)
        return expense_df
if __name__ == "__main__":
    print("DEBUG: Entered main")
    friends_input = input("Enter the names of friends (comma-separated): ")
    friends = [name.strip() for name in friends_input.split(",")]

   ## friends = ["balamurugan", "kathiravan", "velmurugan", "Murugan", "karthikeyan", "kumaran"]
    expense_sharing = ExpenseSharing(friends)
    while True:

       payer = input("Enter the name of the payer(is the expense done if done type 'done'): ")
       if payer.lower()=='done':
            break
       else:
           amount = float(input("Enter the amount paid: "))
           description = input("Enter a description for the expense: ")
           participants_input = input("Enter the names of participants (comma-separated): ")
           participants = [name.strip() for name in participants_input.split(",")]

                # Add expense
           expense_sharing.add_expense(payer, amount, description, participants)
           print(f"Expense added!\n")
##exp1=expense_sharing.add_expense("balamurugan", 1000, "LUNCH", ["balamurugan", "kathiravan", "velmurugan"])
##exp2=expense_sharing.add_expense("kathiravan", 3500, "PRINTOUT ", ["balamurugan", "kathiravan", "velmurugan", "Murugan"])
##exp3=expense_sharing.add_expense("velmurugan", 800, "movie tickets", ["balamurugan", "kathiravan", "velmurugan", "Murugan", "karthikeyan", "kumaran"])
##exp4=expense_sharing.add_expense("Murugan", 1500, "popcorn", ["balamurugan", "kathiravan", "velmurugan", "Murugan", "karthikeyan", "kumaran"])
##exp5=expense_sharing.add_expense("karthikeyan", 2000, "dinner", ["balamurugan", "kathiravan", "velmurugan", "Murugan", "karthikeyan"])
##exp6=expense_sharing.add_expense("kumaran", 500, "snacks", ["balamurugan", "kathiravan", "velmurugan", "Murugan", "karthikeyan", "kumaran"])

expense_sharing.calculate_balances()
print("\n.........balances:......")
for friend, balance in expense_sharing.balances.items():
    print(f"{friend}: ${balance:.2f}")
print("\n--- Settlement Transactions ---")
transactions = expense_sharing.calculate_settlements()

print("\n-----------EXPENSES DETAILS-------------")

expense_df = expense_sharing.generate_expense_df()
print(expense_df)
