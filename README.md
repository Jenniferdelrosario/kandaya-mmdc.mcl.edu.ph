import java.time.Duration;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Employee {
    private int empId;
    private String name;
    private double basicSalary;
    private double hourlyRate;
    private List<WorkHours> workHours;

    public Employee(int empId, String name, double basicSalary, double hourlyRate) {
        this.empId = empId;
        this.name = name;
        this.basicSalary = basicSalary;
        this.hourlyRate = hourlyRate;
        this.workHours = new ArrayList<>();
    }

    public void addWorkHours(String date, LocalDateTime login, LocalDateTime logout) {
        double hoursWorked = Math.max(0, Duration.between(login, logout).toMinutes() / 60.0);
        workHours.add(new WorkHours(LocalDate.parse(date), hoursWorked));
    }

    public double calculateWeeklySalary() {
        double totalHours = workHours.stream().mapToDouble(WorkHours::getHoursWorked).sum();
        return Math.round(totalHours * hourlyRate * 100.0) / 100.0;
    }

    public Map<String, Double> calculateDeductions(double sssRate, double philhealthRate, double pagibigRate, double taxRate) {
        double sss = sssRate;
        double philhealth = philhealthRate;
        double pagibig = pagibigRate;
        double tax = taxRate * calculateWeeklySalary();
        double totalDeductions = sss + philhealth + pagibig + tax;

        Map<String, Double> deductions = new HashMap<>();
        deductions.put("SSS", Math.round(sss * 100.0) / 100.0);
        deductions.put("PhilHealth", Math.round(philhealth * 100.0) / 100.0);
        deductions.put("Pag-IBIG", Math.round(pagibig * 100.0) / 100.0);
        deductions.put("Tax", Math.round(tax * 100.0) / 100.0);
        deductions.put("Total", Math.round(totalDeductions * 100.0) / 100.0);
        return deductions;
    }

    public double calculateNetSalary() {
        return Math.round((calculateWeeklySalary() - calculateDeductions(500, 300, 200, 0.1).get("Total")) * 100.0) / 100.0;
    }

    public void displaySummary() {
        System.out.println("Employee: " + name + " (" + empId + ")");
        System.out.printf("Gross Weekly Salary: PHP %.2f%n", calculateWeeklySalary());
        System.out.println("Deductions:");
        for (Map.Entry<String, Double> entry : calculateDeductions(500, 300, 200, 0.1).entrySet()) {
            System.out.printf("  %s: PHP %.2f%n", entry.getKey(), entry.getValue());
        }
        System.out.printf("Net Weekly Salary: PHP %.2f%n", calculateNetSalary());
    }
}

class WorkHours {
    private LocalDate date;
    private double hoursWorked;

    public WorkHours(LocalDate date, double hoursWorked) {
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public double getHoursWorked() {
        return hoursWorked;
    }
}

public class PayrollSystem {
    public static void main(String[] args) {
        Employee eduard = new Employee(10005, "Eduard Hernandez", 52670, 313.51);

        eduard.addWorkHours("2024-06-03", LocalDateTime.of(2024, 6, 3, 9, 48), LocalDateTime.of(2024, 6, 3, 17, 13));
        eduard.addWorkHours("2024-06-04", LocalDateTime.of(2024, 6, 4, 9, 50), LocalDateTime.of(2024, 6, 4, 20, 20));
        eduard.addWorkHours("2024-06-05", LocalDateTime.of(2024, 6, 5, 9, 10), LocalDateTime.of(2024, 6, 5, 17, 17));

        eduard.displaySummary();
    }
}
