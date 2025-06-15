import os

class Student:
    def __init__(self, roll, name, course):
        self.roll = roll
        self.name = name
        self.course = course

    def __str__(self):
        return f"Roll No: {self.roll}, Name: {self.name}, Course: {self.course}"

def add_student():
    roll = input("Enter Roll Number: ")
    name = input("Enter Name: ")
    course = input("Enter Course: ")

    student = Student(roll, name, course)
    with open("students.txt", "a") as f:
        f.write(f"{student.roll},{student.name},{student.course}\n")
    print("Student added successfully!\n")

def view_students():
    if not os.path.exists("students.txt"):
        print("No student records found.\n")
        return

    with open("students.txt", "r") as f:
        students = f.readlines()
        if not students:
            print("No student records found.\n")
        else:
            print("\nList of Students:")
            for line in students:
                roll, name, course = line.strip().split(",")
                print(f"Roll No: {roll}, Name: {name}, Course: {course}")
            print()

def search_student():
    roll_to_find = input("Enter Roll Number to Search: ")
    found = False

    with open("students.txt", "r") as f:
        for line in f:
            roll, name, course = line.strip().split(",")
            if roll == roll_to_find:
                print(f"\nStudent Found: Roll No: {roll}, Name: {name}, Course: {course}\n")
                found = True
                break
    if not found:
        print("Student not found.\n")

def delete_student():
    roll_to_delete = input("Enter Roll Number to Delete: ")
    found = False

    with open("students.txt", "r") as f:
        students = f.readlines()

    with open("students.txt", "w") as f:
        for line in students:
            roll, name, course = line.strip().split(",")
            if roll != roll_to_delete:
                f.write(line)
            else:
                found = True

    if found:
        print("Student deleted successfully.\n")
    else:
        print("Student not found.\n")

# Main Menu
while True:
    print("===== Student Management System =====")
    print("1. Add Student")
    print("2. View All Students")
    print("3. Search Student by Roll No")
    print("4. Delete Student by Roll No")
    print("5. Exit")
    choice = input("Enter your choice (1-5): ")

    if choice == "1":
        add_student()
    elif choice == "2":
        view_students()
    elif choice == "3":
        search_student()
    elif choice == "4":
        delete_student()
    elif choice == "5":
        print("Exiting program. Goodbye!")
        break
    else:
        print("Invalid choice. Please try again.\n")
