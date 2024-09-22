# Expense-Tracker

import os
from datetime import datetime

# Initialize an empty list to hold expense records
expenses = []

def add_expense(amount, category):
    """Add a new expense to the list."""
    expense = {
        'date': datetime.now().strftime('%Y-%m-%d'),
        'amount': amount,
        'category': category
    }
    expenses.append(expense)

def generate_report():
    """Generate a summary report of expenses."""
    report = {}
    total_expense = 0

    for expense in expenses:
        total_expense += expense['amount']
        category = expense['category']
        if category in report:
            report[category]['total'] += expense['amount']
            report[category]['count'] += 1
        else:
            report[category] = {'total': expense['amount'], 'count': 1}

    print("\n--- Expense Summary Report ---")
    for category, details in report.items():
        print(f"Category: {category}")
        print(f"Total Amount: ${details['total']:.2f}")
        print(f"Count: {details['count']}")
        print("------------------------------")
    print(f"Total Expenses: Rs.{total_expense:.2f}")

if __name__ == "__main__":

    while True:
        print("\nExpense Tracker")
        print("1. Add Expense")
        print("2. Generate Report")
        print("3. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            try:
                amount = float(input("Enter amount: "))
                print("Categories: Food, Transport, Medical, Bills, Fee, Others")
                category = input("Enter category from the list above: ")
                add_expense(amount, category)
                print("Expense added successfully.")
            except ValueError:
                print("Invalid amount. Please enter a number.")
        elif choice == '2':
            generate_report()
        elif choice == '3':
            print("Exiting...")
            break
        else:
            print("Invalid choice. Please try again.")
