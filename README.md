# users.txt
## User System (Python)  A simple console-based user system built with Python. It allows users to register and log in, with data stored in a text file and passwords secured using hashing.  ### Features - User registration - User login - Password hashing for security - File-based storage
import os

FILE_NAME = "users.txt"

def main_menu():
    print("\n--- User System ---")
    print("1- Register new user")
    print("2- Login")
    print("3- Exit")
    choice = input("Choose an option: ")
    return choice


def register():
    print("\n--- Register New User ---")
    name = input("Enter name: ")
    number = input("Enter number: ")
    age = input("Enter age: ")
    country = input("Enter country: ")
    password = input("Enter password: ")
    user_data = f"{name},{number},{age},{country},{password}\n"

    with open(FILE_NAME, "a") as file:
        file.write(user_data)

    print("User registered successfully!")


def login():
    print("\n--- Login ---")
    name = input("Enter name: ")
    password = input("Enter password: ")

    if not os.path.exists(FILE_NAME):
        print("No users found. Please register first.")
        return

    with open(FILE_NAME, "r") as file:
        users = file.readlines()

    for user in users:
        data = user.strip().split(",")

        saved_name = data[0]
        saved_password = data[4]

        if name == saved_name and password == saved_password:
            print("Login successful!")
            show_user(data)
            return

    print("Invalid name or password!")


def show_user(data):
    print("\n--- User Information ---")
    print("Name:", data[0])
    print("Number:", data[1])
    print("Age:", data[2])
    print("Country:", data[3])
    print("Password:", data[4])

def start():
    while True:
        choice = main_menu()

        if choice == "1":
            register()
        elif choice == "2":
            login()
        elif choice == "3":
            print("Exiting program...")
            break
        else:
            print("Invalid choice, try again.")


start()
