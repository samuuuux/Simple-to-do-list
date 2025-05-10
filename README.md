# Simple-to-do-list
import sys
import os

todo_file = "todo.txt"


def load_tasks():
    if not os.path.exists(todo_file):
        return []
    with open(todo_file, "r") as f:
        return [line.strip() for line in f.readlines()]


def save_tasks(tasks):
    with open(todo_file, "w") as f:
        for task in tasks:
            f.write(task + "\n")


def add_task(task):
    tasks = load_tasks()
    tasks.append(task)
    save_tasks(tasks)
    print(f"Added task: {task}")


def remove_task(index):
    tasks = load_tasks()
    try:
        removed = tasks.pop(index - 1)
        save_tasks(tasks)
        print(f"Removed task: {removed}")
    except IndexError:
        print("Error: Invalid task number.")


def view_tasks():
    tasks = load_tasks()
    if not tasks:
        print("No tasks in your to-do list.")
    else:
        print("Your To-Do List:")
        for i, task in enumerate(tasks, start=1):
            print(f"{i}. {task}")


def main():
    if len(sys.argv) < 2:
        print("Usage: python todo.py [add/remove/view] [task/number]")
        return

    command = sys.argv[1].lower()

    if command == "add" and len(sys.argv) >= 3:
        task = " ".join(sys.argv[2:])
        add_task(task)
    elif command == "remove" and len(sys.argv) == 3:
        try:
            index = int(sys.argv[2])
            remove_task(index)
        except ValueError:
            print("Error: Task number must be an integer.")
    elif command == "view":
        view_tasks()
    else:
        print("Invalid command or arguments.")


if __name__ == "__main__":
    main()
