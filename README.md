# Poo-consol-employer-dev

Voici comment vous pouvez structurer votre projet Java en suivant les spécifications demandées. Chaque classe ou interface sera implémentée dans un fichier séparé.

### 1. Interface `EmployeeOperations`
Cette interface définit les opérations de base pour la gestion des employés.

```java
// EmployeeOperations.java
public interface EmployeeOperations {
    void addEmployee(Employee employee);
    void removeEmployee(int id);
    void displayAllEmployees();
    void displayEmployee(int id);
}
```

### 2. Classe Abstraite `Employee`
Cette classe représente un employé avec des attributs de base et une méthode abstraite qui sera définie dans les sous-classes.

```java
// Employee.java
public abstract class Employee {
    private int id;
    private String name;
    private String position;
    private double salary;

    public Employee(int id, String name, String position, double salary) {
        this.id = id;
        this.name = name;
        this.position = position;
        this.salary = salary;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getPosition() {
        return position;
    }

    public double getSalary() {
        return salary;
    }

    public void setId(int id) {
        this.id = id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setPosition(String position) {
        this.position = position;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    // Méthode abstraite
    public abstract void displayDetails();

    @Override
    public String toString() {
        return "Employee [ID=" + id + ", Name=" + name + ", Position=" + position + ", Salary=" + salary + "]";
    }
}
```

### 3. Classe `Manager`
Cette classe hérite de `Employee` et ajoute des spécificités pour les managers, comme le nombre de personnes qu'il gère.

```java
// Manager.java
public class Manager extends Employee {
    private int numberOfPeople;

    public Manager(int id, String name, String position, double salary, int numberOfPeople) {
        super(id, name, position, salary);
        this.numberOfPeople = numberOfPeople;
    }

    public int getNumberOfPeople() {
        return numberOfPeople;
    }

    public void setNumberOfPeople(int numberOfPeople) {
        this.numberOfPeople = numberOfPeople;
    }

    @Override
    public void displayDetails() {
        System.out.println(super.toString() + ", Manages " + numberOfPeople + " people.");
    }
}
```

### 4. Classe `Developer`
Cette classe hérite de `Employee` et ajoute des spécificités pour les développeurs, comme la spécialisation dans un langage particulier.

```java
// Developer.java
public class Developer extends Employee {
    private String programmingLanguage;

    public Developer(int id, String name, String position, double salary, String programmingLanguage) {
        super(id, name, position, salary);
        this.programmingLanguage = programmingLanguage;
    }

    public String getProgrammingLanguage() {
        return programmingLanguage;
    }

    public void setProgrammingLanguage(String programmingLanguage) {
        this.programmingLanguage = programmingLanguage;
    }

    @Override
    public void displayDetails() {
        System.out.println(super.toString() + ", Specializes in " + programmingLanguage + ".");
    }
}
```

### 5. Classe `EmployeeManager`
Cette classe gère les employés en implémentant l'interface `EmployeeOperations`. Elle permet d'ajouter, de supprimer et d'afficher les employés.

```java
// EmployeeManager.java
import java.util.ArrayList;
import java.util.List;

public class EmployeeManager implements EmployeeOperations {
    private List<Employee> employees;

    public EmployeeManager() {
        employees = new ArrayList<>();
    }

    @Override
    public void addEmployee(Employee employee) {
        employees.add(employee);
        System.out.println("Employé ajouté avec succès !");
    }

    @Override
    public void removeEmployee(int id) {
        Employee employeeToRemove = null;
        for (Employee employee : employees) {
            if (employee.getId() == id) {
                employeeToRemove = employee;
                break;
            }
        }

        if (employeeToRemove != null) {
            employees.remove(employeeToRemove);
            System.out.println("Employé supprimé avec succès !");
        } else {
            System.out.println("Aucun employé trouvé avec l'ID " + id);
        }
    }

    @Override
    public void displayAllEmployees() {
        if (employees.isEmpty()) {
            System.out.println("Aucun employé enregistré.");
        } else {
            for (Employee employee : employees) {
                employee.displayDetails();
            }
        }
    }

    @Override
    public void displayEmployee(int id) {
        for (Employee employee : employees) {
            if (employee.getId() == id) {
                employee.displayDetails();
                return;
            }
        }
        System.out.println("Aucun employé trouvé avec l'ID " + id);
    }
}
```

