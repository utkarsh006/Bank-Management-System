

//================================================================
//                   HEADER FILES USED IN THIS PROJECT
//================================================================

#include<iostream>
#include<fstream>
#include<cctype>
#include<iomanip>
using namespace std;

//================================================================
//                   CLASS USED IN THIS PROJECT
//================================================================


class account
{
	int acno;
	char name[100];
	int deposit;
	char actype;

public:	void create_account();	//function to fetch data from the user
	    void deposit_amount(int);	//function to deosit the amount
	    void withdraw_amount(int);	//function to withdraw the amount
		void show_account() const;	//function to diplay the data on screen
	    void record() const;	//function to show data in tabular format
		void update();	//function to modify the data
	    int retacno() const;	//function to return account number
	    int retdeposit() const;	//function to return balance amount
	    char rettype() const;	//function to return the account type
};       

void account::create_account()
{
	cout<<"============ Fill the form given below ============";
	cout<<"\n\nEnter the account No. :";
	cin>>acno;
	cout<<"\nEnter Account Holder name : ";
	cin.ignore();
	cin.getline(name,100);
	cout<<"\nEnter your Account Type (C:CURRENT ACCOUNT, S:SAVING ACCOUNT (C/S) : ";
	cin>>actype;
	actype=toupper(actype);
	cout<<"\nEnter The Initial amount(>=500 for Saving Account and >=1000 for Current Account) : ";
	cin>>deposit;
	cout<<"\n\n-> Your Account has been created successfully.You can now continue your transactions...";
	cout<<"\n!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Thank You !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!";
}

void account::show_account() const
{
	cout<<"============ Account Holder Details ============";
	cout<<"\nAccount No. : "<<acno;
	cout<<"\nAccount Holder Name : ";
	cout<<name;
	cout<<"\nType of Account : "<<actype;
	cout<<"\n Total Balance amount : "<<deposit;
	cout<<"\n\n******************************";
}


void account::update()
{
	cout<<"====== FILL THE FORM BELOW TO UPDATE YOUR ACCOUNT ======";
	cout<<"\n Enter the Account No. : "<<acno;
	cout<<"\n Update the Account Holder Name : ";
	cin.ignore();
	cin.getline(name,100);
	cout<<"\n Update the account type : ";
	cin>>actype;
	actype=toupper(actype);
	cout<<"\n Update the Balance amount : ";
	cin>>deposit;
}

	
void account::deposit_amount(int a)
{
	deposit+=a;
}
	
void account::withdraw_amount(int a)
{
	deposit-=a;
}
	
void account::record() const
{
	cout<<acno<<setw(10)<<" "<<name<<setw(15)<<" "<<actype<<setw(8)<<deposit<<endl;
}

	
int account::retacno() const
{
	return acno;
}

int account::retdeposit() const
{
	return deposit;
}

char account::rettype() const
{
	return actype;
}


//================================================================
//    	  DECLARATION OF FUNCTIONS
//================================================================
void write_account();	//function to write record in binary file
void display_details(int);	//function to display account details given by user
void modify_account(int);	//function to modify record of the file
void delete_account(int);	//function to delete record of the file
void display_all();		//function to display all account details
void deposit_withdraw(int, int); // function to desposit/withdraw amount 
void introduction();	//function to introductory screen

//================================================================
//    	   MAIN FUNCTION
//=================================================================


int main()
{
	char ch;
	int no;
	introduction();
	do
	{
		system("cls");
		cout<<"\n\n\n\t====== MAIN MENU ======";
		cout<<"\n\n\t-> 01. NEW ACCOUNT";
		cout<<"\n\n\t-> 02. DEPOSIT AMOUNT";
		cout<<"\n\n\t-> 03. WITHDRAW AMOUNT";
		cout<<"\n\n\t-> 04. BALANCE ENQUIRY";
		cout<<"\n\n\t-> 05. ALL ACCOUNT HOLDER LIST";
		cout<<"\n\n\t-> 06. CLOSE AN ACCOUNT";
		cout<<"\n\n\t-> 07. UPDATE AN ACCOUNT";
		cout<<"\n\n\t-> 08. EXIT !!!";
		cout<<"\n\n\tSelect Your Option (1-8): ";
		cin>>ch;
		system("cls");
		switch(ch)
		{
		case '1':
			write_account();
			break;
		case '2':
			cout<<"\n\n\tEnter the account No. : "; cin>>no;
			deposit_withdraw(no, 1);
			break;
		case '3':
			cout<<"\n\n\tEnter The account No. : "; cin>>no;
			deposit_withdraw(no, 2);
			break;
		case '4': 
			cout<<"\n\n\tEnter The account No. : "; cin>>no;
			display_details(no);
			break;
		case '5':
			display_all();
			break;
		case '6':
			cout<<"\n\n\tEnter The account No. : "; cin>>no;
			delete_account(no);
			break;
		 case '7':
			cout<<"\n\n\tEnter The account No. : "; cin>>no;
			modify_account(no);
			break;
		 case '8':
			cout<<"\n\n\t!!!!!!!!!! Thanks for visiting !!!!!!!!!!";
			break;
		 default :cout<<"\a";
		}
		cin.ignore();
		cin.get();
	}while(ch!='8');
	return 0;
}


//================================================================
//    	function to write in file
//================================================================

void write_account()
{
	account ac;
	ofstream outFile;
	outFile.open("account.dat",ios::binary|ios::app);
	ac.create_account();
	outFile.write(reinterpret_cast<char *> (&ac), sizeof(account));
	outFile.close();
}

