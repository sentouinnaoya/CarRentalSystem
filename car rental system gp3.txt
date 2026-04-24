#include <iostream>
#include <string>
#include <conio.h>
#include <stdlib.h>
#include <fstream>
#include <iomanip>
#include <unordered_map>
#include <limits>
#include <cstdlib>
#include <cstring>
#include <random>
#include <chrono>
#include <cctype>
#include <regex>
using namespace std;
void userInvoice();
void login1();
void myfunction();
string name;
string rentedCar;
int theChoice;
int input;
void Warning();
 string ans;
 void exitFunction();
 void returnsavedata();
 string getCurrentTime();
 void showrecordedData();
void recordFile();
void returnFunction();
void returnsaveStringToFile(const string &str);
void returnrecordFile();
void returnrecordedFile();
void thankYou();
double totalRentalAmount;
struct Cars{
public:
string company[16]={"MarutiSuzuki", "Volkswagen", "BMW", "Audi", "KIA", "Tesla", "Mercedes", "Mahindra", "TATA", "Toyota",
                     "FordMustang", "ChevroletCamaroZL1", "Porsche", "Lamborghini", "Nissan", "McLaren"
                   };

string model[16]={"Swift", "2020", "X5", "R8", "Seltos", "Model S", "S-Class", "Thar", "Nano", "Highlander", "2024", "2024", "Cayenne",
        "Huracán", "GT-R", "Artura"};

string color[16]={"Yellow","Black","Red","Brown","Blue","Sliver","Balck","Grey","Red","Black","Red","Black","Yellow",
                    "green","Gray","Orange"};

string maxSpeed[16]={"80km", "200km", "300km", "250km", "320km", "400km", "200km", "250km", "280km", "100km", "155km", "198km",
        "205km", "202km", "196km", "212km"};

string companyName[16]={"Maruti Suzuki India Limited","Volkswagen AG","Bayerische Motoren Werke AG","Audi AG","Kia Corporation","Tesla, Inc.",
                  "Mercedes-Benz Group AG","Mahindra & Mahindra Limited","Tata Motors","Toyota Motor Corporation","Ford Motor Company","Chevrolet",
                                     "Dr. Ing. h.c. F. Porsche AG","Automobili Lamborghini S.p.A.","Nissan Motor Co., Ltd.","McLaren Automotive"
    };

int price[21]={ 40, 30, 100, 500, 50, 150, 200, 60, 25, 80, 100, 150, 200, 1000, 300, 800};



}car;

struct LeaseInfo{
    public:
    string name;
    string address[100];
    int paymentAcc[100];
    int numberOfDay;
    string phoneNumber;
}lease;

struct ReturnForm {
    std::string customerName;
    std::string invoiceNumber;
    std::string carName;
}returndata;


bool authenticate2(const string& customerName,  const string& invoiceNumber) {
    ifstream file("output1.txt");
    if (!file.is_open()) {
        cerr << "Unable to open file" << endl;
        return false;
    }

    string storedCustomerName,storedCarName;

    while (file >> storedCustomerName >> storedCarName) {
        if (storedCustomerName == customerName  && storedCarName == invoiceNumber) {
            return true;
        }
    }

    return false;
}



void returnFunction1()
{   cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;

   cout<<"\t\tPlease enter your name and the car name you rented to validate to complete your return form;\n";


    cout << "\t\tEnter your name: ";
    cin >> returndata.customerName;
 cout << "\t\tEnter your invoiceNumber: ";
    cin >> returndata.invoiceNumber;
    cout << "\t\tEnter the car you rented: ";
    cin >> returndata.carName;

    if (authenticate2(returndata.customerName,  returndata.invoiceNumber)) {
        cout << "\t\tIt is confirmed you returned the car. "<< endl;
        void returnsaveStringToFile(const string &str);
 returnrecordFile();
    } else {
        cout << "\t\tThere is no invalid data." << endl;
        returnFunction1();
    }



}
void returnFunction()
{
returnFunction1();
cout<<"Enter 'exit' to exit:";
cin>>ans;
if(ans=="exit")
{
    exitFunction();
}
if(ans=="no"){
    returnFunction1();
}

};

void returnsaveStringToFile(const string &str) {
    static string staticStr ="\n\t\t\t\t\t\t"+returndata.customerName+" returned "+returndata.carName+" at "+getCurrentTime();

    // Save another string to a file
    ofstream outFile("output.txt", ios::app); // Open file in append mode
    if (outFile.is_open()) {
        outFile << staticStr << "\n"; // Write static string to the file
        outFile << str << "\n";       // Write the passed string to the file
        outFile.close();
} else {
        cerr << "Unable to open file." << endl;
    }
}

