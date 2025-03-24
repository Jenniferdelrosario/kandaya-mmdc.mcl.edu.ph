# Payroll Calculation 

# Constants for deduction rates
SSS_RATE = 0.04
PHILHEALTH_RATE = 0.02
PAGIBIG_RATE = 0.01
WITHHOLDING_TAX_RATE = 0.10

def calculate_deductions(salary):
    """Calculate deductions based on given salary."""
    sss = salary * SSS_RATE
    philhealth = salary * PHILHEALTH_RATE
    pagibig = salary * PAGIBIG_RATE
    withholding_tax = salary * WITHHOLDING_TAX_RATE
    total = sss + philhealth + pagibig + withholding_tax
    return round(sss, 2), round(philhealth, 2), round(pagibig, 2), round(withholding_tax, 2), round(total, 2)

def calculate_salary(employee):
    """Compute weekly salary, deductions, and net salary."""
    weekly_salary = employee["daily_rate"] * employee["days_worked"]
    sss, philhealth, pagibig, withholding_tax, total_deductions = calculate_deductions(weekly_salary)
    net_salary = round(weekly_salary - total_deductions, 2)
    
    print(f"Employee: {employee['name']} ({employee['employee_no']})")
    print(f"Weekly Salary: PHP {weekly_salary:.2f}")
    print(f"SSS Deduction: PHP {sss:.2f}")
    print(f"PhilHealth Deduction: PHP {philhealth:.2f}")
    print(f"Pag-IBIG Deduction: PHP {pagibig:.2f}")
    print(f"Withholding Tax: PHP {withholding_tax:.2f}")
    print(f"Total Deductions: PHP {total_deductions:.2f}")
    print(f"Net Salary: PHP {net_salary:.2f}")

employee = {
    "name": "Eduard",
    "employee_no": 1,
    "daily_rate": 500,
    "days_worked": 5 
}

# Calculate and display salary details
calculate_salary(employee)