### 6. Classe `Main`
Cette classe contient le point d'entrée du programme et gère l'interaction utilisateur via la console.

```java
// Main.java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        EmployeeManager manager = new EmployeeManager();
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n*** Gestion des Employés ***");
            System.out.println("1. Ajouter un Manager");
            System.out.println("2. Ajouter un Développeur");
            System.out.println("3. Supprimer un employé par ID");
            System.out.println("4. Afficher tous les employés");
            System.out.println("5. Afficher un employé par ID");
            System.out.println("6. Quitter");
            System.out.print("Choisissez une option: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Entrer l'ID: ");
                    int managerId = scanner.nextInt();
                    scanner.nextLine(); // Consommer la nouvelle ligne

                    System.out.print("Entrer le nom: ");
                    String managerName = scanner.nextLine();

                    System.out.print("Entrer le poste: ");
                    String managerPosition = scanner.nextLine();

                    System.out.print("Entrer le salaire: ");
                    double managerSalary = scanner.nextDouble();

                    System.out.print("Nombre de personnes gérées: ");
                    int numberOfPeople = scanner.nextInt();

                    Manager newManager = new Manager(managerId, managerName, managerPosition, managerSalary, numberOfPeople);
                    manager.addEmployee(newManager);
                    break;

                case 2:
                    System.out.print("Entrer l'ID: ");
                    int developerId = scanner.nextInt();
                    scanner.nextLine(); // Consommer la nouvelle ligne

                    System.out.print("Entrer le nom: ");
                    String developerName = scanner.nextLine();

                    System.out.print("Entrer le poste: ");
                    String developerPosition = scanner.nextLine();

                    System.out.print("Entrer le salaire: ");
                    double developerSalary = scanner.nextDouble();
                    scanner.nextLine(); // Consommer la nouvelle ligne

                    System.out.print("Langage de programmation: ");
                    String programmingLanguage = scanner.nextLine();

                    Developer newDeveloper = new Developer(developerId, developerName, developerPosition, developerSalary, programmingLanguage);
                    manager.addEmployee(newDeveloper);
                    break;

                case 3:
                    System.out.print("Entrer l'ID de l'employé à supprimer: ");
                    int removeId = scanner.nextInt();
                    manager.removeEmployee(removeId);
                    break;

                case 4:
                    manager.displayAllEmployees();
                    break;

                case 5:
                    System.out.print("Entrer l'ID de l'employé à afficher: ");
                    int displayId = scanner.nextInt();
                    manager.displayEmployee(displayId);
                    break;

                case 6:
                    System.out.println("Quitter le programme...");
                    break;

                default:
                    System.out.println("Option invalide! Veuillez réessayer.");
            }
        } while (choice != 6);

        scanner.close();
    }
}
```

### Explication

1. **Interface `EmployeeOperations`** : Elle définit les opérations de base pour la gestion des employés, telles que l'ajout, la suppression, et l'affichage des employés.
2. **Classe Abstraite `Employee`** : Cette classe contient les attributs de base pour un employé et une méthode abstraite `displayDetails()` que chaque sous-classe implémentera.
3. **Classe `Manager`** : Hérite de `Employee` et ajoute un attribut pour le nombre de personnes que le manager gère. La méthode `displayDetails()` est définie pour afficher ces informations supplémentaires.
4. **Classe `Developer`** : Hérite de `Employee` et ajoute un attribut pour le langage de programmation. La méthode `displayDetails()` affiche cette spécialisation.
5. **Classe `EmployeeManager`** : Gère la liste des employés et implémente les méthodes définies dans l'interface `EmployeeOperations`.
6. **Classe `Main`** : Gère l'interaction avec l'utilisateur via un menu en boucle, permettant d'ajouter, de supprimer, ou d'afficher des employés.
7. 

### Comment exécuter