void returnrecordFile() {
    string newString = "\t\t\t\t\t\t---------------------------------------------";
    returnsaveStringToFile(newString);


}

void returnrecordedFile()
{
    int max=1000;
    char buffer[max];
    ifstream infile("output.txt");
    while(!infile.eof())
    {
        infile.getline(buffer,max);
        cout<<buffer<<endl;
    }
}
void showrecordedData() {
    // File name
   string filename = "output.txt";

    // Open the file in read mode
   ifstream inFile(filename);

    // Check if the file is open
    if (inFile.is_open()) {
        string line;

        // Read the file line by line
        while (getline(inFile, line)) {
            // Display the line
            cout << line << endl;
        }

        // Close the file
        inFile.close();
    } else {
        cerr << "Unable to open file for reading." << endl;
    }


}

void menu()
{
    int index=16;
    int num=1;
    for(int i=0;i<sizeof(car.company)/sizeof(car.company[0]);i++){
        cout<<"\t\t\t";
        cout<<"Enter "<<num<<" "<<"\t- To Select "<<car.company[i]<<endl;
        num++;
    }
}
void details(int Choice)
{

    system("CLS");
    cout<<"\n\n\n\t\t\t----------------------------------------\n";
    cout<<"\t\t\tYou have selected -"<<car.company[Choice-1]<<endl;
    cout<<"\t\t\t--------------------------------------\n\n\n";
    cout<<"\t\t\tModel :"<<car.model[Choice-1]<<endl;
    cout<<"\t\t\tColor :"<<car.color[Choice-1]<<endl;
    cout<<"\t\t\tMaximum Speed :"<<car.maxSpeed[Choice-1]<<endl;
    cout<<"\t\t\tRepresentative company :"<<car.companyName[Choice-1]<<endl;
    cout<<"\t\t\tRental Price : $"<<car.price[Choice-1]<<endl;
}

void checkLease(int k){
string q;
        if(lease.paymentAcc[k]>=totalRentalAmount){

        cout << "\n\n\n\t\t\tProcess has been done successfully!!\n\n" << endl;
userInvoice();
     void saveStringToFile();
                recordFile();
                system("PAUSE");
                system("CLS");
                thankYou();
cout<<"Enter 'exit' to exit:";
cin>>q;
if(q=="exit"){
    exitFunction();
}
        }
        else{
            cout<<"\n\n\n\t\t\tSorry! Not Available. "<<endl;
            cout<<"\n\n\n\t\t\tYour payment is not enough for rent this car. "<<endl;
            cout<<"\n\n\n\t\t\tIs anything can I help?"<<endl;
        }

        }

bool validateUsername(const string& username) {
    // Regular expression to allow only alphanumeric characters (no spaces or special characters)
    regex usernamePattern("^[a-zA-Z0-9]+$");

    // Return true if the username matches the pattern
    return regex_match(username, usernamePattern);
}

// Function to check if a string contains only digits and is of a specific length
bool isValidPhoneNumber(const string& phoneNumber) {
    if (phoneNumber.length() != 10) return false;
    for (char c : phoneNumber) {
        if (!isdigit(c)) {
            return false;
        }
    }
    return true;
}
void userInput(int theChoice)
{
    system("CLS");
    int i;
    int j=theChoice-1;
    cout<<"\t\t\t--------------------------------------------------\n";
    cout<<"\t\t\tPlease Provide Your Personal Details For Invoice: \n";
    cout<<"\t\t\t--------------------------------------------------\n";
    cout<<"\n\n\t\t\t\t\NOTE:PLEASE PROVIDE AND SET USERNAME WITH NO SPACES."<<endl;


 while (true) {
        cout << "\t\t\tEnter your name: ";
        cin >> lease.name;

        if (validateUsername(lease.name)) {
            break; // Exit the loop if the username is valid
        } else {
            cout << "\t\t\tInvalid input: Username should only contain alphanumeric characters. Please try again.\n";
        }
 }
    // Address input (assuming simple validation or none required)
    cout << "\t\t\tEnter Your Address: ";
    cin.ignore();  // To ignore leftover newline character from previous input
    getline(cin, lease.address[j]);


// Phone number validation
    do {
        cout << "\t\t\tEnter Your Phone Number: ";
        cin >> lease.phoneNumber;
        if (!isValidPhoneNumber(lease.phoneNumber)) {
            cout << "\t\t\tInvalid phone number. Please enter a 10-digit phone number without spaces or letters.\n";
        }
    } while (!isValidPhoneNumber(lease.phoneNumber));

    // Number of days validation
    cout << "\t\t\tHow long do you want to rent (in days): ";
   while (!(cin >> lease.numberOfDay) || lease.numberOfDay <= 0) {
        cout << "\t\t\tInvalid input. Please enter a positive number of days.\n";
        cin.clear();  // Clear the error flag
        cin.ignore(numeric_limits<streamsize>::max(), '\n');  // Ignore remaining input
    }

}


