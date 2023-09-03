#include <iostream>
#include <fstream>
#include <vector>
#include <cctype>  // For isdigit
#include <limits>  // For numeric_limits
#include <sstream> // For stringstream

using namespace std;

class Contact {
public:
    string fname;
    string lname;
    string phone_num;

    Contact(const string& first, const string& last, const string& phone)
        : fname(first), lname(last), phone_num(phone) {}

    void displayContact() const {
        cout << "\n\n\t\tContact details.." << endl;
        cout << "\n\tFirst Name : " << fname;
        cout << "\n\tLast Name : " << lname;
        cout << "\n\tPhone Number : " << phone_num << endl;
    }
};

// Function to add a new contact to the system
void addContact(vector<Contact>& contacts) {
    system("cls");
    string fname, lname, phone_num;

    cout << "\n\n\tEnter First Name : ";
    cin >> fname;
    cout << "\n\tEnter Last Name : ";
    cin >> lname;
    cout << "\n\tEnter 10-Digit Phone Number : ";
    cin >> phone_num;

    // Validate the phone number format
    if (!isValidPhoneNumber(phone_num)) {
        cout << "\n\tInvalid Phone Number! It must contain 10 digits." << endl;
        return;
    }

    // Create a Contact object and add it to the contacts vector
    contacts.emplace_back(fname, lname, phone_num);

    // Save the contact to a file
    ofstream phone("number.txt", ios::app);
    if (phone.is_open()) {
        phone << fname << " " << lname << " " << phone_num << endl;
        cout << "\n\tContact Saved Successfully !" << endl;
        phone.close();
    } else {
        cout << "\n\tError Opening File !" << endl;
    }
}

// Function to search for a contact by name
void searchContact(const vector<Contact>& contacts) {
    bool found = false;
    string keyword;
    cout << "\n\tEnter Name To Search : ";
    cin >> keyword;

    for (const auto& contact : contacts) {
        if (keyword == contact.fname || keyword == contact.lname) {
            system("cls");
            contact.displayContact();
            found = true;
            break;
        }
    }

    if (!found)
        cout << "\n\tNo Such Contact Found" << endl;
}

// Function to validate a phone number format (exactly 10 digits)
bool isValidPhoneNumber(const string& str) {
    if (str.length() != 10 || !isAllDigits(str)) {
        return false;
    }
    return true;
}

// Function to check if a string consists of only digits
bool isAllDigits(const string& str) {
    return all_of(str.begin(), str.end(), ::isdigit);
}

// Function to clear the input buffer
void clearInputBuffer() {
    cin.clear();
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
}

// Main function
int main() {
    vector<Contact> contacts;
    ifstream myfile("number.txt");

    // Load existing contacts from the file
    string first, last, phone;
    while (myfile >> first >> last >> phone) {
        contacts.emplace_back(first, last, phone);
    }

    while (true) {
        system("cls");
        cout << "\n\n\n\t\tContact Management.";
        cout << "\n\n\t1. Add Contact\n\t2. Search Contact\n\t3. Help\n\t4. Exit\n\t> ";

        int choice;
        cin >> choice;

        switch (choice) {
            case 1:
                addContact(contacts);
                break;
            case 2:
                searchContact(contacts);
                break;
            case 3:
                // Add help information here if needed
                break;
            case 4:
                myfile.close();
                return 0;
            default:
                cout << "\n\n\tInvalid Input !" << endl;
                clearInputBuffer(); // Clear input buffer to prevent issues with invalid inputs causing an infinite loop
        }

        cout << "\n\tPress Enter To Continue..";
        cin.ignore();
        cin.get();
    }

    return 0;
}