Compilez tous les fichiers Java et 
exécutez la classe `Main`. Le programme vous guidera à travers le menu pour gérer les employés de l'entreprise en fonction de leur rôle (Manager ou Développeur).






Pour ajouter une méthode de mise à jour des informations d'un employé, vous pouvez modifier la classe `EmployeeManager` pour inclure cette fonctionnalité. Voici les modifications nécessaires :

### Mise à jour dans l'interface `EmployeeOperations`

Ajoutez une méthode `updateEmployee` dans l'interface pour définir la signature de cette fonctionnalité.

```java
// EmployeeOperations.java
public interface EmployeeOperations {
    void addEmployee(Employee employee);
    void removeEmployee(int id);
    void displayAllEmployees();
    void displayEmployee(int id);
    void updateEmployee(int id);  // Nouvelle méthode pour la mise à jour
}
```

### Implémentation de la méthode `updateEmployee` dans la classe `EmployeeManager`

Ajoutez la méthode `updateEmployee` dans la classe `EmployeeManager` pour permettre la mise à jour des informations d'un employé existant.

```java
// EmployeeManager.java
import java.util.Scanner;

public class EmployeeManager implements EmployeeOperations {
    private List<Employee> employees;
    private Scanner scanner;

    public EmployeeManager() {
        employees = new ArrayList<>();
        scanner = new Scanner(System.in);
    }

    @Override
    public void addEmployee(Employee employee) {
        employees.add(employee);
        System.out.println("Employé ajouté avec succès !");
    }

    @Override
    public void removeEmployee(int id) {
        Employee employeeToRemove = null;
        for (Employee employee : employees) {
            if (employee.getId() == id) {
                employeeToRemove = employee;
                break;
            }
        }

        if (employeeToRemove != null) {
            employees.remove(employeeToRemove);
            System.out.println("Employé supprimé avec succès !");
        } else {
            System.out.println("Aucun employé trouvé avec l'ID " + id);
        }
    }

    @Override
    public void displayAllEmployees() {
        if (employees.isEmpty()) {
            System.out.println("Aucun employé enregistré.");
        } else {
            for (Employee employee : employees) {
                employee.displayDetails();
            }
        }
    }

    @Override
    public void displayEmployee(int id) {
        for (Employee employee : employees) {
            if (employee.getId() == id) {
                employee.displayDetails();
                return;
            }
        }
        System.out.println("Aucun employé trouvé avec l'ID " + id);
    }

    @Override
    public void updateEmployee(int id) {
        for (Employee employee : employees) {
            if (employee.getId() == id) {
                System.out.println("Employé trouvé :");
                employee.displayDetails();

                System.out.println("Que souhaitez-vous mettre à jour?");
                System.out.println("1. Nom");
                System.out.println("2. Poste");
                System.out.println("3. Salaire");
                if (employee instanceof Manager) {
                    System.out.println("4. Nombre de personnes gérées");
                } else if (employee instanceof Developer) {
                    System.out.println("4. Langage de programmation");
                }
                System.out.print("Choix : ");
                int choice = scanner.nextInt();
                scanner.nextLine(); // Consommer la nouvelle ligne

                switch (choice) {
                    case 1:
                        System.out.print("Entrer le nouveau nom : ");
                        String newName = scanner.nextLine();
                        employee.setName(newName);
                        break;
                    case 2:
                        System.out.print("Entrer le nouveau poste : ");
                        String newPosition = scanner.nextLine();
                        employee.setPosition(newPosition);
                        break;
                    case 3:
                        System.out.print("Entrer le nouveau salaire : ");
                        double newSalary = scanner.nextDouble();
                        employee.setSalary(newSalary);
                        break;
                    case 4:
                        if (employee instanceof Manager) {
                            System.out.print("Entrer le nouveau nombre de personnes gérées : ");
                            int newNumberOfPeople = scanner.nextInt();
                            ((Manager) employee).setNumberOfPeople(newNumberOfPeople);
                        } else if (employee instanceof Developer) {
                            System.out.print("Entrer le nouveau langage de programmation : ");
                            String newProgrammingLanguage = scanner.nextLine();
                            ((Developer) employee).setProgrammingLanguage(newProgrammingLanguage);
                        }
                        break;
                    default:
                        System.out.println("Choix invalide !");
                        break;
                }
                System.out.println("Employé mis à jour avec succès !");
                return;
            }
        }
        System.out.println("Aucun employé trouvé avec l'ID " + id);
    }
}
```

