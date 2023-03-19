import java.util.Random;
public class Employee {
    private String firstName;
    private String lastName;
    private String email;
    private String password;
    public Employee(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = "";
        this.password = "";
    }
    public String getFirstName() {
        return firstName;
    }
    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }
    public String getLastName() {
        return lastName;
    }
    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
}
public class CredentialService {
    private static final String[] DEPARTMENTS = {"Technical", "Admin", "Human Resource", "Legal"};
    public static String generatePassword() {
        String capitalLetters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String smallLetters = "abcdefghijklmnopqrstuvwxyz";
        String numbers = "0123456789";
        String specialCharacters = "!@#$%^&*_=+-/";
        String allCharacters = capitalLetters + smallLetters + numbers + specialCharacters;
        Random random = new Random();
        StringBuilder password = new StringBuilder();
        password.append(capitalLetters.charAt(random.nextInt(capitalLetters.length())));
        password.append(smallLetters.charAt(random.nextInt(smallLetters.length())));
        password.append(numbers.charAt(random.nextInt(numbers.length())));
        password.append(specialCharacters.charAt(random.nextInt(specialCharacters.length())));
        for (int i = 4; i < 10; i++) {
            password.append(allCharacters.charAt(random.nextInt(allCharacters.length())));
        }
        return password.toString();
    }
    public static String generateEmailAddress(String firstName, String lastName, String department) {
        return firstName.toLowerCase() + lastName.toLowerCase() + "@" + department.toLowerCase() + ".company.com";
    }
    public static void showCredentials(Employee employee, String department) {
        String password = generatePassword();
        String email = generateEmailAddress(employee.getFirstName(), employee.getLastName(), department);
        System.out.println("Dear " + employee.getFirstName() + " your generated credentials are as follows");
        System.out.println("Email ---> " + email);
        System.out.println("Password ---> " + password);
        employee.setEmail(email);
        employee.setPassword(password);
    }
}
public class Main {
    public static void main(String[] args) {
        System.out.println("Please enter the department from the following:");
        for (int i = 0; i < CredentialService.DEPARTMENTS.length; i++) {
            System.out.println((i+1) + ". " + CredentialService.DEPARTMENTS[i]);
        }
        int choice = Integer.parseInt(System.console().readLine());
        Employee employee = new Employee("Harshit", "Choudary");
        CredentialService.showCredentials(employee, CredentialService.DEPARTMENTS[choice-1]);
    }
}