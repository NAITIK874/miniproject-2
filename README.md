import csv
from datetime import datetime

class Expense:
    def __init__(self, date, category, description, amount):
        self.date = date
        self.category = category
        self.description = description
        self.amount = amount

class ExpenseLogger:
    def __init__(self, filename='expenses.csv'):
        self.filename = filename

    def add_expense(self, expense):
        with open(self.filename, mode='a', newline='') as file:
            writer = csv.writer(file)
            writer.writerow([expense.date, expense.category, expense.description, expense.amount])
        print("Expense added successfully!")

    def view_expenses(self):
        try:
            with open(self.filename, mode='r') as file:
                reader = csv.reader(file)
                print("\nExpenses:")
                print(f"{'Date':<12} {'Category':<15} {'Description':<25} {'Amount':>8}")
                print("-" * 60)
                for row in reader:
                    print(f"{row[0]:<12} {row[1]:<15} {row[2]:<25} {row[3]:>8}")
        except FileNotFoundError:
            print("No expenses found yet.")

# -----------------------------
# Main program loop
# -----------------------------
logger = ExpenseLogger()

while True:
    print("\nExpense Logger")
    print("1. Add Expense")
    print("2. View Expenses")
    print("3. Exit")

    choice = input("Enter your choice: ")

    if choice == '1':
        date = datetime.now().strftime("%Y-%m-%d")
        category = input("Enter category (e.g., Food, Travel): ")
        description = input("Enter description: ")
        amount = input("Enter amount: ")
        expense = Expense(date, category, description, amount)
        logger.add_expense(expense)

    elif choice == '2':
        logger.view_expenses()

    elif choice == '3':
        print("Goodbye!")
        break

    else:
        print("Invalid choice. Try again.")
