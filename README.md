# ScriptScape
Scripts
import json

class ToDoList:
    def __init__(self, filename="tasks.json"):
        self.filename = filename
        self.load_tasks()

    def load_tasks(self):
        try:
            with open(self.filename, "r") as file:
                self.tasks = json.load(file)
        except FileNotFoundError:
            self.tasks = []

    def save_tasks(self):
        with open(self.filename, "w") as file:
            json.dump(self.tasks, file, indent=4)

    def add_task(self, task):
        self.tasks.append({"task": task, "completed": False})
        self.save_tasks()

    def remove_task(self, index):
        if 0 <= index < len(self.tasks):
            del self.tasks[index]
            self.save_tasks()

    def complete_task(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks[index]["completed"] = True
            self.save_tasks()

    def display_tasks(self):
        for i, task in enumerate(self.tasks):
            status = "✔" if task["completed"] else "✘"
            print(f"{i + 1}. {task['task']} [{status}]")

def main():
    todo_list = ToDoList()

    while True:
        print("\nTo-Do List Menu")
        print("1. Add task")
        print("2. Remove task")
        print("3. Complete task")
        print("4. View tasks")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            task = input("Enter the task: ")
            todo_list.add_task(task)
        elif choice == "2":
            index = int(input("Enter the task number to remove: ")) - 1
            todo_list.remove_task(index)
        elif choice == "3":
            index = int(input("Enter the task number to complete: ")) - 1
            todo_list.complete_task(index)
        elif choice == "4":
            todo_list.display_tasks()
        elif choice == "5":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
