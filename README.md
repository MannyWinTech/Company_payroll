#include <iostream>
#include <iomanip>
#include <fstream>
using namespace std;

//Function Prototypes
void getEmployeeData(int[], int[], double[], int);
void calcPay(int empID[], int hours[],double pay_rate[], double wages[], int Numemp);


//Main
int main()
{
	cout << "*** Welcome to Employee Payroll System ***" << endl;
	const int Numemp = 7;
	int empID[Numemp] = { 565882045, 4520125, 7895122, 8777542,
	845277, 1302850, 7580489 };

	int hours[Numemp];
	double pay_rate[Numemp];
	double wages[Numemp];
	ofstream backupFile;
	backupFile.open("PayrollDataBackup.txt");

	getEmployeeData(empID, hours, pay_rate, Numemp);
	calcPay(empID, hours, pay_rate, wages, Numemp);

	for (int i = 0; i < Numemp; i++)
	{
		cout << fixed << showpoint << setprecision(2); //Ensure a .00 decimal point for currancy
		cout << "_______________________________________________\n";
		cout << " Employee # " << empID[i] << "\n";
		cout << " Pay Rate = $" << pay_rate[i] << " ^^^ Hours Worked = " << hours[i] << endl;
		cout << " Gross Pay = $" << wages[i] << endl;
		cout << "_______________________________________________\n";
		backupFile << empID[i] << " " << hours[i] << " " << pay_rate[i] << " " << endl;
	}

	backupFile.close();

	system("pause");
	return 0;
}

//Function to getEmployeeData from the user
void getEmployeeData(int empID[], int hours[], double payRate[], int Numemp)
{
	for (int i = 0; i < Numemp; i++)
	{
		cout << "Enter hours for Employee # " << empID[i] << ": ";
		cin >> hours[i];
		while (hours[i] <= 0)//Validate input
		{
			cout << "Hours can't be negative!!\n"
				<< "Enter hours for Employee # " << empID[i] << ": ";
			cin >> hours[i];
		}
		cout << "Enter pay rate for Employee # " << empID[i] << ": $";
		cin >> payRate[i];
		while (payRate[i] < 15.00)//Validate input
		{
			cout << "Nobody makes less than $15.00!!\n"
				<< "Enter pay rate for Employee # " << empID[i] << ": $";
			cin >> payRate[i];
		}
		cout << "\n";
	}

}


// Function to calculate the pay
void calcPay(int empID[], int hours[], double payRate[], double wages[], int Numemp)
{
	for (int i = 0; i < Numemp; i++)
	{
		wages[i] = hours[i] * payRate[i];
	}
};