### Mise à jour dans la classe `Main`

Ajoutez l'option de mise à jour dans le menu interactif de la classe `Main`.

```java
// Main.java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        EmployeeManager manager = new EmployeeManager();
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n*** Gestion des Employés ***");
            System.out.println("1. Ajouter un Manager");
            System.out.println("2. Ajouter un Développeur");
            System.out.println("3. Supprimer un employé par ID");
            System.out.println("4. Afficher tous les employés");
            System.out.println("5. Afficher un employé par ID");
            System.out.println("6. Mettre à jour un employé par ID");  // Nouvelle option de mise à jour
            System.out.println("7. Quitter");
            System.out.print("Choisissez une option: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Entrer l'ID: ");
                    int managerId = scanner.nextInt();
                    scanner.nextLine(); // Consommer la nouvelle ligne

                    System.out.print("Entrer le nom: ");
                    String managerName = scanner.nextLine();

                    System.out.print("Entrer le poste: ");
                    String managerPosition = scanner.nextLine();

                    System.out.print("Entrer le salaire: ");
                    double managerSalary = scanner.nextDouble();

                    System.out.print("Nombre de personnes gérées: ");
                    int numberOfPeople = scanner.nextInt();

                    Manager newManager = new Manager(managerId, managerName, managerPosition, managerSalary, numberOfPeople);
                    manager.addEmployee(newManager);
                    break;

                case 2:
                    System.out.print("Entrer l'ID: ");
                    int developerId = scanner.nextInt();
                    scanner.nextLine(); // Consommer la nouvelle ligne

                    System.out.print("Entrer le nom: ");
                    String developerName = scanner.nextLine();

                    System.out.print("Entrer le poste: ");
                    String developerPosition = scanner.nextLine();

                    System.out.print("Entrer le salaire: ");
                    double developerSalary = scanner.nextDouble();
                    scanner.nextLine(); // Consommer la nouvelle ligne

                    System.out.print("Langage de programmation: ");
                    String programmingLanguage = scanner.nextLine();

                    Developer newDeveloper = new Developer(developerId, developerName, developerPosition, developerSalary, programmingLanguage);
                    manager.addEmployee(newDeveloper);
                    break;

                case 3:
                    System.out.print("Entrer l'ID de l'employé à supprimer: ");
                    int removeId = scanner.nextInt();
                    manager.removeEmployee(removeId);
                    break;

                case 4:
                    manager.displayAllEmployees();
                    break;

                case 5:
                    System.out.print("Entrer l'ID de l'employé à afficher: ");
                    int displayId = scanner.nextInt();
                    manager.displayEmployee(displayId);
                    break;

                case 6:
                    System.out.print("Entrer l'ID de l'employé à mettre à jour: ");
                    int updateId = scanner.nextInt();
                    manager.updateEmployee(updateId);
                    break;

                case 7:
                    System.out.println("Quitter le programme...");
                    break;

                default:
                    System.out.println("Option invalide! Veuillez réessayer.");
            }
        } while (choice != 7);

        scanner.close();
    }
}
```

### Explication

1. **Méthode `updateEmployee`** : Cette méthode permet de rechercher un employé par ID et de mettre à jour ses informations. Selon le type d'employé (Manager ou Developer), des options spécifiques sont proposées.
2. **Interface `EmployeeOperations`** : La méthode `updateEmployee` a été ajoutée à l'interface pour garantir que toutes les classes qui implémentent cette interface fournissent une implémentation pour la mise à jour des employés.
3. **Classe `Main`** : Une nouvelle option de mise à jour a été ajoutée au menu, permettant à l'utilisateur de choisir de mettre à jour un employé par ID.

### Comment utiliser

Compilez tous les fichiers Java et exécutez la classe `Main`. Le programme vous guidera à travers le menu pour ajouter, supprimer, afficher ou mettre à jour les employés de l'entreprise.