void payment(int choice)
{
    system("PAUSE");
    system("CLS");
    int j=choice-1;
    cout<<"-----------------------------------------------------------"<<endl;
    cout<<"\t\t\t\n\tPAYMENT WON'T PROCEED IF THE GIVEN AMOUNT"<<endl;
    cout<<"-----------------------------------------------------------"<<endl;
    cout<<"\n\n\t\t\tPayment Amount : $";
    cin>>lease.paymentAcc[j];
    checkLease(j);

}







bool authenticate(const string& username, const string& password) {
    ifstream file("users.txt");
    if (!file.is_open()) {
        cerr << "Unable to open file" << endl;
        return false;
    }

string storedUsername, storedPassword;
    while (file >> storedUsername >> storedPassword) {
        if (storedUsername == username && storedPassword == password) {
            return true;
        }
    }

    return false;
}
// Function to sign up a user
void signUp(unordered_map<string, string>& users) {

        Warning();
        system("PAUSE");
        system("CLS");
    string username, password;
    cout<<"\n\n\t\t\t\t\tCar Rental System Sign up!"<<endl;
    cout<<"\n\n\t\t\t\t\NOTE:PLEASE PROVIDE AND SET USERNAME WITH NO SPACES."<<endl;
    cout << "\n\n\t\t\t\t\tEnter username: ";
   cin >> username;

    // Check if the username already exists
    if (users.find(username) != users.end()) {
       cout << "Username already exists. Please choose another username." << endl;
        return;
    }

    cout << "\n\n\t\t\t\t\tEnter password: ";
    cin >> password;
    // Store the username and password
    users[username] = password;

    // Save the credentials to a file
    ofstream outFile("users.txt", ios::app);
    if (outFile.is_open()) {
        outFile << username << " " << password << endl;
        outFile.close();
       cout << "User signed up successfully!" << endl;
    } else {
       cout << "Unable to open file to save credentials." <<endl;
    }
}

// Function to load users from file
void loadUsers(unordered_map<string, string>& users) {

    ifstream inFile("users.txt");
    string username, password;

    if (inFile.is_open()) {
        while (inFile >> username >> password) {
            users[username] = password;
        }
        inFile.close();
    } else {
        cout << "Unable to open file to load users." << endl;
    }
}
void exitFunction()
{
        exit(0);
}

string getCurrentTime() {
    auto now = chrono::system_clock::now();
    time_t now_time = chrono::system_clock::to_time_t(now);
    tm local_time = *localtime(&now_time);

    stringstream timeStream;
    timeStream << put_time(&local_time, "%Y-%m-%d %H:%M:%S");

    return timeStream.str();
}
void saveStringToFile(const string &str) {
    static string staticStr ="\n\t\t\t\t\t\t"+lease.name+" rented "+car.company[theChoice-1]+" at "+getCurrentTime();


// Save another string to a file
    ofstream outFile("recorded.txt",ios::app); // Open file in append mode
    if (outFile.is_open()) {
        outFile << staticStr << "\n"; // Write static string to the file
        outFile << str << "\n";       // Write the passed string to the file
        outFile.close();
} else {
        cerr << "Unable to open file." << endl;
    }
}

void recordFile() {
    string newString = "\t\t\t\t\t\t---------------------------------------------";
    saveStringToFile(newString);


}


void recordedFile()
{
    int max=1000;
    char buffer[max];
    ifstream infile("recorded.txt");
    while(!infile.eof())
    {
        infile.getline(buffer,max);
        cout<<buffer<<endl;
    }
}



