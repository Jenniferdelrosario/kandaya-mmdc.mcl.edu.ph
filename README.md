# Employee details (from motorph sheet)
employee = {
    "name": "Eduard",
    "employee_no": 1,
    "daily_rate": 500
    "days_worked": 5
}

# Time Calculations - Weekly Salary
weekly_salary = employee["daily_rate"] * employee["days_worked"]
print(f"Employee: {employee['name']} ({employee['employee_no']})")
print(f"Weekly Salary: PHP {weekly_salary}")

# SSS Deduction (Example: 4% of weekly salary)
sss_deduction = weekly_salary * 0.04
print(f"SSS Deduction: PHP {sss_deduction}")

# PhilHealth Deduction (Example: 2% of weekly salary)
philhealth_deduction = weekly_salary * 0.02
print(f"PhilHealth Deduction: PHP {philhealth_deduction}")

# Pag-IBIG Deduction (Example: 1% of weekly salary)
pagibig_deduction = weekly_salary * 0.01
print(f"Pag-IBIG Deduction: PHP {pagibig_deduction}")

# Withholding Tax (Example: 10% of weekly salary)
withholding_tax = weekly_salary * 0.10
print(f"Withholding Tax: PHP {withholding_tax}")

# Total Deductions and Net Salary
total_deductions = sss_deduction + philhealth_deduction + pagibig_deduction + withholding_tax
net_salary = weekly_salary - total_deductions
print(f"Total Deductions: PHP {total_deductions}")
print(f"Net Salary: PHP {net_salary}")
