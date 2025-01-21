# Log-Event-Editor
import os

# Function to view logs
def view_logs():
    log_file = "/var/log/syslog"  # You can modify it to any other log file like /var/log/auth.log
    if os.path.exists(log_file):
        with open(log_file, 'r') as file:
            print(file.read())
    else:
        print("Log file does not exist.")

# Function to add a log
def add_log(message):
    log_file = "/var/log/syslog"
    with open(log_file, 'a') as file:
        file.write(f"{message}\n")
    print(f"Log added: {message}")

# Function to edit a log
def edit_log(search_str, replace_str):
    log_file = "/var/log/syslog"
    if os.path.exists(log_file):
        with open(log_file, 'r') as file:
            logs = file.readlines()

        with open(log_file, 'w') as file:
            for log in logs:
                if search_str in log:
                    log = log.replace(search_str, replace_str)
                file.write(log)
        print(f"Edited log: {search_str} to {replace_str}")
    else:
        print("Log file does not exist.")

# Function to delete a log
def delete_log(delete_str):
    log_file = "/var/log/syslog"
    if os.path.exists(log_file):
        with open(log_file, 'r') as file:
            logs = file.readlines()

        with open(log_file, 'w') as file:
            for log in logs:
                if delete_str not in log:
                    file.write(log)
        print(f"Deleted logs containing: {delete_str}")
    else:
        print("Log file does not exist.")

# Menu to provide options to the user
def menu():
    while True:
        print("\nEvent Log Editor")
        print("1. View Logs")
        print("2. Add Log")
        print("3. Edit Log")
        print("4. Delete Log")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            view_logs()
        elif choice == "2":
            message = input("Enter log message to add: ")
            add_log(message)
        elif choice == "3":
            search_str = input("Enter log entry to search for: ")
            replace_str = input("Enter new log entry: ")
            edit_log(search_str, replace_str)
        elif choice == "4":
            delete_str = input("Enter log entry to delete: ")
            delete_log(delete_str)
        elif choice == "5":
            print("Exiting the Event Log Editor...")
            break
        else:
            print("Invalid choice! Please enter a valid option.")

if __name__ == "__main__":
    menu()