void showCarDetails(int carIndex, string cars[], string model[], string color[], string maxSpeed[],string companyName[], double newPrices1[], double newPrices2[],
                    double rentalPrice[],
                       double rentalPrice1[16]) {
    system("CLS");

// Clear the console (simulate going to a new page)
    cout << string(0, '\n');
    // Display detailed information about the selected car
    cout << "\n\t\t                   CAR RENTAL SYSTEM - CAR'S DETAILS                " << endl;
    cout << "\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "\t\t   | Car:          \t     | " << cars[carIndex] << "\t\t\t\t\t" << endl;
    cout << "\t\t   | Car Model:    \t     | " << model[carIndex] << "\t\t\t\t\t" << endl;
    cout << "\t\t   | Car Color:    \t     | " << color[carIndex] << "\t\t\t\t\t" << endl;
    cout << "\t\t   | Car Maxspeed: \t     | " << maxSpeed[carIndex] << "\t\t\t\t\t" << endl;
    cout << "\t\t   | Representative company: | " << companyName[carIndex] << "\t\t" << endl;
    cout << "\t\t   | Car's price:  \t     | $" << newPrices1[carIndex] <<"-$"<<newPrices2[carIndex]<< "\t\t\t\t" << endl;
    cout << "\t\t   | Rental price: \t     | $" << rentalPrice[carIndex] <<"-$"<<rentalPrice1[carIndex]<<  "\t\t\t\t\t" << endl;
    cout << "\t\t   | % of rental:  \t     | 20%   \t\t\t\t\t" << endl;
    cout << "\t\t   |____________________________________________________________________|" << endl;


    cout << "\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "\t\t   |NOTE: The prices of these cars are constantly changing.|  " << endl;
    cout << "\t\t   |            So, we are constantly updating the changes.|" << endl;
    cout << "\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "\t\t   | Description:  " << endl;


// Display specific details based on the selected car
    switch (carIndex) {
        case 0:
            cout << "\t\t    Indian manufacturer known for affordable, reliable cars like the Swift and Alto." << endl;
            break;
        case 1:
            cout << "\t\t    German automaker famous for models like the Golf and Passat." << endl;
            break;
        case 2:
            cout << "\t\t    German luxury brand known for performance and quality, with models such as the 3 Series and X5." << endl;
            break;
        case 3:
            cout << "\t\t    German luxury manufacturer offering sleek designs and advanced technology, including the A4 and Q7." << endl;
            break;
        case 4:
            cout << "\t\t    South Korean brand offering stylish and reliable vehicles, such as the Seltos and Stinger." << endl;
            break;
        case 5:
            cout << "\t\t    American electric vehicle pioneer with innovative models like the Model S and Model 3." << endl;
            break;
        case 6:
            cout << "\t\t    German luxury brand known for comfort and safety, with models like the S-Class and G-Class." << endl;
            break;
        case 7:
            cout << "\t\t   Indian manufacturer specializing in rugged SUVs and utility vehicles, such as the Scorpio and Thar." << endl;
            break;
        case 8:
            cout << "\t\t    Indian manufacturer specializing in rugged SUVs and utility vehicles, such as the Scorpio and Thar." << endl;
            break;
        case 9:
            cout << "\t\t    Japanese brand known for reliability and hybrid technology, with popular models like the Corolla and Prius." << endl;
            break;
        case 10:
            cout << "\t\t    Iconic American muscle car with powerful engines and classic design." << endl;
            break;
        case 11:
            cout << "\t\t    High-performance version of the Camaro, known for its supercharged V8 engine." << endl;
            break;
        case 12:
            cout << "\t\t    German sports car manufacturer renowned for performance and precision, with models like the 911 and Panamera." << endl;
            break;
        case 13:
            cout << "\t\t    Italian luxury brand famous for its exotic, high-performance cars, including the Aventador and Huracán." << endl;
            break;
        case 14:
            cout << "\t\t    Japanese manufacturer offering a range of vehicles from economy cars to high-performance models like the GT-R." << endl;
            break;
        case 15:
            cout << "\t\t    British brand known for luxury, high-performancesports cars and supercars, including the 720S and P1." << endl;
            break;
        default:
            cout << "\t\t    No details available for this car." << endl;
            break;

    }
     cout << "\t\t   **************************************************************" << endl;
}

void calculation()
{
        double days = lease.numberOfDay;
    double total= car.price[theChoice-1];
     totalRentalAmount=days*total;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t\tYour rental fee is : "<<totalRentalAmount<<endl;
}

