import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Task {
    private String name;
    private boolean completed;

    public Task(String name) {
        this.name = name;
        this.completed = false;
    }

    public String getName() {
        return name;
    }

    public boolean isCompleted() {
        return completed;
    }

    public void markAsCompleted() {
        this.completed = true;
    }

    @Override
    public String toString() {
        return "Task: " + name + " (Completed: " + completed + ")";
    }
}

class Project {
    private String name;
    private List<Task> tasks;

    public Project(String name) {
        this.name = name;
        this.tasks = new ArrayList<>();
    }

    public String getName() {
        return name;
    }

    public List<Task> getTasks() {
        return tasks;
    }

    public void addTask(String taskName) {
        Task task = new Task(taskName);
        tasks.add(task);
    }

    public void markTaskAsCompleted(int taskIndex) {
        if (taskIndex >= 0 && taskIndex < tasks.size()) {
            tasks.get(taskIndex).markAsCompleted();
        } else {
            System.out.println("Invalid task index.");
        }
    }

    @Override
    public String toString() {
        return "Project: " + name + "\n" + tasks.toString();
    }
}

public class ProjectManagementTool {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        List<Project> projects = new ArrayList<>();

        while (true) {
            System.out.println("\nProject Management Tool");
            System.out.println("1. Create a new project");
            System.out.println("2. List all projects");
            System.out.println("3. Select a project");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter project name: ");
                    String projectName = scanner.nextLine();
                    Project project = new Project(projectName);
                    projects.add(project);
                    System.out.println("Project created: " + projectName);
                    break;
                case 2:
                    System.out.println("\nList of Projects:");
                    for (int i = 0; i < projects.size(); i++) {
                        System.out.println(i + ". " + projects.get(i).getName());
                    }
                    break;
                case 3:
                    System.out.print("Enter project index: ");
                    int projectIndex = scanner.nextInt();
                    if (projectIndex >= 0 && projectIndex < projects.size()) {
                        Project selectedProject = projects.get(projectIndex);
                        while (true) {
                            System.out.println("\nSelected Project: " + selectedProject.getName());
                            System.out.println("1. Add task");
                            System.out.println("2. List tasks");
                            System.out.println("3. Mark task as completed");
                            System.out.println("4. Back to main menu");
                            System.out.print("Enter your choice: ");
                            int projectChoice = scanner.nextInt();
                            scanner.nextLine(); // Consume newline

                            switch (projectChoice) {
                                case 1:
                                    System.out.print("Enter task name: ");
                                    String taskName = scanner.nextLine();
                                    selectedProject.addTask(taskName);
                                    System.out.println("Task added: " + taskName);
                                    break;
                                case 2:
                                    List<Task> tasks = selectedProject.getTasks();
                                    System.out.println("\nTasks:");
                                    for (int i = 0; i < tasks.size(); i++) {
                                        System.out.println(i + ". " + tasks.get(i).toString());
                                    }
                                    break;
                                case 3:
                                    System.out.print("Enter task index to mark as completed: ");
                                    int taskIndex = scanner.nextInt();
                                    selectedProject.markTaskAsCompleted(taskIndex);
                                    break;
                                case 4:
                                    break;
                                default:
                                    System.out.println("Invalid choice.");
                            }

                            if (projectChoice == 4) {
                                break;
                            }
                        }
                    } else {
                        System.out.println("Invalid project index.");
                    }
                    break;
                case 4:
                    System.out.println("Exiting the Project Management Tool.");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid choice.");
            }
        }
    }
}
