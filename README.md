Download Link: https://assignmentchef.com/product/solved-payableinterfacetest
<br>
Program in C#Modify the payroll application. If the object currently being processed is a BasePlusCommissionEmployee, the application should increase the BasePlusCommissionEmployee’s base salary by 10%.

Complete the following steps to create the new application:

a) Modify classes HourlyEmployee and CommissionEmployee (Fig. 12.7) to place them in the IPayable hierarchy as derived classes of the version of Employee that implements IPayable. [Hint: Change the name of method Earnings to GetPaymentAmount in each derived class.]b) Modify class BasePlusCommissionEmployee such that it extends the version of class CommissionEmployee created in Part a.c) Modify PayableInterfaceTest to polymorphically process three salariedEmployee, two HourlyEmployee, one CommissionEmployee and two Base- PlusCommissionEmployee.d) Create a menu that allows a user to select one of the following options to display a string representation of each IPayable objects.

Sort last name in descending order using IComparableSort pay amount in ascending order using IComparerSort by social security number in descending order using a selection sort and delegateUse the following data to test your program:

IPayable[] payableObjects = new IPayable[ 8 ];payableObjects[ 0 ] = new SalariedEmployee( “John”, “Smith”, “111-11-1111”, 700M );payableObjects[1] = new SalariedEmployee(“Antonio”, “Smith”, “555-55-5555”, 800M);payableObjects[2] = new SalariedEmployee(“Victor”, “Smith”, “444-44-4444”, 600M);payableObjects[ 3 ] = new HourlyEmployee( “Karen”, “Price”, “222-22-2222”, 16.75M, 40M );payableObjects[4] = new HourlyEmployee(“Ruben”, “Zamora”, “666-66-6666”, 20.00M, 40M);payableObjects[ 5 ] = new CommissionEmployee( “Sue”, “Jones”, “333-33-3333”, 10000M, .06M );payableObjects[ 6 ] = new BasePlusCommissionEmployee( “Bob”, “Lewis”, “777-77-7777”, 5000M, .04M, 300M );payableObjects[7] = new BasePlusCommissionEmployee(“Lee”,”Duarte”, “888-88-888”, 5000M, .04M, 300M);

Return the following documents

– main method– code on sorting by social security number in descending order using selection sort and delegate– code on sorting by last name in descending order– run time output sorting by pay amount in ascending order– UML diagram

public interface IPayable{decimal GetPaymentAmount(); // calculate payment; no implementation} // end interface IPayable_________________________________________public abstract class Employee{// read-only property that gets employee’s first namepublic string FirstName { get; private set; }

// read-only property that gets employee’s last namepublic string LastName { get; private set; }

// read-only property that gets employee’s social security numberpublic string SocialSecurityNumber { get; private set; }

// three-parameter constructorpublic Employee( string first, string last, string ssn ){FirstName = first;LastName = last;SocialSecurityNumber = ssn;} // end three-parameter Employee constructor

// return string representation of Employee object, using propertiespublic override string ToString(){return string.Format( “{0} {1}
social security number: {2}”,FirstName, LastName, SocialSecurityNumber );} // end method ToString

} // end abstract class Employee

__________________________________________________________

public class HourlyEmployee : Employee{private decimal wage; // wage per hourprivate decimal hours; // hours worked for the week

// five-parameter constructorpublic HourlyEmployee( string first, string last, string ssn,decimal hourlyWage, decimal hoursWorked ): base( first, last, ssn ){Wage = hourlyWage; // validate hourly wage via propertyHours = hoursWorked; // validate hours worked via property} // end five-parameter HourlyEmployee constructor

// property that gets and sets hourly employee’s wagepublic decimal Wage{get{return wage;} // end getset{if ( value &gt;= 0 ) // validationwage = value;elsethrow new ArgumentOutOfRangeException( “Wage”,value, “Wage must be &gt;= 0” );} // end set} // end property Wage

// property that gets and sets hourly employee’s hourspublic decimal Hours{get{return hours;} // end getset{if ( value &gt;= 0 &amp;&amp; value &lt;= 168 ) // validationhours = value;elsethrow new ArgumentOutOfRangeException( “Hours”,value, “Hours must be &gt;= 0 and &lt;= 168” );} // end set} // end property Hours

// calculate earnings; override Employee’s abstract method Earningspublic override decimal Earnings(){if ( Hours &lt;= 40 ) // no overtimereturn Wage * Hours;elsereturn ( 40 * Wage ) + ( ( Hours – 40 ) * Wage * 1.5M );} // end method Earnings

// return string representation of HourlyEmployee objectpublic override string ToString(){return string.Format(“hourly employee: {0}
{1}: {2:C}; {3}: {4:F2}”,base.ToString(), “hourly wage”, Wage, “hours worked”, Hours );} // end method ToString} // end class HourlyEmployee_____________________________________________

