import json
import os

# Define the file to store the tasks
TASKS_FILE = 'tasks.json'

# Function to load tasks from the file
def load_tasks():
    if os.path.exists(TASKS_FILE):
        with open(TASKS_FILE, 'r') as file:
            return json.load(file)
    return []

# Function to save tasks to the file
def save_tasks(tasks):
    with open(TASKS_FILE, 'w') as file:
        json.dump(tasks, file, indent=4)

# Function to display the tasks
def display_tasks(tasks):
    if not tasks:
        print("No tasks in the to-do list.")
    else:
        print("\nTo-Do List:")
        for idx, task in enumerate(tasks, 1):
            status = "Done" if task['completed'] else "Pending"
            print(f"{idx}. {task['description']} - {status}")
        print()

# Function to add a task
def add_task(tasks):
    description = input("Enter the task description: ")
    task = {'description': description, 'completed': False}
    tasks.append(task)
    save_tasks(tasks)
    print("Task added successfully!")

# Function to mark a task as completed
def complete_task(tasks):
    display_tasks(tasks)
    if not tasks:
        return
    task_number = int(input("Enter the task number to mark as completed: "))
    if 1 <= task_number <= len(tasks):
        tasks[task_number - 1]['completed'] = True
        save_tasks(tasks)
        print("Task marked as completed!")
    else:
        print("Invalid task number.")

# Function to delete a task
def delete_task(tasks):
    display_tasks(tasks)
    if not tasks:
        return
    task_number = int(input("Enter the task number to delete: "))
    if 1 <= task_number <= len(tasks):
        tasks.pop(task_number - 1)
        save_tasks(tasks)
        print("Task deleted successfully!")
    else:
        print("Invalid task number.")

# Main function to run the To-Do List application
def main():
    tasks = load_tasks()

    while True:
        print("\nTo-Do List Application")
        print("1. View tasks")
        print("2. Add a task")
        print("3. Mark a task as completed")
        print("4. Delete a task")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            display_tasks(tasks)
        elif choice == '2':
            add_task(tasks)
        elif choice == '3':
            complete_task(tasks)
        elif choice == '4':
            delete_task(tasks)
        elif choice == '5':
            print("Exiting the application.")
            break
        else:
            print("Invalid choice. Please choose a valid option.")

if __name__ == "__main__":
    main()