void tPercentcPage() {

    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t\t\t-----------------------------------------------\n";
        cout<<"\t\t\t\t                  CAR RENTAL SYSTEM            \n";
        cout<<"\t\t\t\t     Welcome to our Car Information System:    \n"<<endl;
        cout<<"\t\t\t\t-----------------------------------------------\n";
    // Array of car names
    string cars[16] = {
        "Maruti Suzuki", "Volkswagen", "BMW", "Audi", "KIA", "Tesla", "Mercedes", "Mahindra", "TATA", "Toyota",
        "Ford Mustang", "Chevrolet Camaro ZL1", "Porsche", "Lamborghini", "Nissan", "McLaren"
    };

    string model[16] = {
        "Swift", "2020", "X5", "R8", "Seltos", "Model S", "S-Class", "Thar", "Nano", "Highlander", "2024", "2024", "Cayenne",
        "Huracán", "GT-R", "Artura"
    };

    string color[16] = {
        "Yellow", "Black", "Red", "Brown", "Blue", "Silver", "Black", "Grey", "Red", "Black", "Red", "Black", "Yellow",
        "Green", "Gray", "Orange"
    };


string maxSpeed[16] = {
        "80km", "200km", "300km", "250km", "320km", "400km", "200km", "250km", "280km", "100km", "155km", "198km",
        "205km", "202km", "196km", "212km"
    };
     string companyName[16]={"Maruti Suzuki India Limited","Volkswagen AG","Bayerische Motoren Werke AG","Audi AG","Kia Corporation","Tesla, Inc.",
                  "Mercedes-Benz Group AG","Mahindra & Mahindra Limited","Tata Motors","Toyota Motor Corporation","Ford Motor Company","Chevrolet",
                                     "Dr. Ing. h.c. F. Porsche AG","Automobili Lamborghini S.p.A.","Nissan Motor Co., Ltd.","McLaren Automotive"
    };
    // Array of corresponding car prices
    double newPrices1[16] = {
        15000, 7000, 60000, 150000, 25000, 90000, 110000, 20000, 7000,
        45000, 45000, 70000, 80000, 250000, 115000, 250000
    };
    double newPrices2[16]={
        20000,10000,80000,200000,30000,110000,150000,25000,10000,55000,
        60000.80000,120000,300000,160000,300000};

    double rentalPrice[16] = {
        40, 30, 100, 500, 50, 150, 200, 60, 25, 80, 100, 150, 200, 1000, 300, 800
    };
    double rentalPrice1[16]{
        70,40,200,90,300,400,100,100,40,150,250,300,300,1500,600,1200};

    int choice;

    while (true) {
        // Display the list of cars
        cout << "\t\t\t\t" << "Select a car by its number to see the details:" << endl;
        for (int i = 0; i < 16; i++) {
            cout << "\t\t\t\t" << (i + 1) << ". " << cars[i] << endl;
        }

        // Get the user's choice
        cout << "\t\t\t\t" << "Enter the car number (1-16): ";
        cin >> choice;

        // Check if the choice is within the valid range
        if (choice >= 1 && choice <= 16) {
            // Show the car details
            showCarDetails(choice - 1, cars, model, color, maxSpeed,companyName, newPrices1,newPrices2,rentalPrice, rentalPrice1);

            cout << "\nWould you like to check another car? (y/n): ";
            char another;
            cin >> another;

            if (another != 'y' && another != 'Y') {
                return;
            } else {
                system("CLS");


     cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
                // Clear the console to simulate going back to the car list
                cout << string(0, '\n');
            }
        } else {system("CLS");
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
            cout << "\t\t\tInvalid choice! Please select only a valid car number." << endl;
                           system("PAUSE");
                            system("CLS");
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
    cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t\t-----------------------------------------------\n";
        cout<<"\t\t\t               ***Welcome Back***              \n";
        cout<<"\t\t\t-----------------------------------------------\n";
                // Clear the console to simulate going back to the car list
                cout << string(0, '\n');



        }

    }
}

void Warning() {
    cout<<"\n\n\n\n\n\t\t\t\t\t-------------------------------------------------------------------"<<endl;
    cout<<"\t\t\t\t\t!!!!!!!!!!!!!!!!!!FOLLOW NOTES AND INSTRUCTIONS!!!!!!!!!!!!!!!!!!"<<endl;
    cout<<"\t\t\t\t\t-------------------------------------------------------------------"<<endl;
}



void records() {

    int choice;


while (true) {
        cout << "\n\t\t\t\t\t\t1. Rental Records\n";
        cout << "\n\t\t\t\t\t\t2. Return Records\n";
        cout << "\n\t\t\t\t\t\t3. Exit\n";
        cout << "\n\t\t\t\t\t\tEnter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1:
                 system("CLS");
                cout<<"\n\t\t\t\t\t\t---------------------------------------------------";
                cout<<"\n\t\t\t\t\t\t\t\t*Rental Records*"<<endl;
                cout<<"\t\t\t\t\t\t---------------------------------------------------"<<endl;
                recordedFile();
                system("PAUSE");
                system("CLS");
                break;
            case 2:
               system("CLS");
                cout<<"\n\t\t\t\t\t\t---------------------------------------------------";
                cout<<"\n\t\t\t\t\t\t\t\t*Return Records*"<<endl;
                cout<<"\t\t\t\t\t\t---------------------------------------------------"<<endl;
               returnrecordedFile();
                system("PAUSE");
                system("CLS");
                break;
            case 3:
                 system("CLS");
                 login1();
                 break;

            default:
                std::cout << "Invalid choice, please try again.\n";
        }
    }
}