//===============================================================
//    	function to read specific record from file
//================================================================

void display_details(int x)
{
	account d;
	bool flag=false;
	ifstream inFile;
	inFile.open("account.dat",ios::binary);
	if(!inFile)
	{
		cout<<"Unable to open the file ! Press any key to continue...";
		return;
	}
	cout<<"\n========== Account Holder Details ==========\n";

    	while(inFile.read(reinterpret_cast<char *> (&d), sizeof(account)))
	{
		if(d.retacno()==x)
		{
			d.show_account();
			flag=true;
		}
	}
	inFile.close();
	if(flag==false)
		cout<<"\n\n SORRY YOU HAVE ENTERED THE WRONG ACCOUNT NUMBER !!!";
}


//================================================================
//    	function to modify record of file
//================================================================

void modify_account(int x)
{
	bool found=false;
	account m;
	fstream File;
	File.open("account.dat",ios::binary|ios::in|ios::out);
	if(!File)
	{
		cout<<"Unable to open the file ! Press any Key to Continue...";
		return;
	}
	while(!File.eof() && found==false)
	{
		File.read(reinterpret_cast<char *> (&m), sizeof(account));
		if(m.retacno()==x)
		{
			m.show_account();
			cout<<"\n\n===== Enter The New Details of account ====="<<endl;
			m.update();
			int pos=(-1)*static_cast<int>(sizeof(account));
			File.seekp(pos,ios::cur);
			File.write(reinterpret_cast<char *> (&m), sizeof(account));
			cout<<"\n\n\t Your record is updated sucessfully !!!";
			found=true;
		  }
	}
	File.close();
	if(found==false)
		cout<<"\n\n Record Not Found ";
}

//===============================================================
//    	function to delete record of file
//===============================================================


void delete_account(int x)
{
	account dac;
	ifstream inFile;
	ofstream outFile;
	inFile.open("account.dat",ios::binary);
	if(!inFile)
	{
		cout<<"Unable to open the file! Press any Key Continue...";
		return;
	}
	outFile.open("Temp.dat",ios::binary);
	inFile.seekg(0,ios::beg);
	while(inFile.read(reinterpret_cast<char *> (&dac), sizeof(account)))
	{
		if(dac.retacno()!=x)
		{
			outFile.write(reinterpret_cast<char *> (&dac), sizeof(account));
		}
	}
	inFile.close();
	outFile.close();
	remove("account.dat");
	rename("Temp.dat","account.dat");
	cout<<"\n\n\t Your reord is successfully deleted !!!";
}

//===============================================================
//    	function to display all accounts deposit list
//===============================================================

void display_all()
{
	account dall;
	ifstream inFile;
	inFile.open("account.dat",ios::binary);
	if(!inFile)
	{
		cout<<"Unable to open the file ! Press any Key to Continue...";
		return;
	}
	cout<<"\n\n\t\tACCOUNT HOLDER LIST\n\n";
	cout<<"====================================================\n";
	cout<<"A/c no.      NAME           ACC.TYPE  BALANCE\n";
	cout<<"====================================================\n";
	while(inFile.read(reinterpret_cast<char *> (&dall), sizeof(account)))
	{
		dall.record();
	}
	inFile.close();
}

//===============================================================
//    	function to deposit and withdraw amounts
//===============================================================

void deposit_withdraw(int x, int option)
{
	int amt;
	bool found=false;
	account dw;
	fstream File;
	File.open("account.dat", ios::binary|ios::in|ios::out);
	if(!File)
	{
		cout<<"Unable to open the file ! Press any Key Continue...";
		return;
	}
	while(!File.eof() && found==false)
	{
		File.read(reinterpret_cast<char *> (&dw), sizeof(account));
		if(dw.retacno()==x)
		{
			dw.show_account();
			if(option==1)
			{
				cout<<"\n\n\t====== DEPOSIT AMOUNT ====== ";
				cout<<"\n\nEnter The amount to be deposited : ";
				cin>>amt;
				dw.deposit_amount(amt);
			}
			if(option==2)
			{
				cout<<"\n\n\t====== WITHDRAW AMOUNT =======";
				cout<<"\n\nEnter The amount to be withdrawn : ";
				cin>>amt;
				int bal=dw.retdeposit()-amt;
				if((bal<500 && dw.rettype()=='S') || (bal<1000 && dw.rettype()=='C'))
					cout<<"SORRY !!! Amount Can't be withdrawn !!";
				else
					dw.withdraw_amount(amt);
			}
			int pos=(-1)*static_cast<int>(sizeof(dw));
			File.seekp(pos,ios::cur);
			File.write(reinterpret_cast<char *> (&dw), sizeof(account));
			cout<<"\n\n\t Your Record Has been updated successfully";
			found=true;
	       }
         }
	File.close();
	if(found==false)
		cout<<"\n\n Record Not Found ";
}


//===============================================================
//    	INTRODUCTION FUNCTION
//===============================================================


void introduction()
{
	cout<<"\n\n\n\t  BANK";
	cout<<"\n\n\tMANAGEMENT";
	cout<<"\n\n\t  SYSTEM";
	cout<<"\n\n\n\nMADE BY : UTKARSH SAXENA  NISHKARSH SAXENA";
    cin.get();
}

//===============================================================
//    			END OF PROJECT
//===============================================================
