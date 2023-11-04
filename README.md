# Expenses-tracker-
import csv

# Initialize an empty list to store expenses
expenses = []

# Load existing expenses from a CSV file, if available
def load_expenses():
    try:
        with open("expenses.csv", mode="r", newline="") as file:
            reader = csv.DictReader(file)
            for row in reader:
                expenses.append(row)
    except FileNotFoundError:
        pass

# Save expenses to a CSV file
def save_expenses():
    with open("expenses.csv", mode="w", newline="") as file:
        fieldnames = ["Date", "Description", "Category", "Amount"]
        writer = csv.DictWriter(file, fieldnames=fieldnames)
        writer.writeheader()
        for expense in expenses:
            writer.writerow(expense)

# Add a new expense
def add_expense():
    date = input("Enter the date (YYYY-MM-DD): ")
    description = input("Enter a description: ")
    category = input("Enter a category: ")
    amount = float(input("Enter the amount: "))

    expense = {
        "Date": date,
        "Description": description,
        "Category": category,
        "Amount": amount,
    }

    expenses.append(expense)
    print("Expense added successfully.")

# View all expenses
def view_expenses():
    if not expenses:
        print("No expenses recorded yet.")
    else:
        for expense in expenses:
            print(
                f"Date: {expense['Date']}, Description: {expense['Description']}, "
                f"Category: {expense['Category']}, Amount: rs {expense['Amount']:.2f}"
            )

# Main loop
load_expenses()
while True:
    print("\nExpense Tracker")
    print("1. Add an Expense")
    print("2. View Expenses")
    print("3. Exit")
    choice = input("Enter your choice (1/2/3): ")

    if choice == "1":
        add_expense()
    elif choice == "2":
        view_expenses()
    elif choice == "3":
        save_expenses()
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Please choose 1, 2, or 3.")
