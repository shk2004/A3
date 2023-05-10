# A3


import tkinter as tk
import pickle

class Employee:
    def __init__(self, id_number, name, department, job_title, basic_salary):
        self.id_number = id_number
        self.name = name
        self.department = department
        self.job_title = job_title
        self.basic_salary = basic_salary

class Car:
    def __init__(self, id_number, name, price, car_type):
        self.id_number = id_number
        self.name = name
        self.price = price
        self.car_type = car_type

class Sales:
    def __init__(self, employee_id, car_name, sale_price):
        self.employee_id = employee_id
        self.car_name = car_name
        self.sale_price = sale_price

class Company:
    def __init__(self):
        self.employees = []
        self.cars = []
        self.sales = []

    def add_employee(self, employee):
        self.employees.append(employee)

    def add_car(self, car):
        self.cars.append(car)

    def add_sale(self, sale):
        self.sales.append(sale)

    def get_employee_details(self, id_number):
        for employee in self.employees:
            if employee.id_number == id_number:
                return employee.__dict__
        return None

    def get_car_details(self, id_number):
        for car in self.cars:
            if car.id_number == id_number:
                return car.__dict__
        return None

    def get_employee_sales_details(self, id_number):
        sales_details = []
        for sale in self.sales:
            if sale.employee_id == id_number:
                sales_details.append(sale.__dict__)
        return sales_details

    def calculate_salaries(self):
        salaries = {}
        for sale in self.sales:
            salesperson_share = sale.sale_price * 0.065
            manager_share = sale.sale_price * 0.035
            company_share = sale.sale_price - salesperson_share - manager_share
            if sale.employee_id in salaries:
                salaries[sale.employee_id] += salesperson_share
            else:
                salaries[sale.employee_id] = salesperson_share
            for employee in self.employees:
                if employee.job_title == "Manager":
                    if employee.id_number == sale.employee_id:
                        if employee.id_number in salaries:
                            salaries[employee.id_number] += manager_share
                        else:
                            salaries[employee.id_number] = manager_share
        return salaries

class GUI:
    def __init__(self):
        self.company = Company()

        self.root = tk.Tk()
        self.root.geometry("600x400")
        self.root.title("B&M Company Management System")

        tk.Label(self.root, text="Employee Details").grid(row=0, column=0, pady=10)
        tk.Label(self.root, text="ID Number").grid(row=1, column=0)
        self.employee_id_entry = tk.Entry(self.root)
        self.employee_id_entry.grid(row=1, column=1)
        tk.Label(self.root, text="Name").grid(row=2, column=0)
        self.name_entry = tk.Entry(self.root)
        self.name_entry.grid(row=2, column=1)
        tk.Label(self.root, text="Department").grid(row=3, column=0)
        self