void thankYou()
{       cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<" ________                                                                              "<<endl;
        cout<<"/        |/  |                          /  |            /  \    /  |                       /  |/  |"<<endl;
        cout<<"$$$$$$$$/ $$ |____    ______   _______  $$ |          $$  \  /$$/______              $$ |$$ |"<<endl;
        cout<<"   $$ |   $$      \  /      \ /       \ $$ |  /  |       $$  \/$$//      \ /  |  /  |      $$ |$$ |"<<endl;
        cout<<"   $$ |   $$$$$$$  | $$$$$$  |$$$$$$$  |$$ |_/$$/         $$  $$//$$$$$$  |$$ |  $$ |      $$ |$$ |"<<endl;
        cout<<"   $$ |   $$ |  $$ | /    $$ |$$ |  $$ |$$   $$<           $$$$/ $$ |  $$ |$$ |  $$ |      $$/ $$/ "<<endl;
        cout<<"   $$ |   $$ |  $$ |/$$$$$$$ |$$ |  $$ |$$$$$$  \           $$ | $$ \__$$ |$$ \__$$ |          "<<endl;
        cout<<"   $$ |   $$ |  $$ |$$    $$ |$$ |  $$ |$$ | $$  |          $$ | $$    $$/ $$    $$/       /  |/  |"<<endl;
        cout<<"   $$/    $$/   $$/  $$$$$$$/ $$/   $$/ $$/   $$/           $$/   $$$$$$/   $$$$$$/        $$/ $$/ "<<endl;

}
void returnMenu()
{
     char decide;
    while(decide != 'y' && decide != 'n'){
        cout << "\n\t\t\t\t\tBack To Menu? (y/n): ";

        cin >> decide;
        if (decide == 'y') {
            system("CLS");
            login1();
        } else if (decide == 'n') {
            cout << "Continue..." << endl;
            system("CLS");
        } else {

            cout << "Invalid input..." << endl;
            system("PAUSE");
            system("CLS");
        }

    }
}
void login1()
{
    system("CLS");


cout<<"              |			                                      __        __                     |"<<endl;
cout<<"              |			  _________ ______   ________  ____  / /_____ _/ /                     |"<<endl;
cout<<"              |			 / ___/ __ `/ ___/  / ___/ _ \\/ __ \\/ __/ __ `/ /                      |"<<endl;
cout<<"              |			/ /__/ /_/ / /     / /  /  __/ / / / /_/ /_/ / /                       |"<<endl;
cout<<"              |			\\___/\\__,_/_/     /_/   \\___/_/ /_/\\__/\\__,_/_/                        |"<<endl;
cout<<"              |			        _______  _______/ /____  ____ ___                              |"<<endl;
cout<<"              |			       / ___/ / / / ___/ __/ _ \\/ __ `__ \\                             |"<<endl;
cout<<"              |			      (__  / /_/ (__  / /_/  __/ / / / / /                             |"<<endl;
cout<<"              |			     /____/\\__, /____/\\__/\\___/_/ /_/ /_/                              |"<<endl;
cout<<"              |			          /____/                                                       |"<<endl;


cout<<"\n\n\n\n\t\t\t\t\t\t1. "<<"Login"<<endl;
    cout<<"\n\t\t\t\t\t\t2. "<<"SignUp"<<endl;
    cout<<"\n\t\t\t\t\t\t3. "<<"Car's Info."<<endl;
    cout<<"\n\t\t\t\t\t\t4. "<<"Return"<<endl;
    cout<<"\n\t\t\t\t\t\t5. "<<"Records"<<endl;
    cout<<"\n\t\t\t\t\t\t6. "<<"Exit"<<endl;
    cout<<endl;
    cout<<endl;
    cout<<"\t\t\t\t\t\Select One:";
    cin>>input;
    if(input==1){
             system("CLS");
        Warning();
        system("PAUSE");
        system("CLS");
        system("CLS");
        int login();
        login();
    }
    if(input==2){
        system("CLS");
            returnMenu();
        system("CLS");
        unordered_map<string, string> users;
        loadUsers(users);
         signUp(users);
    }

    if(input==3){
        system("CLS");
        tPercentcPage();
        system("CLS");
        login1();
    }
    if(input==4){
            system("CLS");
            returnFunction();

    }
    if(input==5){


        system("CLS");
        records();

        login1();
    }
    if(input==6){
       exitFunction();
    }
}
string invoiceNumber()
{


 // Seed the random number generator with the current time
    unsigned seed = chrono::system_clock::now().time_since_epoch().count();
    mt19937 gen(seed); // Mersenne Twister engine with the seed

    // Define the range for a 4-digit number
    uniform_int_distribution<> distr(1000, 9999);

    // Generate and print a 4-digit random number
    int randomNumber = distr(gen);
   string randstring1=to_string(randomNumber);
    string randstring2="#"+randstring1;
    return randstring2;
}
const string string1=invoiceNumber();
void userInvoice()
{
    system("CLS");
    int aChoice=theChoice-1;
    int Choice;
    double rentalAmount = lease.paymentAcc[aChoice];
    double carPrice = car.price[aChoice];
    double remainingBalance = totalRentalAmount - rentalAmount;



    cout<<"\n\t\t                    CAR RENTAL  -  CUSTOMER INVOICE                "<<endl;
            cout<<"\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"<<endl;
            cout<<"\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"<<endl;
            cout<<"\t\t   | Invoice No.  "<<"          |"<<setw(10)<<string1<<"  |"<<endl;
            cout<<"\t\t   | Customer Name  "<<"        |"<<setw(10)<<lease.name<<"  |"<<endl;
            cout<<"\t\t   | Car Model  "<<"            |"<<setw(10)<<car.model[aChoice]<<"  |"<<endl;
            cout<<"\t\t   | Representative company"<<" |"<<setw(10)<<car.companyName[aChoice]<<" |"<<endl;
            cout<<"\t\t   | Car No.  "<<"              |"<<setw(10)<<theChoice<<"  |"<<endl;
            cout<<"\t\t   | Number of days  "<<"       |"<<setw(10)<<lease.numberOfDay<<"  |"<<endl;
            cout<<"\t\t   | Rental Amount  "<<"        |"<<"$"<<setw(10)<<lease.paymentAcc[aChoice]<<" |"<<endl;
            cout<<"\t\t   | Refunds        "<<"        |"<<"$"<<setw(10)<<remainingBalance<<" |"<<endl;
            cout<<"\t\t   | Caution Money  "<<"        |"<<setw(10)<<" 0"<<"  |"<<endl;
            cout<<"\t\t   | Advanced  "<<"             |"<<setw(10)<<" 0"<<"  |"<<endl;
            cout<<"\t\t   | Date      "<<"             |"<<setw(10)<<getCurrentTime()<<"   |"<<endl;
            cout<<"\t\t   |______________________________________________________________|"<<endl;
            cout<<"\t\t   | Total Rental Amount  "<<"  |"<<setw(6)<<totalRentalAmount<<" |"<<endl;
            cout<<"\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"<<endl;
            cout<<"\t\t   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"<<endl;
            cout<<"\t\t   NOTE: This is computer generated invoice. "<<endl;
            cout<<"\t\t         It does not require an authorised signture."<<endl;
            cout<<"\t\t   **************************************************************"<<endl;
            cout<<"\t\t   Take this to fill return form."<<endl;
            cout<<"\t\t   **************************************************************"<<endl;
}
void words()
{
                    cout<<"\n\n\t\t\t\t\t--------------------------------"<<endl;

cout<<"\t\t\t\t\tYour Choice is not been updated."<<endl;
                    cout<<"\t\t\t\t\t--------------------------------"<<endl;
}


