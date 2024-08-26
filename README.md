CODE:
#include <iostream>
#include <string>
using namespace std;
 
// declaring a constant integer to store maximum number of members and books allowed
const int MAX_MEMBERS = 1000;
const int MAX_BOOKS = 10;

// structs to hold information of members and books
struct Member {
    string name;
    string phoneNumber;
    int regNumber;
    int points;

};

struct Book {
    string title;
    string author;
    int serialNumber;
    bool isIssued;
    string issuedTo;

};
// array to store members and books
Member members[MAX_MEMBERS];
Book books[MAX_BOOKS];

//current count of books and members
int memberCount = 0;
int bookCount = 0;

//function to display members
void displayBanner()
{
    cout << "  *                                                                                                *" << endl;
    cout << "  *                                                                                                *" << endl;
    cout << "  *                                                                                                *" << endl;
    cout << "  *                              WELCOME TO LIBRARY MANAGEMENT SYSTEM                              *" << endl;
    cout << "  *                                                                                                *" << endl;
    cout << "  *                                                                                                *" << endl;
    cout << "  *                                                                                                *" << endl;
}
//functions to register members
void registerMember()
{
    if (memberCount < MAX_MEMBERS)
    {
        Member newMember;
        cout << "Enter member name: ";
        cin >> newMember.name;
        cout << "Enter phone number: ";
        cin >> newMember.phoneNumber;
        newMember.regNumber = memberCount + 1;// assign a regestration number
        newMember.points = 0;// initialize points to 0
        members[memberCount++] = newMember; // add the new member to the array
        cout << "Member registered successfully with registration number: " << newMember.regNumber << endl;
    }
    else
    {
        cout << "Member limit reached." << endl;
    }
}
// function to add books
void addBook()
{
    if (bookCount < MAX_BOOKS)
    {
        Book newBook;
        cout << "Enter book title: ";
        cin >> newBook.title;
        cout << "Enter book author: ";
        cin >> newBook.author;
        newBook.serialNumber = bookCount + 1;// assign book serial number
        newBook.isIssued = false;// check book is available or not
        books[bookCount++] = newBook;//the new book to the array
        cout << "Book added successfully with serial number: " << newBook.serialNumber << endl;
    }
    else
    {
        cout << "Book limit reached." << endl;
    }
}
// function to issue book
void issueBook()
{
    int serialNumber, regNumber;
    cout << "Enter book serial number: ";
    cin >> serialNumber;
    cout << "Enter member registration number: ";
    cin >> regNumber;

    for (int i = 0; i < bookCount; i++)
    {
        if (books[i].serialNumber == serialNumber && !books[i].isIssued)
        {
            for (int j = 0; j < memberCount; j++)
            {
                if (members[j].regNumber == regNumber)
                {
                    books[i].isIssued = true;// Mark the book as issued
                    books[i].issuedTo = members[j].name;// Record who the book is issued to
                    members[j].points += 1; // increase the member's points
                    cout << "Book issued successfully to " << members[j].name << endl;
                    return;
                }
            }
        }
    }
    cout << "Book not found or already issued, or member not found." << endl;
}
// function to return book
void returnBook()
{
    int serialNumber;
    cout << "Enter book serial number: ";
    cin >> serialNumber;

    for (int i = 0; i < bookCount; i++)
    {
        if (books[i].serialNumber == serialNumber && books[i].isIssued)
        {

            for (int j = 0; j < memberCount; j++)
            {
                if (members[j].name == books[i].issuedTo)
                {

                }
            }

            books[i].isIssued = false;// mark the book as returned
            books[i].issuedTo = "";// clear the record of who the book was issued to
            cout << "Book returned successfully." << endl;
            return;
        }
    }
    cout << "Book not found or not issued." << endl;
}
// Function to display the list of members
void displayMembers()
{
    cout << "List of Members:" << endl;
    for (int i = 0; i < memberCount; i++)
    {
        cout << "Name: " << members[i].name << ", Phone: " << members[i].phoneNumber <<
            ",Reg Number: " << members[i].regNumber << ", Points: " << members[i].points << endl;
    }
}
// Function to display the list of books
void displayBooks() {
    cout << "List of Books:" << endl;
    for (int i = 0; i < bookCount; i++)
    {
        cout << "Title: " << books[i].title << ", Author: " << books[i].author
            << ", Serial Number: " << books[i].serialNumber
            << ", Issued: " << (books[i].isIssued ? "Yes" : "No") << endl;
    }
}
// Main function to control the program flow
int main() 
{
    int choice;
    while (true)
    {    
        displayBanner();
        cout << "Library Management System" << endl;
        cout << "1. Add Book" << endl;
        cout << "2. Register Members" << endl;
        cout << "3. Issue Book" << endl;
        cout << "4. Return Book" << endl;
        cout << "5. Display Members" << endl;
        cout << "6. Display Books" << endl;
        cout << "7. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {

       
        case 1:
            addBook();
            break;
        case 2:
            registerMember();
            break;
        case 3:
            issueBook();
            break;
        case 4:
            returnBook();
            break;
        case 5:
            displayMembers();
            break;
        case 6:
            displayBooks();
            break;
        case 7:
            return 0;
        default:
            cout << "Invalid choice. Please try again." << endl;
        }
    }
    return 0;
}
