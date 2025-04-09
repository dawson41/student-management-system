# student-management-system
student_result_management/
│
├── main.py
└── database.db
import sqlite3

# Connect to SQLite database
conn = sqlite3.connect('database.db')
c = conn.cursor()

# Create table
c.execute('''CREATE TABLE IF NOT EXISTS results
             (id INTEGER PRIMARY KEY, name TEXT, subject TEXT, score INTEGER)''')

def add_result(name, subject, score):
    c.execute("INSERT INTO results (name, subject, score) VALUES (?, ?, ?)", (name, subject, score))
    conn.commit()

def view_results():
    c.execute("SELECT * FROM results")
    return c.fetchall()

def main():
    while True:
        print("1. Add Result")
        print("2. View Results")
        print("3. Exit")
        choice = input("Enter your choice: ")

        if choice == '1':
            name = input("Enter student name: ")
            subject = input("Enter subject: ")
            score = int(input("Enter score: "))
            add_result(name, subject, score)
            print("Result added successfully.")
        elif choice == '2':
            results = view_results()
            for result in results:
                print(result)
        elif choice == '3':
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()

# Close the connection
conn.close()
