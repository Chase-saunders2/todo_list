
def show_menu():
    print("\n--- TO-DO LIST MENU ---")
    print("1. View tasks")
    print("2. Add a task")
    print("3. Complete a task")
    print("4. Delete a task")
    print("5. Save and Exit")

def view_tasks(tasks):
    if not tasks:
        print("No tasks yet!")
    else:
        for i, task in enumerate(tasks, 1):
            status = "✅" if task["done"] else "❌"
            print(f"{i}. {task['title']} {status}")

def add_task(tasks):
    title = input("Enter task: ")
    tasks.append({"title": title, "done": False})
    print(f"Added task: {title}")

def complete_task(tasks):
    view_tasks(tasks)
    choice = int(input("Enter task number to mark complete: ")) - 1
    if 0 <= choice < len(tasks):
        tasks[choice]["done"] = True
        print(f"Marked '{tasks[choice]['title']}' as complete!")

def delete_task(tasks):
    view_tasks(tasks)
    choice = int(input("Enter task number to delete: ")) - 1
    if 0 <= choice < len(tasks):
        removed = tasks.pop(choice)
        print(f"Deleted task: {removed['title']}")

def save_tasks(tasks, filename="tasks.txt"):
    with open(filename, "w") as f:
        for task in tasks:
            f.write(f"{task['title']}|{task['done']}\n")
    print("Tasks saved. Goodbye!")

def load_tasks(filename="tasks.txt"):
    tasks = []
    try:
        with open(filename, "r") as f:
            for line in f:
                title, done = line.strip().split("|")
                tasks.append({"title": title, "done": done == "True"})
    except FileNotFoundError:
        pass
    return tasks

def main():
    tasks = load_tasks()
    while True:
        show_menu()
        choice = input("Choose an option (1-5): ")

        if choice == "1":
            view_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            complete_task(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            save_tasks(tasks)
            break
        else:
            print("Invalid choice. Try again!")

if __name__ == "__main__":
    main()