void returnsignUp(unordered_map<string, string>& customers) {

    system("PAUSE");
    system("CLS");

    string customerName=lease.name;
    string carName=string1;
    // Check if the customer name already exists

    customers[customerName] = carName;

    // Save the customer details to a file
    ofstream outFile("output1.txt", ios::app);
    if (outFile.is_open()) {
        outFile << customerName << " " << carName << endl;
        outFile.close();

    } else {
        cout << "Unable to open file to save customer details." << endl;
    }
}

// Function to load customers from file
void returnloadCustomers(unordered_map<string, string>& customers) {

    ifstream inFile("output1.txt");
    string customerName, carName;

    if (inFile.is_open()) {
        while (inFile >> customerName >> carName) {
            customers[customerName] = carName;
        }
        inFile.close();
    } else {
        cout << "Unable to open file to load customers." << endl;
    }
}




int main()
{

        login1();


        system("CLS");
        string decide="yes";
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t\t-----------------------------------------------\n";
        cout<<"\t\t\tSIMPLE CAR RENTAL SYSTEM\n";
        cout<<"\t\t\tWelcome to our Company ,Choose from the menu :"<<endl;
        cout<<"\t\t\t-----------------------------------------------\n";

        while(decide!="exit"){
            menu();
            cout<<"\n\n\n\t\t\tYour Choice: ";
            cin>>theChoice;

                      details(theChoice);


cout<<"\n\n\n\t\t\tAre you sure you want to rent this car?(yes/no/exit)";
            cin>>decide;
            if(decide=="yes"){

                   userInput(theChoice);
                   system("CLS");
                   calculation();
                     unordered_map<string, string> customers;

    returnloadCustomers(customers);
    returnsignUp(customers);


                   payment(theChoice);

            cout<<"\n\n\n\t\t\tBack To Menu?(yes/no)";
            cin>>decide;

            if(decide=="no"){

                    system("CLS");
                    thankYou();
                    system("PAUSE");
                    system("CLS");

                   exitFunction();

                break;
            }

            system("CLS");
            }

            else{
                if(decide=="no"){
                    system("CLS");
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t                                                                      "<<endl;
        cout<<"\t\t\t-----------------------------------------------\n";
        cout<<"\t\t\t               ***Welcome Back***              \n";
        cout<<"\t\t\t-----------------------------------------------\n";

                    continue;
                }
                else if(decide=="exit"){
                    system("CLS");
                    exitFunction();
                    break;
                }

            }

        }
        getch();


    return 0;
}





