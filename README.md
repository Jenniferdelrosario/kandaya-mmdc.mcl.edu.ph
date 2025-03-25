class Employee:
    def __init__(self, emp_id, name, basic_salary, hourly_rate):
        self.emp_id = emp_id
        self.name = name
        self.basic_salary = basic_salary
        self.hourly_rate = hourly_rate
        self.work_hours = []

    def add_work_hours(self, date, login, logout):
        hours_worked = max(0, (logout - login).total_seconds() / 3600)  # Convert seconds to hours
        self.work_hours.append((date, hours_worked))

    def calculate_weekly_salary(self):
        total_hours = sum(hours for _, hours in self.work_hours)
        gross_salary = total_hours * self.hourly_rate
        return round(gross_salary, 2)

    def calculate_deductions(self, sss_rate=500, philhealth_rate=300, pagibig_rate=200, tax_rate=0.1):
        sss = sss_rate
        philhealth = philhealth_rate
        pagibig = pagibig_rate
        tax = tax_rate * self.calculate_weekly_salary()
        total_deductions = sss + philhealth + pagibig + tax
        return {"SSS": round(sss, 2), "PhilHealth": round(philhealth, 2), "Pag-IBIG": round(pagibig, 2), "Tax": round(tax, 2), "Total": round(total_deductions, 2)}

    def calculate_net_salary(self):
        return round(self.calculate_weekly_salary() - self.calculate_deductions()["Total"], 2)

    def display_summary(self):
        print(f"Employee: {self.name} ({self.emp_id})")
        print(f"Gross Weekly Salary: PHP {self.calculate_weekly_salary():,.2f}")
        print("Deductions:")
        for key, value in self.calculate_deductions().items():
            print(f"  {key}: PHP {value:,.2f}")
        print(f"Net Weekly Salary: PHP {self.calculate_net_salary():,.2f}")

# Example Usage
from datetime import datetime

# Employee instance
eduard = Employee(10005, "Eduard Hernandez", 52670, 313.51)

# Add work hours
eduard.add_work_hours("06/03/2024", datetime(2024, 6, 3, 9, 48), datetime(2024, 6, 3, 17, 13))
eduard.add_work_hours("06/04/2024", datetime(2024, 6, 4, 9, 50), datetime(2024, 6, 4, 20, 20))
eduard.add_work_hours("06/05/2024", datetime(2024, 6, 5, 9, 10), datetime(2024, 6, 5, 17, 17))

# Display summary
eduard.display_summary()