public class CommissionEmployee : Employee{private decimal grossSales; // gross weekly salesprivate decimal commissionRate; // commission percentage

// five-parameter constructorpublic CommissionEmployee( string first, string last, string ssn,decimal sales, decimal rate ) : base( first, last, ssn ){GrossSales = sales; // validate gross sales via propertyCommissionRate = rate; // validate commission rate via property} // end five-parameter CommissionEmployee constructor

// property that gets and sets commission employee’s gross salespublic decimal GrossSales{get{return grossSales;} // end getset{if ( value &gt;= 0 )grossSales = value;elsethrow new ArgumentOutOfRangeException(“GrossSales”, value, “GrossSales must be &gt;= 0” );} // end set} // end property GrossSales

// property that gets and sets commission employee’s commission ratepublic decimal CommissionRate{get{return commissionRate;} // end getset{if ( value &gt; 0 &amp;&amp; value &lt; 1 )commissionRate = value;elsethrow new ArgumentOutOfRangeException( “CommissionRate”,value, “CommissionRate must be &gt; 0 and &lt; 1” );} // end set} // end property CommissionRate

// calculate earnings; override abstract method Earnings in Employeepublic override decimal Earnings(){return CommissionRate * GrossSales;} // end method Earnings

// return string representation of CommissionEmployee objectpublic override string ToString(){return string.Format( “{0}: {1}
{2}: {3:C}
{4}: {5:F2}”,“commission employee”, base.ToString(),“gross sales”, GrossSales, “commission rate”, CommissionRate );} // end method ToString___________________________________

public class BasePlusCommissionEmployee{private decimal baseSalary; // base salary per week

// six-parameter constructorpublic BasePlusCommissionEmployee( string first, string last,string ssn, decimal sales, decimal rate, decimal salary )

{BaseSalary = salary; // validate base salary via property} // end six-parameter BasePlusCommissionEmployee constructor

// property that gets and sets// base-salaried commission employee’s base salarypublic decimal BaseSalary{get{return baseSalary;} // end getset{if ( value &gt;= 0 )baseSalary = value;elsethrow new ArgumentOutOfRangeException( “BaseSalary”,value, “BaseSalary must be &gt;= 0” );} // end set} // end property BaseSalary

// calculate earnings; override method Earnings in CommissionEmployeepublic override decimal Earnings(){return BaseSalary + base.Earnings();} // end method Earnings

// return string representation of BasePlusCommissionEmployee objectpublic override string ToString(){return string.Format( “base-salaried {0}; base salary: {1:C}”,base.ToString(), BaseSalary );} // end method ToString} // end class BasePlusCommissionEmployee______________________________________________

public class SalariedEmployee : Employee{private decimal weeklySalary;

// four-parameter constructorpublic SalariedEmployee( string first, string last, string ssn,decimal salary ) : base( first, last, ssn ){WeeklySalary = salary; // validate salary via property} // end four-parameter SalariedEmployee constructor

// property that gets and sets salaried employee’s salarypublic decimal WeeklySalary{get{return weeklySalary;} // end getset{if ( value &gt;= 0 ) // validationweeklySalary = value;elsethrow new ArgumentOutOfRangeException( “WeeklySalary”,value, “WeeklySalary must be &gt;= 0” );} // end set} // end property WeeklySalary

// calculate earnings; override abstract method Earnings in Employeepublic override decimal Earnings(){return WeeklySalary;} // end method Earnings

// return string representation of SalariedEmployee objectpublic override string ToString(){return string.Format( “salaried employee: {0}
{1}: {2:C}”,base.ToString(), “weekly salary”, WeeklySalary );} // end method ToString} // end class SalariedEmployee

______________________________________________

public class PayrollSystemTest{public static void Main( string[] args ){// create derived class objectsSalariedEmployee salariedEmployee =new SalariedEmployee( “John”, “Smith”, “111-11-1111”, 800.00M );HourlyEmployee hourlyEmployee =new HourlyEmployee( “Karen”, “Price”,“222-22-2222”, 16.75M, 40.0M );CommissionEmployee commissionEmployee =new CommissionEmployee( “Sue”, “Jones”,“333-33-3333”, 10000.00M, .06M );BasePlusCommissionEmployee basePlusCommissionEmployee =new BasePlusCommissionEmployee( “Bob”, “Lewis”,“444-44-4444”, 5000.00M, .04M, 300.00M );

Console.WriteLine( “Employees processed individually:
” );

Console.WriteLine( “{0}
earned: {1:C}
”,salariedEmployee, salariedEmployee.Earnings() );Console.WriteLine( “{0}
earned: {1:C}
”,hourlyEmployee, hourlyEmployee.Earnings() );Console.WriteLine( “{0}
earned: {1:C}
”,commissionEmployee, commissionEmployee.Earnings() );Console.WriteLine( “{0}
earned: {1:C}
”,basePlusCommissionEmployee,basePlusCommissionEmployee.Earnings() );

// create four-element Employee arrayEmployee[] employees = new Employee[ 4 ];

// initialize array with Employees of derived typesemployees[ 0 ] = salariedEmployee;employees[ 1 ] = hourlyEmployee;employees[ 2 ] = commissionEmployee;employees[ 3 ] = basePlusCommissionEmployee;

Console.WriteLine( “Employees processed polymorphically:
” );

// generically process each element in array employeesforeach ( Employee currentEmployee in employees ){Console.WriteLine( currentEmployee ); // invokes ToString

// determine whether element is a BasePlusCommissionEmployeeif ( currentEmployee is BasePlusCommissionEmployee ){// downcast Employee reference to// BasePlusCommissionEmployee referenceBasePlusCommissionEmployee employee =( BasePlusCommissionEmployee ) currentEmployee;

employee.BaseSalary *= 1.10M;Console.WriteLine(“new base salary with 10% increase is: {0:C}”,employee.BaseSalary );} // end if

Console.WriteLine(“earned {0:C}
”, currentEmployee.Earnings() );} // end foreach

// get type name of each object in employees arrayfor ( int j = 0; j &lt; employees.Length; j++ )Console.WriteLine( “Employee {0} is a {1}”, j,employees[ j ].GetType() );} // end Main} // end class PayrollSystemTest