int login(){
string pass="";
string uname="";
char ch;
 char decide;
    while(decide != 'y' && decide != 'n'){
        cout << "\n\t\t\t\t\tBack To Menu? (y/n): ";

        cin >> decide;
        if (decide == 'y') {
            system("CLS");
            login1();
        } else if (decide == 'n') {
            cout << "Continue..." << endl;
            system("CLS");
        } else {

            cout << "Invalid input..." << endl;
            system("PAUSE");
            system("CLS");
        }

    }

char name;

cout<<"\n\n\t\t\t\t------------------------------------------------"<<endl;
cout<<"\t\t\t\t\t\t\tLOGIN"<<endl;
cout<<"\t\t\t\t------------------------------------------------"<<endl;
 string username, password;
 cout<<"\n\n\t\t\t\t\NOTE:PLEASE PROVIDE AND SET USERNAME WITH NO SPACES OR UNDERSCORE"<<endl;
    cout << "\n\n\t\t\t\t\tEnter username: ";
    cin >> username;
    cout << "\n\n\t\t\t\t\tEnter password: ";

ch=_getch();
 while(ch!=13){
    password.push_back(ch);
    cout<<"*";
    ch=_getch();}


if (authenticate(username, password)) {
    cout<<"\n\n\n\n\t\t\t\t\tAccess Granted! Welcome To Our System \n\n";
    system("PAUSE");
    system("CLS");
    } else {
    cout<<"\n\n\n\n\t\t\t\t\tAccess Aborted...Please Try Again!!\n";
    system("PAUSE");
    system("CLS");
    login();
    }

 }







   void myfunction()
{
        system("CLS");
        string decide="yes";
        cout<<"\t\t\t-----------------------------------------------\n";
        cout<<"\t\t\tSIMPLE CAR RENTAL SYSTEM\n";
        cout<<"\t\t\tWelcome to our Company ,Choose from the menu :"<<endl;
        cout<<"\t\t\t-----------------------------------------------\n";


while(decide!="exit"){
            menu();
            cout<<"\n\n\n\t\t\tYour Choice: ";
            cin>>theChoice;

            details(theChoice);
            cout<<"\n\n\n\t\t\tAre you sure you want to rent this car?(yes/no/exit)";
            cin>>decide;
            if(decide=="yes"){
                   userInput(theChoice);
                   payment(theChoice);
                void saveStringToFile();
                recordFile();

            cout<<"\n\n\n\t\t\tBack To Menu?(yes/exit)";
            cin>>decide;

            if(decide=="exit"){

                    system("CLS");
                    thankYou();
                    system("PAUSE");
                    system("CLS");


                break;
            }

            system("CLS");
            }

            else{
                if(decide=="no"){
                    system("CLS");
                    continue;
                }
                else if(decide=="exit"){
                    system("CLS");
                         login1();
                    while(input==2){
                    myfunction();
                    }
                    break;
                }

            }

        }
        getch();

}
