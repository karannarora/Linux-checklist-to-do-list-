#!/bin/bash
# File path for the todo.txt file
TODO_FILE="$HOME/todo.txt"
# Function to display the todo list
function display_todos {
if [[ ! -f $TODO_FILE ]]; then
echo "No todo list found. Start by adding a task!"
return
fi
echo "Your Todo List:"
cat -n "$TODO_FILE"
echo ""
}
# Function to add a new task
function add_todo {
  read -p "Enter your new task: " task
  echo "$task" >> "$TODO_FILE"
  echo "Task added!"
}
# Function to delete a task
function delete_todo {
  display_todos
  read -p "Enter the task number to delete: " task_number
  sed -i "${task_number}d" "$TODO_FILE"
  echo "Task deleted!"
}
# Main menu
while true; do
  echo "Todo List Manager"
  echo "1. Display Todos"
  echo "2. Add Todo"
  echo "3. Delete Todo"
  echo "4. Exit"
  read -p "Choose an option: " choice
  case $choice in
    1) display_todos ;;
    2) add_todo ;;
    3) delete_todo ;;
    4) exit 0 ;;
    *) echo "Invalid option. Please try again." ;;
  esac
done