# Payroll-Project
//
//  main.cpp
//  m11
//
//  Created by Aikerim Daniiar kyzy on 7/20/18.
//  Copyright © 2018 Aikerim Daniiar kyzy. All rights reserved.
//

#include <iostream>
#include <iomanip>
using namespace std;
class payroll
{char employeessn[100];char firstname[100];char lastname[100];int hoursworked, overtime, i;
    double hourlyrate, overtimepay, overtimepaycalc, taxrate, regpay, grosspay, taxamount, netpay;
    void calculategrosspay();
    void calculatetaxamount();
    void calculatenetpay();
    void calculateaveragepay();
    static int numEmp;
public: void printheadings();
    void printdata();
    static double averagepay;
    static double sum;
    public: payroll();
    void printreport();};

    double payroll::averagepay = 0.0;
double payroll::sum = 0.0;
int payroll::numEmp = 0;payroll::payroll() {
    cout << "First name: " << endl;
    cin >> firstname;cout << "Last name: " << endl;
    cin >> lastname;cout << "First three numbers of employee's ssn: " << endl;
    cin >> employeessn;cout << "Please enter the amount of hours worked: " << endl;
    cin >> hoursworked;cout << "Please enter in the hourly wage: $" << endl;cin >> hourlyrate;}
void payroll::calculategrosspay() {
    grosspay = hoursworked * hourlyrate;
    if (hoursworked>40){overtime = hoursworked - 40;
        regpay = 40 * hourlyrate;
        overtimepaycalc = hourlyrate * 1.5;overtimepay = overtime * overtimepaycalc;
        grosspay = overtimepay + regpay;}
    else{overtime = 0;regpay = 40 * hourlyrate;
        overtimepaycalc = hourlyrate * 1.5;
        overtimepay = overtime * overtimepaycalc;
        grosspay = overtimepay + regpay;}
    
};
void payroll::calculatetaxamount()
{if (grosspay >= 0) taxrate = .30;
    taxamount = grosspay * taxrate;}
void payroll::calculatenetpay() {
    netpay = grosspay - taxamount;}
void payroll::calculateaveragepay()
{sum += netpay;
    averagepay = (sum / numEmp);}
void payroll::printheadings() {cout << setw(45) << "-Aikerim Daniiar's Payroll System-" << endl;
    cout << "----------------------------------------------------------------------------------------------------" << endl;
    cout << "FirstName  LastName   SSN    Hours    Rate   OThours    OTpay    REGpay    GROSSpay   Taxes   NETpay" << endl;
    cout << "=========  ========   ====   =====    ====   =======    =====    ======    ========   =====   ======" << endl;
    cout << "----------------------------------------------------------------------------------------------------" << endl;
    
};
void payroll::printdata()
{cout << setprecision(2) << fixed << left;//setiosflags (ios::fixed | ios::left);
    cout << setw(10) << firstname << setw(10) << lastname << setw(3) << " " << employeessn << setw(4) << " " << hoursworked << setw(5) << " " << hourlyrate << setw(7) << "" << overtime << setw(4) << "" << overtimepay << setw(4) << " " << regpay << setw(4) << " " << grosspay << setw(4) << "" << taxamount << setw(4) <<"" << netpay << endl << endl;}
void payroll::printreport() {
        numEmp++;
        calculategrosspay();
    calculatetaxamount();
    calculatenetpay();
    calculateaveragepay();
    printdata();
    
}
int main(void) {int numEmp;//memory needed for the array
    cout << "Enter the number of Employees: ";
    cin >> numEmp;payroll *employee = new payroll[numEmp];//pointer used with the array
    employee[0].printheadings();
    for (int i = 0; i<numEmp; i++)
    {employee[i].printreport();//to print each employee
        
    }
    cout << "Average Net Pay of all the Employees : $ " << payroll::averagepay<< endl;
    delete[] employee; //frees memory used by array
    system("PAUSE");
    return 0;}


