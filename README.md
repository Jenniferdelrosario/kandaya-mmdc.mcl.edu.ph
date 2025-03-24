# Employee Details
employee = {
    "name": "Hernandez Eduard",
    "employee_no": 10005,
    "hourly_rate": 313.51
}

# Number of days worked (Example input)
days_worked = 5  # Change as needed

# Weekly Salary Calculation
weekly_salary = 0
day = 0
while day < days_worked:
    weekly_salary += employee["hourly_rate"]
    day += 1

print(f"Employee: {employee['name']} (ID: {employee['employee_no']})")
print(f"Weekly Salary: PHP {weekly_salary:.2f}\n")

# Deductions Calculation
deductions = {
    "SSS": 0.045 * weekly_salary,  # Example 4.5% deduction
    "PhilHealth": 0.03 * weekly_salary,  # Example 3% deduction
    "PagIBIG": 100,  # Fixed contribution
    "Withholding Tax": 0.10 * weekly_salary  # Example 10% tax
}

total_deductions = 0
print("Deductions:")
for key, value in deductions.items():
    print(f"{key}: PHP {value:.2f}")
    total_deductions += value

net_salary = weekly_salary - total_deductions
print(f"\nNet Salary: PHP {net_salary:.2f}")
