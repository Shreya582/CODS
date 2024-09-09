# CODSOFT
# INERNSHIP PROJECT

import tkinter as tk
from tkinter import ttk
from tkinter import messagebox

class ToDoList:
    def _init_(self, root):
        self.root = root
        self.root.title("To-Do List App")
        self.tasks = []
        self.frame_tasks = tk.Frame(self.root)
        self.frame_tasks.pack(fill="both", expand=True)

        self.frame_buttons = tk.Frame(self.root)
        self.frame_buttons.pack(fill="x")

        self.task_list = tk.Listbox(self.frame_tasks, width=40)
        self.task_list.pack(side="left", fill="both", expand=True)
    
        self.scrollbar = tk.Scrollbar(self.frame_tasks)
        self.scrollbar.pack(side="right", fill="y")
        self.task_list.config(yscrollcommand=self.scrollbar.set)
        self.scrollbar.config(command=self.task_list.yview)
  
        self.button_add = tk.Button(self.frame_buttons, text="Add Task", command=self.add_task)
        self.button_add.pack(side="left")

        self.button_update = tk.Button(self.frame_buttons, text="Update Task", command=self.update_task)
        self.button_update.pack(side="left")

        self.button_delete = tk.Button(self.frame_buttons, text="Delete Task", command=self.delete_task)
        self.button_delete.pack(side="left")

        self.button_search = tk.Button(self.frame_buttons, text="Search Tasks", command=self.search_tasks)
        self.button_search.pack(side="left")

        self.button_quit = tk.Button(self.frame_buttons, text="Quit", command=self.root.quit)
        self.button_quit.pack(side="left")

    def add_task(self):
        task_window = tk.Toplevel(self.root)
        task_window.title("Add Task")

        label_task = tk.Label(task_window, text="Task:")
        label_task.pack()

        entry_task = tk.Entry(task_window, width=40)
        entry_task.pack()

        label_priority = tk.Label(task_window, text="Priority:")
        label_priority.pack()

        entry_priority = tk.Entry(task_window, width=40)
        entry_priority.pack()

        label_due_date = tk.Label(task_window, text="Due Date:")
        label_due_date.pack()

        entry_due_date = tk.Entry(task_window, width=40)
        entry_due_date.pack()

        def add_task_to_list():
            task = {"Task": entry_task.get(), "Priority": entry_priority.get(), "Due Date": entry_due_date.get()}
            self.tasks.append(task)
            self.task_list.insert("end", f"{task['Task']} - Priority: {task['Priority']} - Due Date: {task['Due Date']}")

        button_add = tk.Button(task_window, text="Add Task", command=add_task_to_list)
        button_add.pack()

    def update_task(self):
        task_window = tk.Toplevel(self.root)
        task_window.title("Update Task")

        label_task_number = tk.Label(task_window, text="Task Number:")
        label_task_number.pack()

        entry_task_number = tk.Entry(task_window, width=40)
        entry_task_number.pack()

        label_task = tk.Label(task_window, text="Task:")
        label_task.pack()

        entry_task = tk.Entry(task_window, width=40)
        entry_task.pack()

        label_priority = tk.Label(task_window, text="Priority:")
        label_priority.pack()

        entry_priority = tk.Entry(task_window, width=40)
        entry_priority.pack()

        label_due_date = tk.Label(task_window, text="Due Date:")
        label_due_date.pack()

        entry_due_date = tk.Entry(task_window, width=40)
        entry_due_date.pack()

        def update_task_in_list():
            task_number = int(entry_task_number.get()) - 1
            task = {"Task": entry_task.get(), "Priority": entry_priority.get(), "Due Date": entry_due_date.get()}
            self.tasks[task_number] = task
            self.task_list.delete(0, "end")
            for task in self.tasks:
                self.task_list.insert("end", f"{task['Task']} - Priority: {task['Priority']} - Due Date: {task['Due Date']}")

        button_update = tk.Button(task_window, text="Update Task", command=update_task_in_list)
        button_update.pack()

    def delete_task(self):
        task_window = tk.Toplevel(self.root)
        task_window.title("Delete Task")

        label_task_number = tk.Label(task_window, text="Task Number:")
        label_task_number.pack()

        entry_task_number = tk.Entry(task_window, width=40)
        entry_task_number.pack()

        def delete_task_from_list():
            task_number = int(entry_task_number.get())
