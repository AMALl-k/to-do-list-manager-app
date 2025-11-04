# to-do-list-manager-app
# TO DO LIST MANAGING APP
# load existing items
# 1. create a new item
# 2. list items
# 3. mark item as complete
# 4. save items

import json

file_name = "todo_list.json"

def load_tasks():
    try: 
        with open(file_name, "r") as file :
            return json.load(file)    
    except:
        return{"tasks":[]}
    
def save_tasks(tasks):
    try: 
        with open(file_name, "w") as file :
             json.dump(tasks, file)    
    except:
        print("Error saving tasks.")

def view_tasks(tasks):
    task_list = tasks["tasks"]
    if len(tasks["tasks"]) == 0:
        print("No tasks found.")

    else:  
        for idx, task in enumerate(task_list):
            status = "Completed" if task["completed"] else "Pending"
            print(f"{idx + 1}. {task['description']} - {status}")  

def create_task(tasks):
    description = input("Enter the task description: ").strip()
    if description:
        tasks["tasks"].append({"description": description, "completed": False})
        save_tasks(tasks)
        print(f'Task "{description}" added.')
    else:
        print("Task description cannot be empty.")

def mark_task_complete(tasks):
    view_tasks(tasks)
    try:
        task_number = int(input("Enter the task number to mark as complete: ").strip())
        if 1 <= task_number <= len(tasks["tasks"]):
            tasks["tasks"][task_number - 1]["completed"] = True
            save_tasks(tasks)
            print(f'Task "{tasks["tasks"][task_number - 1]["description"]}" marked as complete.')
        else:
             print("Invalid task number.")
    except:
        print("Please enter a valid number.")

def mark_task_incomplete(tasks):
    view_tasks(tasks)
    try:
        task_number = int(input("Enter the task number to mark as INCOMPLETE: ").strip())
        if 1 <= task_number <= len(tasks["tasks"]):
            tasks["tasks"][task_number - 1]["completed"] = False
            save_tasks(tasks)
            print(f'Task "{tasks["tasks"][task_number - 1]["description"]}" marked as incomplete.')
        else:
            print("Invalid task number.")
    except:
        print("Please enter a valid number.")

def delete_task(tasks):
    view_tasks(tasks)
    try:
        task_number = int(input("Enter the task number to delete: ").strip())
        if 1 <= task_number <= len(tasks["tasks"]):
            removed = tasks["tasks"].pop(task_number - 1)
            save_tasks(tasks)
            print(f'Task "{removed.get("description")}" deleted.')
        else:
            print("Invalid task number.")
    except:
        print("Please enter a valid number.")       


def main():
    tasks = load_tasks()
    print(tasks)

    while True:

        print("To-Do List Manager")
        print("1. View Tasks")
        print("2. Create Task")
        print("3. Mark Task as Complete")
        print("4. Save and Exit")
        print("5. Delete Task")
        print("6. Mark Task as Incomplete")

        choice = input("Choose an option (1-4): ").strip()

        if choice == '1':
            view_tasks()
        elif choice == '2':
            create_task(tasks)
        elif choice == '3':
            mark_task_complete(tasks)
        elif choice == '4':
            save_tasks()
            print("Tasks saved. Exiting...")
        elif choice == '5':
            delete_task(tasks)
        elif choice == '6':
            mark_task_incomplete(tasks)         
            break
        else:
            print("Invalid choice. Please try again.")            

main()

to_do_list.json file 
{"tasks": ["saved task", {"description": "wake up early", "completed": false}]}


# 📝 To-Do List Managing App

A simple, interactive **command-line To-Do List Manager** written in Python.  
This program allows users to create, view, mark, delete, and save their daily tasks.  
All tasks are stored in a local JSON file (`todo_list.json`) so they are automatically saved and loaded between runs.

---

## 🚀 Features

✅ Create new to-do items  
✅ View all saved tasks with completion status  
✅ Mark tasks as **complete** or **incomplete**  
✅ Delete unwanted tasks  
✅ Save tasks automatically to JSON file  
✅ Automatically load tasks when the program starts  

---

## 🛠️ Requirements

- Python **3.x**
- No external dependencies (only uses Python’s built-in libraries)

---

## 📚 Libraries Used

| Library | Type | Purpose |
|----------|------|----------|
| `json` | Built-in | To store, load, and save tasks in a `.json` file |
| `input()` | Built-in function | To collect user input for tasks and menu options |
| `print()` | Built-in function | To display options, tasks, and status messages |

---

## 🧠 Core Concepts Used

- **File Handling** – Reading/writing `.json` files for persistent storage  
- **Exception Handling** – Safely handling missing files or invalid user inputs  
- **Dictionaries & Lists** – Managing task data in structured format  
- **Functions** – Code modularization for clarity and reusability  
- **Conditional Logic** – Validating user input and controlling menu flow  

---

## 🧩 Data Structure Overview

All data is stored in a dictionary with a single key `"tasks"`, whose value is a list of task dictionaries:

```python
{
  "tasks": [
    {"description": "Finish Python project", "completed": False},
    {"description": "Buy groceries", "completed": True}
  ]
}
