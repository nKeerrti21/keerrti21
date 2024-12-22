// A Simple Java Project: Task Manager
// This program allows users to add, view, and complete tasks in a task management system.

import java.util.ArrayList;
import java.util.Scanner;

class Task {
    private String description;
    private boolean isCompleted;

    public Task(String description) {
        this.description = description;
        this.isCompleted = false;
    }

    public String getDescription() {
        return description;
    }

    public boolean isCompleted() {
        return isCompleted;
    }

    public void markCompleted() {
        this.isCompleted = true;
    }
}

class TaskManager {
    private ArrayList<Task> tasks;

    public TaskManager() {
        this.tasks = new ArrayList<>();
    }

    public void addTask(String description) {
        tasks.add(new Task(description));
        System.out.println("Task \"" + description + "\" added successfully!");
    }

    public void viewTasks() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks available.");
            return;
        }

        System.out.println("\nTasks:");
        for (int i = 0; i < tasks.size(); i++) {
            Task task = tasks.get(i);
            String status = task.isCompleted() ? "Completed" : "Pending";
            System.out.println((i + 1) + ". " + task.getDescription() + " [" + status + "]");
        }
    }

    public void completeTask(int taskNumber) {
        if (taskNumber > 0 && taskNumber <= tasks.size()) {
            Task task = tasks.get(taskNumber - 1);
            task.markCompleted();
            System.out.println("Task " + taskNumber + " marked as completed!");
        } else {
            System.out.println("Invalid task number.");
        }
    }

    public void deleteTask(int taskNumber) {
        if (taskNumber > 0 && taskNumber <= tasks.size()) {
            Task removedTask = tasks.remove(taskNumber - 1);
            System.out.println("Task \"" + removedTask.getDescription() + "\" deleted successfully!");
        } else {
            System.out.println("Invalid task number.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        TaskManager manager = new TaskManager();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nTask Manager");
            System.out.println("1. Add Task");
            System.out.println("2. View Tasks");
            System.out.println("3. Complete Task");
            System.out.println("4. Delete Task");
            System.out.println("5. Exit");

            System.out.print("Enter your choice: ");
            String choice = scanner.nextLine();

            switch (choice) {
                case "1":
                    System.out.print("Enter the task description: ");
                    String taskDescription = scanner.nextLine();
                    manager.addTask(taskDescription);
                    break;
                case "2":
                    manager.viewTasks();
                    break;
                case "3":
                    try {
                        System.out.print("Enter the task number to complete: ");
                        int taskNumber = Integer.parseInt(scanner.nextLine());
                        manager.completeTask(taskNumber);
                    } catch (NumberFormatException e) {
                        System.out.println("Please enter a valid number.");
                    }
                    break;
                case "4":
                    try {
                        System.out.print("Enter the task number to delete: ");
                        int taskNumber = Integer.parseInt(scanner.nextLine());
                        manager.deleteTask(taskNumber);
                    } catch (NumberFormatException e) {
                        System.out.println("Please enter a valid number.");
                    }
                    break;
                case "5":
                    System.out.println("Exiting Task Manager. Goodbye!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
