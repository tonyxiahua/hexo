---
title: CIS 22C Labs
date: 2016-10-24 08:50:58
tags: [codes,C++]
---
Here is the code page for CIS 22C Labs Delia's Class.
Fall 2016 De Anza College.
Recommend using high resoultion devices to view this page. Thanks.
这是一个我课程代码的页面，如果发现有任何错误请告知我，谢谢。
由于主题排版的问题，在便携设备上可能出现无法显示引索条，建议使用电脑访问。
<!-- more -->

## Lab-1
### City.cpp
```cpp
/*****************************************************************************
                                CIS 22C
                             Linked Lists
 *****************************************************************************/

//Xia Hua
//CIS 22C De Anza College Fall 2016
//Date Oct 4th 2016

#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstdio>
#include "CityList.h"
using namespace std;

void intro();
void readCities(CityList &list, const char inputFileName[]);
void printCities(CityList &list);
void searchCities(CityList &list);
void deleteCities(CityList &list);
void printEndMsg();

/*****************************************************************************
                                Main Function
 *****************************************************************************/

int main()
{
    const char inputFileName[] = "cities.txt";// open
    CityList list;
    intro();
    readCities(list, inputFileName);
    printCities(list);
    
    //Finish Loading
    
    //Display now special age cities.
    list.youngestCity();
    list.oldestCity();
    
    //1.search****************************
    searchCities(list);
    
    //2.delete****************************
    deleteCities(list);
    
    //3.print*****************************
    printCities(list);
    
    //updated cities list
    
    list.youngestCity();
    list.oldestCity();
    
    
    printEndMsg();
    //exit
    system("pause");
    return 0;
}

/*****************************************************************************
 Display a short statement about the purpose of the program
 *****************************************************************************/

void intro()
{
    cout << "_________________________________________\n";
    cout << "Build and process a Linked List of Cities\n\n";
    cout << "Author: Xia Hua       Time: Oct.4.2016"<<endl;
    cout << "_________________________________________\n\n";
}

/********************************************************************************
 Read data about cities from a file and build a sorted linked list
 The list is sorted by city name.
 
 Input Parameter: inputFileName
 Output Parameter: list
 Return Value : none
 *****************************************************************************/

void readCities(CityList &list, const char inputFileName[])
{
    cout << "Reading City data from " << inputFileName << endl<<" . . .  . . ."<<endl;
    City dataIn;
    ifstream infile;
    infile.open(inputFileName);
    string stateName;
    int number;
    string cityName;
    
    while(!infile)
    {
        cout << "Error opening " << inputFileName << "for reading\n";
        exit(111);
    }
    while(infile >> stateName)
    {
        dataIn.setState(stateName);
        infile>>number;
        dataIn.setYear(number);
        infile.ignore();
        getline(infile,cityName, '\n');
        dataIn.setCity(cityName);
        list.insertNode(dataIn);
    }
    infile.close();
    
    cout << "Done reading!"<<endl;
}

/*****************************************************************************
 Display the city list
 Input Parameter: list
 *****************************************************************************/

void printCities(CityList &list)
{
    cout << "\n      Print City Data"<<endl;
    cout << "______________________________"<<endl<<endl;
    
    cout << left << setw(10) << "State" << setw(10) << "Year" << setw(20) << "City" << endl;
    cout << setw(10) << "-----" << setw(10) << "-----" << setw(20) << "----------" << endl;
    list.displayList();
    cout << "__________________________________\n";
    cout << "There are "<< list.countCity() <<" cities in this table!"<<endl;
    cout << "__________________________________\n";
}


/*****************************************************************************
 Search manager: search the city list until the user enters QUIT
 Input Parameter: list
 *****************************************************************************/

void searchCities(CityList &list)
{
    string targetCity;
    
    cout << "\n2. Search"<<endl;
    cout <<   "______"<<endl;
    
    while(targetCity!="quit")
    {
        cout << "\nEnter the city for search (quit for stop searching) : ";
        getline(cin, targetCity);
        
        if(targetCity!="quit")
        {
            list.searchList(targetCity);
        }
    }
    cout << "___________________"<<endl;
}

/*****************************************************************************
 Delete manager: delete cities from the list until the user enters QUIT
 Input Parameter: list
 *****************************************************************************/

void deleteCities(CityList &list)
{
    string targetCity;
    
    cout << "\n3. Delete"<<endl;
    cout << "_______"<< endl;
    
    while(targetCity!="quit")
    {
        cout << endl << "Enter the city for delete (quit for stop searching) : ";
        getline(cin, targetCity);
        
        if(targetCity!="quit")
        {
            list.deleteNode(targetCity);
        }
    }
    cout << "___________________"<<endl;
}

/*****************************************************************************
 Display an "End of the program" message
 *****************************************************************************/

void printEndMsg()
{
    cout << "\n\n___________________________________________________\n\n";
    cout << " This is the End of the Sorted Linked List program!\n";
    cout << " Thanks for using!!!"<<endl;
    cout << "___________________________________________________\n";
}

/***********
 OUTPUT
 ************/
/*
_________________________________________
Build and process a Linked List of Cities

Author: Xia Hua       Time: Oct.4.2016
_________________________________________

Reading City data from cities.txt
. . .  . . .
Done reading!

Print City Data
______________________________

State     Year      City
-----     -----     ----------
MD        1797      Baltimore
MA        1822      Boston
IL        1837      Chicago
OH        1834      Columbus
TX        1856      Dallas
MI        1701      Detroit
TX        1837      Houston
IN        1832      Indianapolis
FL        1822      Jacksonville
CA        1850      Los Angeles
TN        1826      Memphis
WI        1846      Milwaukee
NY        1898      New York
PA        1701      Philadelphia
AZ        1881      Phoenix
TX        1837      San Antonio
CA        1850      San Diego
CA        1850      San Francisco
CA        1850      San Jose
DC        1788      Washington
__________________________________
There are 20 cities in this table!
__________________________________
The youngest city is: New York. Age is :1898
The oldest city is: Detroit. Age is :1701
The another oldest city is: Philadelphia. Age is :1701

2. Search
______

Enter the city for search (quit for stop searching) : Columbus

State     Year      City
-----     -----     ----------
OH        1834      Columbus
Find reslut 1/1

Enter the city for search (quit for stop searching) : Philadelphia

State     Year      City
-----     -----     ----------
PA        1701      Philadelphia
Find reslut 1/1

Enter the city for search (quit for stop searching) : quit
___________________

3. Delete
_______

Enter the city for delete (quit for stop searching) : Philadelphia
The city has been deleted.
There are 19 cities in this table!

Enter the city for delete (quit for stop searching) : New York
<New York  > was not found

Enter the city for delete (quit for stop searching) : New York
The city has been deleted.
There are 18 cities in this table!

Enter the city for delete (quit for stop searching) : quit
___________________

Print City Data
______________________________

State     Year      City
-----     -----     ----------
MD        1797      Baltimore
MA        1822      Boston
IL        1837      Chicago
OH        1834      Columbus
TX        1856      Dallas
MI        1701      Detroit
TX        1837      Houston
IN        1832      Indianapolis
FL        1822      Jacksonville
CA        1850      Los Angeles
TN        1826      Memphis
WI        1846      Milwaukee
AZ        1881      Phoenix
TX        1837      San Antonio
CA        1850      San Diego
CA        1850      San Francisco
CA        1850      San Jose
DC        1788      Washington
__________________________________
There are 18 cities in this table!
__________________________________
The youngest city is: Phoenix. Age is :1881
The oldest city is: Detroit. Age is :1701


____________________________________________

This is the End of the Sorted Linked List program!
Thanks for using!!!
____________________________________________
Program ended with exit code: 0
*/

```


### City.h
```cpp
//
//  City.h
//  HW1
//
//  Created by Rednik Tony on 10/3/16.
//  Copyright © 2016 Hua Xia. All rights reserved.
//
//Xia Hua
//CIS 22C De Anza College Fall 2016
//Date Oct 4th 2016
#ifndef City_h
#define City_h
#include <string>
//#include <iostream>
using namespace std;
/*********************
City Class
 *******************/
class City
{
private:
    string state;
    int year;
    string city;

public:
    //GETTER AND SETTER
    
    void setState(string stateName){
        state=stateName;
    }
    void setYear(int number){
        year=number;
    }
    void setCity(string cityName){
        city= cityName;
    }
    
    string getState(){
        return state;
    }
    int getYear(){
        return year;
    }
    string getCity(){
        return city;
    }
};


#endif /* City_h */
	
```

### CityList.cpp

```cpp

//Xia Hua
//CIS 22C De Anza College Fall 2016
//Date Oct 4th 2016

// Implementation file for the CityList class
#include <iostream>  // For cout and NULL
#include <iomanip>
#include <string>
#include "CityList.h"
using namespace std;

/**************************************************
 Constructor
 This function allocates an empty node to act as a
 sentinel node: it makes the code shorter and the
 processing of the list faster.
 **************************************************/

CityList::CityList()
{
    head = new ListNode;
    head->next = NULL;
    head->data.setYear(0);
    head->data.setState("");
    head->data.setCity("");
}

/**************************************************
 Display the value stored in each node of
 the linked list
 **************************************************/

void CityList::displayList() const
{
    ListNode *nodePtr = head->next;
    while (nodePtr)
    {
        cout << setw(10) << nodePtr->data.getState();
        cout << setw(10) << nodePtr->data.getYear();
        cout << setw(20) << nodePtr->data.getCity() << endl;
        nodePtr = nodePtr->next;//move to the next node
    }
}

/**************************************************
 Calculate and retrun how many cities in the list
 **************************************************/

int CityList::countCity(){
    return counter;}

/**************************************************
 Insert a new node into a sorted list and
 keeps the list sorted
 **************************************************/

void CityList::insertNode(City dataIn)
{
    ListNode *newNode;
    ListNode *nodePtr = head->next;
    ListNode *prevNode = head;
    
    // Allocate a new node and store dataIn there.
    newNode = new ListNode;
    newNode->data = dataIn;
    
    // Skip all nodes whose value is less than num.
    while (nodePtr != NULL && nodePtr->data.getCity() < dataIn.getCity())
    {
        prevNode = nodePtr;
        nodePtr = nodePtr->next;
    }
    // Update links to insert the new node
    prevNode->next = newNode;
    newNode->next = nodePtr;
    counter++;
}

/**************************************************
 Search for a city in the list
 If found, it prints it.
 **************************************************/

void CityList::searchList(string city) const
{
    ListNode *nodePtr;
    nodePtr = head->next;
    
    while (nodePtr != NULL && nodePtr->data.getCity() != city)
    {
        nodePtr = nodePtr->next;
    }
    if(nodePtr != NULL && nodePtr->data.getCity() == city) // Display the value in this node.
    {
        cout << endl << left << setw(10) << "State" << setw(10) << "Year" << setw(20) << "City" << endl;
        cout << setw(10) << "-----" << setw(10) << "-----" << setw(20) << "----------" << endl;
        cout << setw(10) << nodePtr->data.getState();
        cout << setw(10) << nodePtr->data.getYear();
        cout << setw(20) << nodePtr->data.getCity() << endl;
        cout << "Find reslut 1/1"<<endl;
    }
    else // Display error if there is no result in this node
    {
        cout << "<" << city << ">" << " was not found" << endl;
    }
}

/**************************************************
 /////////////Finding the youngest city///////////
 **************************************************/

void CityList::youngestCity() const
{
    ListNode *nodePtr;
    nodePtr = head->next;
    int youngestCity = 0;
    string cityName1 = "";
    string cityName2 = "";
    while (nodePtr !=NULL && nodePtr->data.getYear())
    {
        int pervious = nodePtr->data.getYear();;
        if (youngestCity < pervious)
        {
            youngestCity = pervious;
            cityName1 = nodePtr->data.getCity();
        }
        //check if there has any same age cities
        if (youngestCity == pervious)
        {
            youngestCity = pervious;
            cityName2 = nodePtr->data.getCity();
        }
        nodePtr = nodePtr->next;
    }
    if (nodePtr !=NULL && nodePtr->data.getYear())
    {
        nodePtr -> data.getYear();
    }
    cout<< "The youngest city is: "<<cityName1<<". Age is :"<<youngestCity<<endl;
    //There are some cities has same age. So I make double display list.
    if (cityName2 !=cityName1)
    {
        cout << "The another youngest city is: "<< cityName2 << ". Age is :" << youngestCity << endl;
    }
}
/**************************************************
 /////////////Finding the oldest city/////////////
 **************************************************/

void CityList::oldestCity() const
{
    ListNode *nodePtr;
    nodePtr = head->next;
    int oldestCity = 2016;
    string cityName1 = "";
    string cityName2 = "";
    while (nodePtr !=NULL && nodePtr->data.getYear())
    {
        int pervious = nodePtr->data.getYear();
        if (oldestCity > pervious){
            oldestCity =pervious;
            cityName1 = nodePtr->data.getCity();
        }
        //check if there has any same age cities
        if (oldestCity == pervious){
            oldestCity =pervious;
            cityName2 = nodePtr->data.getCity();
        }
        nodePtr = nodePtr->next;
    }
    if (nodePtr !=NULL && nodePtr->data.getYear())
    {
        nodePtr -> data.getYear();
    }
    cout<< "The oldest city is: "<<cityName1<<". Age is :"<<oldestCity<<endl;
    //There are some cities has same age. So I make double display list.
    if (cityName2 !=cityName1)
    {
        cout << "The another oldest city is: "<< cityName2 << ". Age is :" << oldestCity << endl;
    }
}

/**************************************************
 Delete a city from the list (if found)
 **************************************************/

void CityList::deleteNode(string city)
{
    ListNode *nodePtr = head->next;
    ListNode *prevNode = head;
    while (nodePtr != NULL && nodePtr->data.getCity() != city)
    {
        prevNode = nodePtr;
        nodePtr = nodePtr->next;
    }
    if (nodePtr) // found
    {
        prevNode->next = nodePtr->next;
        delete nodePtr;
        cout << "The city has been deleted."<<endl;
        counter--;
        cout << "There are "<<counter <<" cities in this table!"<<endl;
    }
    else
    {
        cout << "<" << city << ">" << " was not found" << endl;
    }
}

/**************************************************
 Destructor
 This function deletes every node in the list.
 **************************************************/

CityList::~CityList()
{
    ListNode *nodePtr = head;
    ListNode *nextNode;
    while (nodePtr != NULL)
    {
        nextNode = nodePtr->next;
        delete nodePtr;
        nodePtr = nextNode;
    }
}

/**************************************************
                END OF CITYLIST
**************************************************/

```

### CityList.h

```cpp
//Xia Hua
//CIS 22C De Anza College Fall 2016
//Date Oct 4th 2016

// Specification file for the CityList class
#ifndef CITYLIST_H
#define CITYLIST_H
#include <iostream>
#include "City.h"
using namespace std;

class CityList
{
private:
    int counter=0;// This is a counter for how many cities in linked list
    struct ListNode
    {
        City data;
        ListNode *next;
    };
    ListNode *head;
public:
    // Constructor
    CityList();
    // Destructor
    ~CityList();
    // Linked list operations
    
    int countCity();
    void insertNode(City);
    
    void deleteNode(string);
    void searchList(string) const;
    
    void youngestCity() const;      //find the youngestcity
    void oldestCity() const;        //find the oldestcity
    
    void displayList() const;
};
#endif
```

### city.txt

```cpp
CA 1850 San Francisco
MA 1822 Boston
TX 1856 Dallas
IL 1837 Chicago
WI 1846 Milwaukee
TX 1837 Houston
IN 1832 Indianapolis
DC 1788 Washington
FL 1822 Jacksonville
CA 1850 Los Angeles
MI 1701 Detroit
TN 1826 Memphis
TX 1837 San Antonio
NY 1898 New York
PA 1701 Philadelphia
MD 1797 Baltimore
AZ 1881 Phoenix
CA 1850 San Diego
OH 1834 Columbus
CA 1850 San Jose
```

## Lab-2
### main.cpp
```cpp
//
//  main.cpp
//  HW2-Extend
//
//  Created by Rednik Tony on 10/18/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//

#include <iostream>
#include <cstdlib>
#include <string>
#include <ctime>
#include <fstream>
#include <sstream>
#include <algorithm>
#include <iterator>

#include "ClassNode.h"
using namespace std;

//Outer Interface
void intro();
void helpMenu();
void about();
void exitInterface(char, ClassNode &list);
void printForward(ClassNode &list);
void printBackward(ClassNode &list);
void printCounter(ClassNode &list);

void insertLineNumber(ClassNode &list);
void listLineNumber(ClassNode &list);
void deleteLineNumber(ClassNode &list);
void saveFile(char ,ClassNode &list);
//Inner Process
void readText(ClassNode &list, const char inputFileName[]);
void printNodes(ClassNode &list);
void search(ClassNode &list);

int main()
{
    
    const char inputFileName[] = "input.txt";
    ClassNode list;
    
    intro();
    readText(list, inputFileName);

    while(1){
        cout << "*******************************************************"<<endl;
        cout << "Program is running. Type 'H' for program documentation!" << endl;
        char selection = 'Q';
        cout << "*******************************************************\n"<<endl;
        cout << "Please enter your selection (Please type in capital letter, 'H' for help)"<<endl;
        cin >>selection;
        switch (selection)
        {
            case 'T': printCounter(list);break;
            case 'F': printForward(list);break;
            case 'B': printBackward(list);break;
            //----------------------------------
            case 'I': insertLineNumber(list);break;
            case 'L': listLineNumber(list);break;
            case 'D': deleteLineNumber(list);break;
            //----------------------------------
            case 'S': saveFile(selection,list);break;
            //----------------------------------
            case 'H': helpMenu();break;
            case 'A': about();break;
            //----------------------------------
            case 'E': search(list);break;
            case 'Q': exitInterface(selection,list);return 222;break;
            default: cout << "Invaild selection! Please type again!!!" << endl;
        }
    }
    system("pause");//This is for the Visual Studio 2015 IDE ignore the warning infromation at xcode
    return 0;
}

//**************************************************************************************************

void readText(ClassNode &list, const char inputFileName[])
{
    cout << "Reading City data from " << inputFileName << endl<<" . . . Loading. . .Reading Lines. . ."<<endl;
    text dataIn;
    ifstream infile;
    
    infile.open(inputFileName);
    string textIn;
    while(!infile)
    {
        cout << "Error opening" << inputFileName << "for reading\n";
        exit(111);
    }
    while(infile)
    {
        getline( infile , textIn , '\n' );
        dataIn.setText(textIn);
        //cout << textIn <<endl;
        list.insertNode(dataIn);
    }
    infile.close();
    cout << endl;
    cout << ". . .Done reading!"<<endl<<endl;
}

//======================================================

void intro()
{
    cout << "___________________________________________________\n";
    cout << "CIRCULARLY DOUBLY-LINKED LISTS with a sentinel node\n\n";
    cout << "Developer: Xia Hua      Time: Oct.14.2016"<<endl;
    cout << "___________________________________________________\n\n";
    
}

//=======================================================

void printCounter(ClassNode &list){
    cout << "______________________________"<<endl<<endl;
    cout << "Here is the lines number we have: ";
    list.displayCounter();
}

void printForward(ClassNode &list){
    cout << "______________________________"<<endl<<endl;
    list.displayForwList();
}

void printBackward(ClassNode &list){
    cout << "______________________________"<<endl<<endl;
    list.displayBackList();
}

//=======================================================

void insertLineNumber(ClassNode &list){
    int line = 0;
    string text = " ";
    cout << "Please enter the line and information you want to insert.\n(Ignore this message if you already typed)." << endl;
    cin >> line >> text;
    cout <<"Insert a new line of text at position"<<line<<"in the list..."<< endl;
    cout << "\n___________________________________________________"<<endl;
    list.insertNodeLine(line, text);
    cout <<endl;
}

void listLineNumber(ClassNode &list)
{
    int line1=0;
    int line2=0;
    cout << "Please enter the lines you want to show.(Ignore this message if you already typed)." << endl;
    cout << "\n___________________________________________________"<<endl;
    cin >> line1 >> line2;
    list.listNodeLine(line1,line2);
    cout << endl;
}

void deleteLineNumber(ClassNode &list)
{
    int line1, line2;
    line1 = line2 =0;
    cout << "Please enter the lines you want to delete.(Ignore this message if you already typed)." << endl;
    cout << "\n___________________________________________________"<<endl;
    cin >> line1 >> line2;
    list.deleteNodeLine(line1,line2);
    cout << "Delete finish...Continue..."<< endl<<endl;
}

//=================================================

void helpMenu()
{
    cout << endl;
    cout << "_________________________________________\n";
    cout << "\t\t\tHere is Help Page"<<endl;
    cout << "Instructions for T, F, B, I, L, D, S, H, A and Q"<< endl;
    cout << "_________________________________________\n";
    cout << "T:\nDisplay the total number of lines in the text."<< endl;
    cout << "_________________________________________\n";
    cout << "F:\nPrint all lines from first to last (show the line numbers: 1, 2, 3, etc.)" << endl;
    cout << "_________________________________________\n";
    cout << "B:\nPrint all lines from last to first (show the line numbers).:"<< endl;
    cout << "_________________________________________\n";
    cout << "I <line number> <text> " << endl;
    cout << "Command: I 3 'This is the new line of text to be inserted' " << endl;
    cout << "Result: Insert a new line of text at position 3 in the list" << endl;
    cout << "_________________________________________\n";
    cout << "L <line number 1> <line number 2>" << endl;
    cout << "Command: L 2 5 " << endl;
    cout << "Result: List lines 2 to 5 inclusive (show the line numbers) " << endl;
    cout << "Command: L 5 2" << endl;
    cout << "Result: List lines 5 to 2 inclusive, in reverse order (show the line numbers)" << endl;
    cout << "_________________________________________\n";
    cout << "D <line number 1> <line number 2> "<< endl;
    cout << "Command: D 3 7\n D 7 3" << endl;
    cout << "Result: Delete lines 3 to 7 inclusive" << endl;
    cout << "_________________________________________\n";
    cout << "S <output file name>" << endl;
    cout << "Command: S out.txt" <<endl;
    cout << "Result: Save the updated text to an output file."<< endl;
    cout << "_________________________________________\n";
    cout << "H :"<<endl;
    cout << "Help: Display instructions for T, F, B, I, L, D, S, H, A and Q" << endl;
    cout << "_________________________________________\n";
    cout << "A " << endl;
    cout << "About: Display information about the developer:" << endl;
    cout << "_________________________________________\n";
    cout << "E <key word>" <<endl;
    cout << "Display the lines that contain the given key word." << endl;
    cout << "_________________________________________\n";
    cout << "Q" << endl;
    cout << "Quit editing the file (save it to backup.txt) "<< endl;
    cout << "_________________________________________\n\n\n";
}

void about()
{
    cout << "____Developer Information_____"<<endl;
    cout << "\n|Developer Information\n|Name: Xia Hua\n|Class: CIS 22C\n|Quater: Fall\n|Year: 2016\n|College: De Anza College" << endl;
    cout << "______________________________"<<endl<<endl;
}

//================================================

void saveFile(char selection,ClassNode &list)
{
    cout << "\n___________________________________________________"<<endl<<endl;
    cout << "Recent line are saving to same folder text file" <<endl;
    list.saveNodeFile(selection);
    cout << "\n\nDone saving!!! "<<endl;
    cout << "\n___________________________________________________"<<endl<<endl;
}

//==================================================

void search (ClassNode &list)
{
    
}

//==========================================
void exitInterface(char selection, ClassNode &list){
    cout << "______________________________"<< endl;
    cout << "Program stopped...Exiting program..." << endl;
    list.saveNodeFile(selection);
    cout <<"........................................" << endl;
    cout << "Your lines was saved to 'backup.txt'" << endl;
    cout << "______________________________"<< endl << endl;
    cout << "Saved at the same folder"<< endl<<endl;
    cout << "Thanks again for using this program!<<endl;
}

```

### ClassNode.cpp

```cpp
//
//  ClassNode.cpp
//  HW2-RE
//
//  Created by Rednik Tony on 10/18/16.
//  Copyright © 2016 Hua Xia. All rights reserved.
//
#include <iostream>
#include <string>
#include <iomanip>
#include <sstream>
#include <algorithm>
#include <iterator>
#include <fstream>
#include "ClassNode.h"
using namespace  std;

ClassNode::ClassNode()
{
    head = new ListNode;
    head->next =head;
    head->prev = head;
    head->data.setText("");
    counter = 0;
}

void ClassNode::insertNode(text dataIn){
    ListNode *newNode;
    newNode = new ListNode;
    newNode->data = dataIn;
    
    ListNode *nodePtr;
    nodePtr =head;
    for (int i=0; i< counter; i++)
    {
         nodePtr = nodePtr->next;
    }
    nodePtr->next = newNode;
    newNode->prev = nodePtr;
    newNode->next = head;
    head -> prev = newNode;
    counter++;
    cout << counter<<".";//TO DO: delete those when those  success
    //cout << newNode->data.getText()<<endl;
}
///////////////////////////////////////////////////////////////////////////////
void ClassNode::displayCounter() const
{
    cout << counter-1 <<endl<<endl;
}

void ClassNode::displayForwList() const
{
    ListNode *temp =head;
    while(temp->next != head->prev)
    {
        temp = temp->next;
        cout << temp->data.getText()<<endl;
    }
}

void ClassNode::displayBackList() const
{
    ListNode *temp=head->prev;
    while (temp->prev != head->prev)
    {
        temp = temp->prev;
        cout << temp->data.getText()<<endl;
    }
}
///////////////////////////////////////////////////////////////////////////////
void ClassNode::insertNodeLine(int line, string textInfo){
    ListNode *tempPtr1;
    ListNode *newnode;
    ListNode *tempPtr2=head;
    
    newnode = new ListNode;

    newnode -> data.setText(textInfo);
    
    for(int i=0; i<line;i++)
    {
        tempPtr2 = tempPtr2 ->next;
    }
    
    tempPtr1 = tempPtr2->next;
    tempPtr2->next = newnode;
    newnode->next = tempPtr1;
    tempPtr1->prev = newnode;
    newnode->prev = tempPtr2;
    if(line == 0)
    {
        head= newnode;
    }
}

void ClassNode::listNodeLine(int line1 ,int line2)
{
    int temp = 0;
    if(line1>0 && line2>0 && line1<=counter && line2<=counter)
    {
        if(line1>line2)
        {
            temp = line2;
            line2 = line1;
            line1 = temp;
        }
    }
    else{
        cout<<"Invalid Input!"<<endl;
    }
    ListNode *nodePtr1=head;
    ListNode *nodePtr2=head;
    for(int i=0; i<line1;i++)
    {
        nodePtr1=nodePtr1->next;
    }
    for(int i=0;i<line2;i++)
    {
        nodePtr2=nodePtr2->next;
    }
    
    int range =line2-line1+1;
    
    if(line1 <= line2)
    {
        for(int i=0; i<range; i++)
        {
            cout<< line1+i << ". " << nodePtr1->data.getText()<<endl;
            nodePtr1=nodePtr1->next;
        }
    }
    else
    {
        for(int i=0; i<range; i++)
        {
            cout<<line2-i << ". " << nodePtr2->data.getText()<<endl;
            nodePtr2=nodePtr2->prev;
        }
    }
}

void ClassNode::deleteNodeLine(int line1, int line2)
{
    int temp = 0;
    if(counter<=0){
        cout << "Empty List!"<< endl;
    }
    
    if(line1>0 && line2>0 && line1<=counter && line2<=counter)
    {
        if(line1>line2)
        {
            temp = line2;
            line2 = line1;
            line1 = temp;
        }
    }
    else{
        cout<<"Invalid Input!"<<endl;
    }
    //----------------------------
    int range = line2 - line1 +1;
    ListNode *temp1 = head;
    ListNode *temp2 = head;
    for(int i=0; i<line1;i++)
    {
        temp1=temp1->next;
    }
    for(int i=0;i<line2+1;i++)
    {
        temp2=temp2->next;
    }
    //---------------------------
    if (line1 == 1){
        head->next= temp2->next;
        temp2->prev = temp1->prev;
        temp1->next= temp2->next;
        cout<< head->data.getText();
    }
    if (line1==line2){
        temp1->prev->next = temp1->next;
    }
    //----------------
    temp1->prev->next = temp2;
    temp2->prev= temp1->prev;
    counter -= range;
}
//------------------------------------
void ClassNode::saveNodeFile(char choice)
{
    if (choice == 'S')
    {
        string outFileName="save.txt";
        cin >> outFileName;
        savefile(outFileName);
    }
    if (choice == 'Q')
    {
        savefile("backup.txt");
    }
}

void ClassNode::savefile(string outFileName){
    ofstream outFile;
    outFile.open(outFileName);
    ListNode* nodeptr=head;
    for(int i=0; i<counter-1; i++)
    {   nodeptr=nodeptr->next;
        outFile<<left<<setw(4)<<i+1<<nodeptr->data.getText()<<endl;
    }
    outFile.close();
    cout<<"Current lines was saved to succeessfully to"<< outFileName <<endl;
    cout<< "You can find this doucment in the same folder"<<endl;
}

//-----------------------------------------

ClassNode::~ClassNode()
{
    ListNode *nodePtr = head;
    ListNode *nextNode;
    for (int i=0;i<counter;i++)
    {
        nextNode= nodePtr -> next;
        delete nodePtr;
        nodePtr = nextNode;
    }
    delete nodePtr;
}

```

### ClassNode.h

```cpp
//
//  ClassNode.hpp
//  HW2-RE
//
//  Created by Rednik Tony on 10/18/16.
//  Copyright © 2016 Hua Xia. All rights reserved.
//

#ifndef ClassNode_h
#define ClassNode_h
#include <iostream>
#include <string>
#include <stdio.h>
#include "Class.h"

class ClassNode{
private:
    int counter=0;
    struct ListNode
    {
        text data;
        ListNode *next;
        ListNode *prev;
    };
    ListNode *head;
public:
    //---------------
    ClassNode();
    ~ClassNode();
    //---------------
    void insertNode(text);
    void displayForwList() const;
    void displayBackList() const;
    void displayCounter() const;
    void deleteNode(text);
    //---------------
    void insertNodeLine(int,string);
    void listNodeLine(int,int);
    void deleteNodeLine(int,int);
    //---------------
    void search();
    //---------------
    void saveNodeFile(char);
    void savefile(string outFileName);
};

#endif /* ClassNode_h */

```

### Class.h

```cpp

//
//  Class.h
//  HW2-RE
//
//  Created by Rednik Tony on 10/18/16.
//  Copyright © 2016 Hua Xia. All rights reserved.
//

#ifndef Class_h
#define Class_h
#include <iostream>
#include <string>
#include <stdio.h>
using namespace std;

class text{
private:
    string textData;
public:
    void setText(string textIn){
        textData = textIn;
    }
    string getText(){
        return textData;
    }
};

#endif /* Class_h */
```

### input.txt
```cpp
AAAAAAAAAAAAAAAA
Charles Babbage 1837
Ada Lovelace 1843 CCCCCCCCCCCCCCC
George Boole 1847
Kurt Gödel 1931
John Atanasoff 1943
John von Neumann 1945
Sergei Alekseyevich Lebedev 1951 Grace Hopper 1952
John Backus 1954
Peter Naur 1960
C.A.R. Hoare 1960
DDDDDDDDDD
EEEEEEEEE
FFFFFF
GGGGGGGGGGGGGGG
Kristen Nygaard 1962
Dennis Ritchie 1967
Ken Thompson 1967
Edsger Dijkstra 1968
Donald Knuth 1968
Niklaus Wirth 1970
Sophie Wilson 1981
Tim Berners-Lee 1989
BBBBBBBBBBB
```

## Lab-3
### main.cpp
```cpp
//
//  main.cpp
//  HW3
//
//  Created by Rednik Tony on 10/25/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//

#include <iostream>
#include <string>
#include <cctype>
#include <iomanip>
#include <fstream>
#include <algorithm>
#include <sstream>
#include <iterator>
#include <vector>
#include "Stack.h"
#include "Queue.h"
using namespace std;
//outer function

void intro();
void writetofiles();
void farewell();
/////////////////////////Here I have 3 functions to process data//////////////////////
void readText(const char [],Queue<string> *,Queue<string> *);
void processfile(Queue<string> *,Queue<string> *, Stack<string> *, Queue<string> *);
void writetofiles(string,Queue<string> *);
/////////////////////////////////////////////////////////////////////////////////////


int main()
{
    Stack<string> *S= new Stack<string>;
    Queue<string> *Q= new Queue<string>;
    Queue<string> *stringdata = new Queue<string>;
    Queue<string> *Raw = new Queue<string>;
    
    intro();
    cout<<"*** Palindromes Test : 1 means it is a palindrome , 0 means it is not a palindrome ***"<<endl<<endl;
    const char inputFileName[] = "test_word_plndrms.txt";
    const string outputFileName = "word_plndrms.txt";
    
    readText(inputFileName,stringdata,Raw);
    processfile(stringdata,Raw,S,Q);
    
    writetofiles(outputFileName,Raw);
    
    system("pasue");
    return 0;
}
/*************************************************************
                        Intro function
 
 *************************************************************/
void intro()
{
    cout << "*******************************************************"<<endl;
    cout << "                Word-By-Word Palindromes               \n"<<endl;
    cout << "Author: Xia Hua        Date: Oct 27th 2016      CIS 22C"<<endl;
    cout << "*******************************************************\n"<<endl;
}
/*************************************************************
                        Read text file
 
 *************************************************************/

void readText(const char inputFileName[],Queue<string> *stringdata, Queue<string> *Raw)
{
    cout << "Reading City data from " << inputFileName << endl<<" . . . Loading. . .Reading Lines. . \n"<<endl;
    ifstream infile;
    
    infile.open(inputFileName);
    string textIn="";
    //getting error msg
    while(!infile)
    {
        cout << "Error opening" << inputFileName << "for reading\n";
        cout << "Check your files on reading!!!"<<endl;
        exit(111);
    }
    //good reading to 2 queues
    while(getline(infile,textIn, '\n'))
    {
        Raw->enqueue(textIn);
        for (int i = 0, len = textIn.size(); i < len; i++)
        {
            if (ispunct(textIn[i]))
            {
                textIn.erase(i--, 1);
                len = textIn.size();
            }
            if (isupper(textIn[i]))
            {
                textIn[i] = tolower(textIn[i]);
            }
        }
        stringdata->enqueue(textIn);
    }
    infile.close();
    
    cout << endl;
    cout << ". . .Done reading!"<<endl<<endl;
}
/*************************************************************
            Here I have the all process method
                    delete, sort, skip
 *************************************************************/
void processfile (Queue<string> *stringdata, Queue<string> *Raw, Stack<string> *S, Queue<string> *Q)
{
    string tempLine="";
    string tempword="";
    
    string Qcompareword="";
    string Scompareword="";
    
    string trash="";
    
    int linecount=1+stringdata->getCount();
    
    for(int t=0; t < linecount-1; t++)
    {
        //This is pocessing a line inside a line
        stringdata->dequeue(tempLine);
        stringstream ss(tempLine);
        while (ss >> tempword)
        {
            Q->enqueue(tempword);
            S->push(tempword);
           // cout << tempword << endl;
            
        }
        
        //Compare the word is the same
        Q->dequeue(Qcompareword);
        S->pop(Scompareword);
        
        int flag=0;
        int numberOfWords = -1+Q->getCount();
        int check=numberOfWords%2;
        //check the even or odd words in line. got the right way to deal with lines.....
        if (check == 0)
        {
            for (int s =0; s< numberOfWords/2;s++)
            {
                if( Qcompareword == Scompareword )
                {
                    flag = 1; //is par
                }
                else
                {
                    flag = 0;// is not par
                }
                Q->dequeue(Qcompareword);
                S->pop(Scompareword);
            }
        }
        else
        {
            for (int s =0; s < numberOfWords/2;s++)
            {
                if( Qcompareword == Scompareword )
                {
                    flag = 1;
                }
                else
                {
                    flag = 0;
                }
                Q->dequeue(Qcompareword);
                S->pop(Scompareword);
            }
        }
        //Bring back to queues
        string outData="";
        Raw->dequeue(outData);
        
        if(flag == 1)
        {
            outData = "1 " + outData;
        }
        else
        {
            outData = "\t0 "+ outData;
        }
        Raw->enqueue(outData);
        
        //cleaning the stack and queue
        while (Q->isEmpty() == false)
        {
            Q->dequeue(trash);
            S->pop(trash);
        }
        //cout <<"numberOfWords " << numberOfWords<<endl;
        stringdata->enqueue(tempLine);
        
        cout << outData << endl<<endl;
    }//This is a long loop.....
}
/*************************************************************
                Write to files & farewell
 
 *************************************************************/

void writetofiles(string outputFileName,Queue<string> *Raw){
    cout << "Processing text files to word_plndrms.txt" << endl;
    ofstream outFile(outputFileName);
    string temp="";
    while(Raw->isEmpty()==false){
        Raw->dequeue(temp);
        outFile << temp <<endl;
    }
    outFile.close();
    cout << "Writing text data finished....."<<endl;
    cout << "Thanks for using !!!"<<endl;
}


```
### Stack.h
```cpp
/**~*~*
 Stack template
 *~**/
#ifndef DYNAMICSTACK_H
#define DYNAMICSTACK_H
#include <iostream>
using namespace std;

template <class T>
class Stack
{
private:
    // Structure for the stach nodes
    struct StackNode
    {
        T value;          // Value in the node
        StackNode *next;  // Pointer to next node
    };
    
    StackNode *top;     // Pointer to the stack top
    int count;
    
public:
    //Constructor
    Stack(){top = NULL; count = 0;}
    
    // Destructor
    ~Stack();
    
    // Stack operations
    bool push(T);
    bool pop(T &);
    bool isEmpty();
    int getCount(){return count;};
    T* getTop();
};

/**~*~*
 Destructor
 *~**/
template <class T>
Stack<T>::~Stack()
{
    StackNode *currNode, *nextNode;
    
    // Position nodePtr at the top of the stack.
    currNode = top;
    
    // Traverse the list deleting each node.
    while (currNode) //while (currNode != NULL)
    {
        nextNode = currNode->next;
        delete currNode;
        currNode = nextNode;
    }
}

/**~*~*
 Member function push pushes the argument onto
 the stack.
 *~**/
template <class T>
bool Stack<T>::push(T item)
{
    StackNode *newNode; // Pointer to a new node
    
    // Allocate a new node and store num there.
    newNode = new StackNode;
    if (!newNode)
        return false;
    newNode->value = item;
    
    // Update links and counter
    newNode->next = top;
    top = newNode;
    count++;
    
    return true;
}

/**~*~*
 Member function pop pops the value at the top
 of the stack off, and copies it into the variable
 passed as an argument.
 *~**/
template <class T>
bool Stack<T>::pop(T &item)
{
    StackNode *temp; // Temporary pointer
    
    // empty stack
    if (count == 0)
        return false;
    
    // pop value off top of stack
    item = top->value;
    temp = top->next;
    delete top;
    top = temp;
    count--;
    
    return true;
}

/**~*~*
 Member function returns the value at the top
 of the stack - copies it into the variable
 passed as an argument.
 *~**/
template <class T>
T* Stack<T>::getTop()
{
    T *item;
    
    // empty stack
    if (count == 0)
        return nullptr;
    
    // get value at top of stack
    *item = top->value;
    
    return item;
}

/**~*~*
 Member function isEmpty returns true if the stack
 is empty, or false otherwise.
 *~**/
template <class T>
bool Stack<T>::isEmpty()
{
    return count == 0;
}
#endif

```
### Queue.h
```cpp
//
//  Queue.hpp
//  HW3
//
//  Created by Rednik Tony on 10/27/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//

/**~*~*
 Queue template
 *~**/
#ifndef DYNAMICQUEUE_H
#define DYNAMICQUEUE_H
#include <iostream>
using namespace std;

template <class T>
class Queue
{
private:
    // Structure for the queue nodes
    struct QueueNode
    {
        T value;          // Value in the node
        QueueNode *next;  // Pointer to next node
    };
    
    QueueNode *front;    // Pointer to the queue front
    QueueNode *rear;     // Pointer to the queue rear
    int count;
    
public:
    //Constructor
    Queue(){front = rear = NULL; count = 0;}
    
    // Destructor
    ~Queue();
    
    // Stack operations
    bool enqueue(T);
    bool dequeue(T &);
    bool isEmpty();
    int  getCount();
    bool queueFront(T &);
    bool queueRear(T &);
};

/**~*~*
 Destructor
 *~**/
template <class T>
Queue<T>::~Queue()
{
    QueueNode *currNode, *nextNode;
    
    // Position nodePtr at the top of the stack.
    currNode = front;
    
    // Traverse the list deleting each node.
    while (currNode) //while (currNode != NULL)
    {
        nextNode = currNode->next;
        delete currNode;
        currNode = nextNode;
    }
}


/**~*~*
 Member function getCount returns
 the number of elements in the queue
 *~**/
template <class T>
int Queue<T>::getCount()
{
    return count;
}

/**~*~*
 Member function isEmpty returns true if the stack
 is empty, or false otherwise.
 *~**/
template <class T>
bool Queue<T>::isEmpty()
{
    return count == 0;
}

/**~*~*
 Member function enqueue inserts the argument into
 the queue.
 *~**/
template <class T>
bool Queue<T>::enqueue(T item)
{
    QueueNode *newNode; // Pointer to a new node
    
    // Allocate a new node and store num there.
    newNode = new QueueNode;
    if (!newNode)
        return false;
    newNode->value = item;
    
    // Update links and counter
    newNode->next = NULL;
    
    if( front == NULL )        // insert to an empty queue
        front = newNode;
    else
        rear->next = newNode;
    
    count++;
    rear = newNode;
    
    return true;
}

/**~*~*
 Member function dequeue deletes the value at the front
 of the queue, and copies it into the variable
 passed as an argument.
 *~**/
template <class T>
bool Queue<T>::dequeue(T &item)
{
    QueueNode *pDel; // Temporary pointer
    
    // empty queue
    if (count == 0)
        return false;
    
    // delete the value at the front of the queue
    item = front->value;
    pDel = front;
    
    if( count == 1 )
        rear = front = NULL;
    else
        front = front->next;
    
    count--;
    delete pDel;
    
    return true;
}

/**~*~*
 Member function queueFront copies the value at the front
 of the queue into the variable passed as an argument.
 *~**/
template <class T>
bool Queue<T>::queueFront(T &item)
{
    if( front == NULL )
        return false;
    
    item = front->value;
    
    return true;
}

/**~*~*
 Member function queueRear copies the value at the rear
 of the queue into the variable passed as an argument.
 *~**/
template <class T>
bool Queue<T>::queueRear(T &item)
{
    if( rear == NULL )
        return false;
    
    item = rear->value;
    return false;
}

#endif
```
### test_word_plndrms.txt

```cpp
Did I say you never say "never say never"? You say I did.
Did I say you never say "never"?
Are you glad you are king?
King, are you glad you are king?
Fall leaves after leaves fall.
Says Mom, "What do you do?" - You do what Mom says.
Says Mom, "What do you do?" - You do what Mom does.
You know, I did little for you, for little did I know you.
You know, I did little for you, since little did I know you.
First Ladies rule the State.
Escher, drawing hands, drew hands drawing.
You can cage a swallow, can't you?
First Ladies rule the State, and state the rule: "ladies first".
Blessed are they that believe they are blessed.
You can cage a swallow, can't you, but you can't swallow a cage, can you? Mind your own business: Own your mind.
Rode, and rode, and rode, and rode, and rode, and rode, and rode!
Clatter and hum and crunch, and crunch and hum and clatter.
Mind your own business.
All for one, and one for all!
Escher, drawing hands, drew hands drawing Escher.
```
### word_plndrms.txt
```cpp
1 Did I say you never say "never say never"? You say I did. 
	0 Did I say you never say "never"?
	0 Are you glad you are king?
1 King, are you glad you are king?
1 Fall leaves after leaves fall.
1 Says Mom, "What do you do?" - You do what Mom says.
1 Says Mom, "What do you do?" - You do what Mom does.
1 You know, I did little for you, for little did I know you.
1 You know, I did little for you, since little did I know you.
	0 First Ladies rule the State.
	0 Escher, drawing hands, drew hands drawing.
	0 You can cage a swallow, can't you?
1 First Ladies rule the State, and state the rule: "ladies first".
1 Blessed are they that believe they are blessed.
1 You can cage a swallow, can't you, but you can't swallow a cage, can you?
1 Mind your own business: Own your mind.
1 Rode, and rode, and rode, and rode, and rode, and rode, and rode!
1 Clatter and hum and crunch, and crunch and hum and clatter.
	0 Mind your own business.
1 All for one, and one for all!
1 Escher, drawing hands, drew hands drawing Escher.
```

## Lab-4
### main.cpp
```cpp
// main test driver for BST
// Created by Frank M. Carrano and Tim Henry.
// modified by Xia Hua.

#include "BinarySearchTree.h"// BST ADT
#include "Queue.h"
#include "Stack.h"
#include <iostream>
#include <string>
#include <fstream>
#include <iomanip>
using namespace std;

// display function to pass to BST traverse functions
void display(string & anItem)
{
    cout << anItem ;
    unsigned long le = anItem.length();
    if (isalpha(anItem[le-1]))
        cout << endl;
}

void check(bool success)
{
    if (success)
        cout << "Done." << endl;
    else
        cout << " Entry not in tree." << endl;
}
/////////////////////////////////////////////////////////////////
void printmenu();
void about();
void exitinfo();


/*************************************************************************
 
                            Main Funcion
 
 *************************************************************************/

int main()
{
    char choice;
    ifstream infile;
    bool success;
    string num, name;
    
    
/*************************************************************************/
    BinarySearchTree<string>* tree = new BinarySearchTree<string>();
/*************************************************************************/
    
    
    infile.open("employees.txt");
    if (infile.is_open())
    {
        string ID,name;
        while (!infile.eof())
        {
            infile >> ID;
            getline(infile,name);
            tree->insert(ID, name);
        }
    }
    else
    {
        cout << "Error openning file. Check your file is ready to open?\n ";
        exit(111);//exit the program with error code 111
    }
    
    /////////////////////////////////////////////////////////////////
    printmenu();
    
    while(choice != 'Q')
    {
        cout << "Please Enter Your Choice: ";
        cin >> choice;
        
        switch (choice)
        {
            case 'S':
            {
                cout << "Enter the unique key : ";
                cin >> num;
                if (tree->getEntry(num, name) == 1)
                    cout <<"Found the data: "<< num << name <<endl<< endl;
                else
                    cout << "Data not found "<<endl<<endl;
                break;
            }
            case 'D':
            {
                cout << "Inorder Traversals"<<endl;
                tree->inOrder(display);
                cout << "\n\nPostorder Traversals"<<endl;
                tree->postOrder(display);
                cout << "\n\nPreorder Traversals"<<endl;
                tree->preOrder(display);
                cout << endl << endl;
                break;
            }
            case 'B':
            {
                tree->breadth(display);
                cout << endl;
                break;
            }
            case 'G':
            {
                cout << "Enter the unique key : ";
                cin >> num;
                success = tree->remove(num);
                check(success);
                cout << endl;
                tree->display_tree();
                cout << endl;
                break;
            }
            case 'T':
            {
                tree->display_tree();
                cout << endl;
                break;
            }
            case 'M':
            {
                printmenu();
                cout << endl;
                break;
            }
            case 'A':
            {
                about();
                cout << endl;
                break;
            }
            case 'Q':
            {
                exitinfo();
                cout << endl;
                return 0;
            }
            default:
            {
                cout << "Please reenter a vaild command!!" << endl;
            }
        }
    }
    infile.close();
    return 0;
}

void printmenu()
{
    cout<<"**********************************************************************************"<<endl;
    cout<<"\t\t\t\t\t\tBinary Search Trees Program"<<endl;
    cout<<"Course: CIS 22C De Anza College Fall 2016                Developer: Xia Hua       "<<endl;
    cout<<"**********************************************************************************"<<endl;
    cout<<" S. Search by a unique key (employee identification number)"<<endl;
    cout<<" D. Recursive Depth-First Traversals: inorder, preorder, postorder"<<endl;
    cout<<" B. Tree Breadth-First Traversal: Print by level"<<endl;
    cout<<" T. Print tree as an indented list (show level numbers)"<<endl;
    cout<<" G. Delete the leaves"<<endl;
    cout<<" M. Display Menu"<<endl;
    cout<<" Q. Quit"<<endl;
    cout<<"**********************************************************************************"<<endl<<endl;
}

void about()
{
    cout << "____Developer Information_____"<<endl;
    cout << "\n|Developer Information\n|Name: Xia Hua\n|Class: CIS 22C\n|Quater: Fall\n|Year: 2016\n|College: De Anza College" << endl;
    cout << "______________________________"<<endl<<endl;
}

void exitinfo()
{
    cout << "Thanks using our program. Your file will be saved on BST_Output.txt at the same folder!" << endl;
}

/**********************************************************************************************************************
                Output
 
 **********************************************************************************
 Binary Search Trees Program
 Course: CIS 22C De Anza College Fall 2016                Developer: Xia Hua
 **********************************************************************************
 S. Search by a unique key (employee identification number)
 D. Recursive Depth-First Traversals: inorder, preorder, postorder
 B. Tree Breadth-First Traversal: Print by level
 T. Print tree as an indented list (show level numbers)
 G. Delete the leaves
 M. Display Menu
 Q. Quit
 **********************************************************************************
 
 Please Enter Your Choice: D
 Inorder Traversals
 1011 Ashley McMullen
 1022 John Plemmons
 2066 Sophia Williams
 2077 Bill Twain
 3022 Duo Xue
 3055 Tim Nguyen
 3088 Josh Smith
 3099 Adriana Ho
 4033 Dale Mehta
 4033 Dale Mehta
 5044 Debbie Lancaster
 
 
 Postorder Traversals
 1011 Ashley McMullen
 2066 Sophia Williams
 2077 Bill Twain
 1022 John Plemmons
 3055 Tim Nguyen
 3088 Josh Smith
 4033 Dale Mehta
 4033 Dale Mehta
 5044 Debbie Lancaster
 3099 Adriana Ho
 3022 Duo Xue
 
 
 Preorder Traversals
 3022 Duo Xue
 1022 John Plemmons
 1011 Ashley McMullen
 2077 Bill Twain
 2066 Sophia Williams
 3099 Adriana Ho
 3088 Josh Smith
 3055 Tim Nguyen
 5044 Debbie Lancaster
 4033 Dale Mehta
 4033 Dale Mehta
 
 
 Please Enter Your Choice: S 3022
 Enter the unique key : Found the data: 3022 Duo Xue
 
 Please Enter Your Choice: S 1022
 Enter the unique key : Found the data: 1022 John Plemmons
 
 Please Enter Your Choice: M
 **********************************************************************************
 Binary Search Trees Program
 Course: CIS 22C De Anza College Fall 2016                Developer: Xia Hua
 **********************************************************************************
 S. Search by a unique key (employee identification number)
 D. Recursive Depth-First Traversals: inorder, preorder, postorder
 B. Tree Breadth-First Traversal: Print by level
 T. Print tree as an indented list (show level numbers)
 G. Delete the leaves
 M. Display Menu
 Q. Quit
 **********************************************************************************
 
 
 Please Enter Your Choice: B
 3022 Duo Xue
 1022 John Plemmons
 3099 Adriana Ho
 1011 Ashley McMullen
 2077 Bill Twain
 3088 Josh Smith
 5044 Debbie Lancaster
 2066 Sophia Williams
 3055 Tim Nguyen
 4033 Dale Mehta
 4033 Dale Mehta
 
 Please Enter Your Choice: T
 
 3. 5044 Debbie Lancaster
 5. 4033 Dale Mehta
 4. 4033 Dale Mehta
 2. 3099 Adriana Ho
 3. 3088 Josh Smith
 4. 3055 Tim Nguyen
 1. 3022 Duo Xue
 3. 2077 Bill Twain
 4. 2066 Sophia Williams
 2. 1022 John Plemmons
 3. 1011 Ashley McMullen
 Please Enter Your Choice: G3022
 Enter the unique key :  Entry not in tree.
 
 
 3. 5044 Debbie Lancaster
 5. 4033 Dale Mehta
 4. 4033 Dale Mehta
 2. 3099 Adriana Ho
 3. 3088 Josh Smith
 4. 3055 Tim Nguyen
 1. 3022 Duo Xue
 3. 2077 Bill Twain
 4. 2066 Sophia Williams
 2. 1022 John Plemmons
 3. 1011 Ashley McMullen
 Please Enter Your Choice: G 3022
 Enter the unique key : Done.
 
 
 3. 5044 Debbie Lancaster
 5. 4033 Dale Mehta
 4. 4033 Dale Mehta
 2. 3099 Adriana Ho
 3. 3088 Josh Smith
 1. 3055 Duo Xue
 3. 2077 Bill Twain
 4. 2066 Sophia Williams
 2. 1022 John Plemmons
 3. 1011 Ashley McMullen
 Please Enter Your Choice: G 3055
 Enter the unique key : Done.
 
 
 3. 5044 Debbie Lancaster
 5. 4033 Dale Mehta
 4. 4033 Dale Mehta
 2. 3099 Adriana Ho
 1. 3088 Duo Xue
 3. 2077 Bill Twain
 4. 2066 Sophia Williams
 2. 1022 John Plemmons
 3. 1011 Ashley McMullen
 Please Enter Your Choice: G 3088
 Enter the unique key : Done.
 
 
 2. 5044 Debbie Lancaster
 4. 4033 Dale Mehta
 3. 4033 Dale Mehta
 1. 3099 Duo Xue
 3. 2077 Bill Twain
 4. 2066 Sophia Williams
 2. 1022 John Plemmons
 3. 1011 Ashley McMullen
 Please Enter Your Choice: M
 **********************************************************************************
 Binary Search Trees Program
 Course: CIS 22C De Anza College Fall 2016                Developer: Xia Hua
 **********************************************************************************
 S. Search by a unique key (employee identification number)
 D. Recursive Depth-First Traversals: inorder, preorder, postorder
 B. Tree Breadth-First Traversal: Print by level
 T. Print tree as an indented list (show level numbers)
 G. Delete the leaves
 M. Display Menu
 Q. Quit
 **********************************************************************************
 
 
 Please Enter Your Choice: A
 ____Developer Information_____
 
 |Developer Information
 |Name: Xia Hua
 |Class: CIS 22C
 |Quater: Fall
 |Year: 2016
 |College: De Anza College
 ______________________________
 
 
 Please Enter Your Choice: Q
 Thanks using our program. Your file will be saved on BST_Output.txt at the same folder!
 */
```

### Emplyee.h
```cpp
//
//  Employee.h
//  HW4
//
//  Created by Rednik Tony on 11/11/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//

#ifndef Employee_h
#define Employee_h
#include <iostream>
#include <string>
#include <fstream>
#include <sstream>
#include <iomanip>
#include <vector>

template<class T>
class DataTree
{
private:
    ifstream inFile;
    BinarySearchTree<T> tree;
    
public:
    DataTree(){};
    DataTree(string filename);
    void display(T &anItem){cout<<" "<<anItem<<endl;}
    void print(){tree.indented();}
    void breadth()
    {
        cout << "\nBreadth First Traversal:\n";
        tree.breadth();
    }
    void inOrder()
    {
        cout << "\nIn-Order Traversal:\n";
        tree.inOrder(display);
    }
    void preOrder()
    {
        cout << "\nPre-Order Traversal:\n";
        tree.preOrder(display);
    }
    void postOrder()
    {
        cout << "\nPost-Order Traversal:\n";
        tree.postOrder(display);
    }
    void deleteLeaves()
    {
        cout << "\nDeleting all leaves...";
        (tree.deleteLeaves()) ? (cout << "Success!\n") : (cout << "Failed, only root remains.\n");
    }
    
    bool search(int num)
    {
        T target(num, "null");
        Employee result;
        if(empTree.getEntry(target, result)){
            cout << "\nFound!: " << result << "\n";
            return true;
        }
        cout << "\nNot found.\n";
        return false;
        
    }
};
#endif /* Employee_h */
```

### BinaryNode.h
```cpp
// Node for a binary tree
// Created by Frank M. Carrano and Tim Henry.
// Modified by Xia Hua 

#ifndef _BINARY_NODE
#define _BINARY_NODE

#include <string>
using namespace std;
template<class ItemType>
class BinaryNode
{
private:
    ItemType              item;         // Data portion
    string name;
    BinaryNode<ItemType>* leftPtr;		// Pointer to left child
    BinaryNode<ItemType>* rightPtr;		// Pointer to right child
    
public:
    ///////////////////////////////////////////////////////////////////// constructors
    BinaryNode(const ItemType & anItem, const string & anName)
    {
        item = anItem; name = anName; leftPtr = 0; rightPtr = 0;
    }
    BinaryNode(const ItemType & anItem, const string & anName,
               BinaryNode<ItemType>* left,
               BinaryNode<ItemType>* right)
    {
        item = anItem;name = anName; leftPtr = left; rightPtr = right;
    }
    ////////////////////////////////////////////////////////////////////////// accessors
    void setItem(const ItemType & anItem)
    {
        item = anItem;
    }
    void setname(const string & anName)
    {
        name = anName;
    }
    void setLeftPtr(BinaryNode<ItemType>* left)
    {
        leftPtr = left;
    }
    void setRightPtr(BinaryNode<ItemType>* right)
    {
        rightPtr = right;
    }
    /////////////////////////////////////////////////////////// mutators
    ItemType getItem() const
    {
        return item;
    }
    string getName() const
    {
        return name;
    }
    BinaryNode<ItemType>* getLeftPtr() const
    {
        return leftPtr;
    }
    BinaryNode<ItemType>* getRightPtr() const
    {
        return rightPtr;
    }

    bool isLeaf() const {return (leftPtr == 0 && rightPtr == 0);}
};

#endif
```

### BinaryTree.h
```cpp
#ifndef _BINARY_TREE
#define _BINARY_TREE
#include "BinaryNode.h"
#include "Queue.h"
#include <cstring>
#include <iostream>
#include <cmath>
#include <string>
#include <fstream>
#include <cstdlib>
#include <sstream>
#include <iomanip>
using namespace std;

template<class ItemType>
class BinaryTree
{
protected:
    BinaryNode<ItemType>* rootPtr;		// ptr to root node
    int count;							// number of nodes in tree
    
public:
    // "admin" functions
    BinaryTree() {rootPtr = 0; count = 0;}
    BinaryTree(const BinaryTree<ItemType> & tree)
    {
        rootPtr = copyTree(tree.rootPtr);
    }
    virtual ~BinaryTree() { }
    BinaryTree & operator = (const BinaryTree & sourceTree);
    
    // common functions for all binary trees
    bool isEmpty() const	{return count == 0;}
    int size() const	    {return count;}
    void clear()			{destroyTree(rootPtr); rootPtr = 0; count = 0;}
    void preOrder(void visit(ItemType &)) const {_preorder(visit, rootPtr);}
    void inOrder(void visit(ItemType &)) const  {_inorder(visit, rootPtr);}
    void postOrder(void visit(ItemType &)) const{_postorder(visit, rootPtr);}
    void breadth(void visit(ItemType &)) const{_breadth(visit, rootPtr);}
    
    
    // abstract functions to be implemented by derived class
    virtual bool insert(const ItemType & newData, string name) = 0;
    virtual bool remove(const ItemType & data) = 0;
    virtual bool getEntry(const ItemType & anEntry, ItemType & returnedItem) const = 0;
    
    ////Display the tree
    void display_tree()
    {
        _display(this->rootPtr, 1);
    }
    void _display(BinaryNode<ItemType> *ptr, int level);
    
private:
    // delete all nodes from the tree
    void destroyTree(BinaryNode<ItemType>* nodePtr);
    
    // copy from the tree rooted at nodePtr and returns a pointer to the copy
    BinaryNode<ItemType>* copyTree(const BinaryNode<ItemType>* nodePtr);
    
    // internal traverse
    void _preorder(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const;
    void _inorder(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const;
    void _postorder(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const;
    void _breadth(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const;
    void printBreadthFirst( BinaryNode<ItemType>* nodePtr, Queue<BinaryNode<ItemType> *> *q, int level, void visit(ItemType anItem, int lvl));
    
    
    
};
//// Copy the tree function
template<class ItemType>
BinaryNode<ItemType>* BinaryTree<ItemType>::copyTree(const BinaryNode<ItemType>* nodePtr)
{
    
    BinaryNode<ItemType>* new_tree_ptr = nullptr;
    if (nodePtr != nullptr)
    {
        new_tree_ptr = new BinaryNode<ItemType>(nodePtr->getItem());
        new_tree_ptr->setItem(nodePtr->getItem());
        new_tree_ptr->setname(nodePtr->getName());
        new_tree_ptr->setLeftPtr(copyTree(nodePtr->getLeftPtr()));
        new_tree_ptr->setRightPtr(copyTree(nodePtr->getRightPtr()));
    }  // end if
    return new_tree_ptr;
}

template<class ItemType>
void BinaryTree<ItemType>::destroyTree(BinaryNode<ItemType>* nodePtr)
{
    if (nodePtr != nullptr)
    {
        destroyTree(nodePtr->getLeftPtr());
        destroyTree(nodePtr->getRightPtr());
        delete nodePtr;
    } // end if
}

template<class ItemType>
void BinaryTree<ItemType>:: _display(BinaryNode<ItemType> *ptr, int level)
{
    
    int i;
    if (ptr != NULL)
    {
        _display(ptr->getRightPtr(), level + 1);
        cout<<""<<endl;
        for (i = 0; i < level && ptr != rootPtr; i++)
            cout << "\t\t\t\t";
        cout <<level<<". "<< ptr->getItem() << ptr->getName();
        _display(ptr->getLeftPtr(), level + 1);
    } // end if
}
/*************************************************************************
 
                                Order Funcions
 
 *************************************************************************/
template<class ItemType>
void BinaryTree<ItemType>::_preorder(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const
{
    if (nodePtr != 0)
    {
        ItemType item = nodePtr->getItem();
        string name = nodePtr->getName();
        visit(item);
        visit(name);
        _preorder(visit, nodePtr->getLeftPtr());
        _preorder(visit, nodePtr->getRightPtr());
    }
}

template<class ItemType>
void BinaryTree<ItemType>::_inorder(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const
{
    if (nodePtr != nullptr)
    {
        _inorder(visit, nodePtr->getLeftPtr());
        ItemType item = nodePtr->getItem();
        string name = nodePtr->getName();
        visit(item);
        visit(name);
        _inorder(visit, nodePtr->getRightPtr());
    }
}

template<class ItemType>
void BinaryTree<ItemType>::_postorder(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const
{
    if (nodePtr != nullptr)
    {
        _postorder(visit, nodePtr->getLeftPtr());
        _postorder(visit, nodePtr->getRightPtr());
        ItemType item = nodePtr->getItem();
        string name = nodePtr->getName();
        visit(item);
        visit(name);
    } 
}
/*************************************************************************
 
                            Breadth Funcion
 
 *************************************************************************/
template<class ItemType>
void BinaryTree<ItemType>::_breadth(void visit(ItemType &), BinaryNode<ItemType>* nodePtr) const
{
    
    if(nodePtr == nullptr)
        return;
    Queue<BinaryNode<ItemType>*> q;
    q.enqueue(nodePtr);
    while(!q.isEmpty())
    {
        BinaryNode<ItemType>* node;
        q.dequeue(node);
        ItemType item = node->getItem();
        string name = node->getName();
        visit(item);
        visit(name);
        if(node->getLeftPtr() != nullptr)
            q.enqueue(node->getLeftPtr());
        if(node->getRightPtr() != nullptr)
            q.enqueue(node->getRightPtr());
    } // end while
}

//Print the tree Tree Breadth-First Traversal, Print by level.
template<class ItemType>
void BinaryTree<ItemType>::printBreadthFirst( BinaryNode<ItemType>* nodePtr, Queue<BinaryNode<ItemType> *> *q,
                                             int level, void visit(ItemType anItem, int lvl))
{
    q->dequeue(nodePtr);
    float n = round(sqrt(level));
    
    visit(nodePtr->getItem(), n);
    visit(nodePtr->getName(), n);
    
    if (nodePtr != NULL && !nodePtr->isLeaf()){
        if (nodePtr->getLeftPtr())
        {
            q->enqueue(nodePtr->getLeftPtr());
        }
        
        if (nodePtr->getRightPtr())
        {
            q->enqueue(nodePtr->getRightPtr());
        }
    }
    if( q->getCount() == 0) return;
    printBreadthFirst(nodePtr, q, level+1, visit);
}

template<class ItemType>
BinaryTree<ItemType> & BinaryTree<ItemType>::operator=(const BinaryTree<ItemType> & sourceTree)
{
    
}

#endif
```

### BinarySearchTree.h
```cpp
// Binary Search Tree ADT
// Created by Frank M. Carrano and Tim Henry.
// Modified by: Xia Hua

#ifndef _BINARY_SEARCH_TREE
#define _BINARY_SEARCH_TREE
#include <string>
using namespace std;
#include "BinaryTree.h"

template<class ItemType>
class BinarySearchTree : public BinaryTree<ItemType>
{
private:
    // internal insert node: insert newNode in nodePtr subtree
    BinaryNode<ItemType>* _insert(BinaryNode<ItemType>* nodePtr, BinaryNode<ItemType>* newNode);
    
    // internal remove node: locate and delete target node under nodePtr subtree
    BinaryNode<ItemType>* _remove(BinaryNode<ItemType>* nodePtr, const ItemType target, bool & success);
    
    // delete target node from tree, called by internal remove node
    BinaryNode<ItemType>* deleteNode(BinaryNode<ItemType>* targetNodePtr);
    
    // remove the leftmost node in the left subtree of nodePtr
    BinaryNode<ItemType>* removeLeftmostNode(BinaryNode<ItemType>* nodePtr, ItemType & successor);
    
    // search for target node
    BinaryNode<ItemType>* findNode(BinaryNode<ItemType>* treePtr, const ItemType & target) const;
    
public:
    // insert a node at the correct location
    bool insert(const ItemType & newEntry, string name);
    // remove a node if found
    bool remove(const ItemType & anEntry);
    // find a target node
    bool getEntry(const ItemType & target, string & returnedItem) const;
    
    
};


///////////////////////// public function definitions ///////////////////////////

template<class ItemType>
bool BinarySearchTree<ItemType>::insert(const ItemType & newEntry, string name)
{
    BinaryNode<ItemType>* newNodePtr = new BinaryNode<ItemType>(newEntry,name);
    this->rootPtr = _insert(this->rootPtr, newNodePtr);
    return true;
}

template<class ItemType>
bool BinarySearchTree<ItemType>::remove(const ItemType & target)
{
    bool isSuccessful = false;
    this->rootPtr = _remove(this->rootPtr, target, isSuccessful);
    return isSuccessful;
}
/*************************************************************************
 
                            GetEntry Funcions
 
 *************************************************************************/
template<class ItemType>
bool BinarySearchTree<ItemType>::getEntry(const ItemType& anEntry, string & returnedItem) const
{
    BinaryNode<ItemType> *obj;
    if ((obj=findNode(this->rootPtr, anEntry)) != NULL)
    {
        returnedItem=obj->getName();
        return true;
    }
    return false;
}

//////////////////////////// private functions ////////////////////////////////////////////
/*************************************************************************
 
                            Insert Funcions
 
 *************************************************************************/
template<class ItemType>
BinaryNode<ItemType>* BinarySearchTree<ItemType>::_insert(BinaryNode<ItemType>* nodePtr,BinaryNode<ItemType>* newNodePtr)
{
    if (nodePtr == NULL)
    {
        return newNodePtr;
    }
    else if (nodePtr->getItem() > newNodePtr->getItem())
    {
        BinaryNode<ItemType>* tempPtr = _insert(nodePtr->getLeftPtr(), newNodePtr);
        nodePtr->setLeftPtr(tempPtr);
    }
    else // if (nodePtr->getItem() < newNodePtr->getItem())
    {
        BinaryNode<ItemType>* tempPtr = _insert(nodePtr->getRightPtr(), newNodePtr);
        nodePtr->setRightPtr(tempPtr);
    }
    return nodePtr;
}
/*************************************************************************
 
                            Remove Funcions
 
 *************************************************************************/
template<class ItemType>
BinaryNode<ItemType>* BinarySearchTree<ItemType>::_remove(BinaryNode<ItemType>* nodePtr,const ItemType target,bool & success)

{
    if (nodePtr == 0)
    {
        success = false;
        return 0;
    }
    if (nodePtr->getItem() > target)
        nodePtr->setLeftPtr(_remove(nodePtr->getLeftPtr(), target, success));
    else if (nodePtr->getItem() < target)
        nodePtr->setRightPtr(_remove(nodePtr->getRightPtr(), target, success));
    else
    {
        nodePtr = deleteNode(nodePtr);
        success = true;
    }
    return nodePtr;
}
/*************************************************************************
 
                            DeleteNode Funcions
 
 *************************************************************************/
template<class ItemType>
BinaryNode<ItemType>* BinarySearchTree<ItemType>::deleteNode(BinaryNode<ItemType>* nodePtr)
{
    if (nodePtr->isLeaf())
    {
        delete nodePtr;
        nodePtr = 0;
        return nodePtr;
    }
    else if (nodePtr->getLeftPtr() == 0)
    {
        BinaryNode<ItemType>* nodeToConnectPtr = nodePtr->getRightPtr();
        delete nodePtr;
        nodePtr = 0;
        return nodeToConnectPtr;
    }
    else if (nodePtr->getRightPtr() == 0)
    {
        BinaryNode<ItemType>* nodeToConnectPtr = nodePtr->getLeftPtr();
        delete nodePtr;
        nodePtr = 0;
        return nodeToConnectPtr;
    }
    else
    {
        ItemType newNodeValue;
        nodePtr->setRightPtr(removeLeftmostNode(nodePtr->getRightPtr(), newNodeValue));
        nodePtr->setItem(newNodeValue);
        return nodePtr;
    }
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

template<class ItemType>
BinaryNode<ItemType>* BinarySearchTree<ItemType>::removeLeftmostNode(BinaryNode<ItemType>* nodePtr,ItemType & successor)
{
    if (nodePtr->getLeftPtr() == 0)
    {
        successor = nodePtr->getItem();
        return deleteNode(nodePtr);
    }
    else
    {
        nodePtr->setLeftPtr(removeLeftmostNode(nodePtr->getLeftPtr(), successor));
        return nodePtr;
    }
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

template<class ItemType>
BinaryNode<ItemType>* BinarySearchTree<ItemType>::findNode(BinaryNode<ItemType>* nodePtr,const ItemType & target) const
{
    if (nodePtr == NULL)
    {
        return NULL;
    }
    else if (nodePtr->getItem() == target)
    {
        return nodePtr;
    }
    else if (nodePtr->getItem() > target)
    {
        return findNode(nodePtr->getLeftPtr(), target);
    }
    else // if (nodePtr->getItem() < target)
    {
        return findNode(nodePtr->getRightPtr(), target);
    }
}
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
#endif

```

### Stack.h
```cpp
/**~*~*
 Stack template
 *~**/
#ifndef DYNAMICSTACK_H
#define DYNAMICSTACK_H
#include <iostream>
using namespace std;

template <class T>
class Stack
{
private:
    // Structure for the stach nodes
    struct StackNode
    {
        T value;          // Value in the node
        StackNode *next;  // Pointer to next node
    };
    
    StackNode *top;     // Pointer to the stack top
    int count;
    
public:
    //Constructor
    Stack(){top = NULL; count = 0;}
    
    // Destructor
    ~Stack();
    
    // Stack operations
    bool push(T);
    bool pop(T &);
    bool isEmpty();
    // getCount()
    // getTop()
};

/**~*~*
 Destructor
 *~**/
template <class T>
Stack<T>::~Stack()
{
    StackNode *currNode, *nextNode;
    
    // Position nodePtr at the top of the stack.
    currNode = top;
    
    // Traverse the list deleting each node.
    while (currNode) //while (currNode != NULL)
    {
        nextNode = currNode->next;
        delete currNode;
        currNode = nextNode;
    }
}

/**~*~*
 Member function push pushes the argument onto
 the stack.
 *~**/
template <class T>
bool Stack<T>::push(T item)
{
    StackNode *newNode; // Pointer to a new node
    
    // Allocate a new node and store num there.
    newNode = new StackNode;
    if (!newNode)
        return false;
    newNode->value = item;
    
    // Update links and counter
    newNode->next = top;
    top = newNode;
    count++;
    
    return true;
}

/**~*~*
 Member function pop pops the value at the top
 of the stack off, and copies it into the variable
 passed as an argument.
 *~**/
template <class T>
bool Stack<T>::pop(T &item)
{
    StackNode *temp; // Temporary pointer
    
    // empty stack
    if (count == 0)
        return false;
    
    // pop value off top of stack
    item = top->value;
    temp = top->next;
    delete top;
    top = temp;
    count--;
    
    return true;
}

/**~*~*
 Member function isEmpty returns true if the stack
 is empty, or false otherwise.
 *~**/
template <class T>
bool Stack<T>::isEmpty()
{
    return count == 0;
}
#endif

```

### Queue.h
```cpp
/**~*~*
 Queue template
 *~**/
#ifndef DYNAMICQUEUE_H
#define DYNAMICQUEUE_H
#include <iostream>
using namespace std;

template <class T>
class Queue
{
private:
    // Structure for the queue nodes
    struct QueueNode
    {
        T value;          // Value in the node
        QueueNode *next;  // Pointer to next node
    };
    
    QueueNode *front;    // Pointer to the queue front
    QueueNode *rear;     // Pointer to the queue rear
    int count;
    
public:
    //Constructor
    Queue(){front = rear = NULL; count = 0;}
    
    // Destructor
    ~Queue();
    
    // Stack operations
    bool enqueue(T);
    bool dequeue(T &);
    bool isEmpty();
    int  getCount();
    bool queueFront(T &);
    bool queueRear(T &);
};

/**~*~*
 Destructor
 *~**/
template <class T>
Queue<T>::~Queue()
{
    QueueNode *currNode, *nextNode;
    
    // Position nodePtr at the top of the stack.
    currNode = front;
    
    // Traverse the list deleting each node.
    while (currNode) //while (currNode != NULL)
    {
        nextNode = currNode->next;
        delete currNode;
        currNode = nextNode;
    }
}


/**~*~*
 Member function getCount returns
 the number of elements in the queue
 *~**/
template <class T>
int Queue<T>::getCount()
{
    return count;
}

/**~*~*
 Member function isEmpty returns true if the stack
 is empty, or false otherwise.
 *~**/
template <class T>
bool Queue<T>::isEmpty()
{
    return count == 0;
}

/**~*~*
 Member function enqueue inserts the argument into
 the queue.
 *~**/
template <class T>
bool Queue<T>::enqueue(T item)
{
    QueueNode *newNode; // Pointer to a new node
    
    // Allocate a new node and store num there.
    newNode = new QueueNode;
    if (!newNode)
        return false;
    newNode->value = item;
    
    // Update links and counter
    newNode->next = NULL;
    
    if( front == NULL )        // insert to an empty queue
        front = newNode;
    else
        rear->next = newNode;
    
    count++;
    rear = newNode;
    
    return true;
}

/**~*~*
 Member function dequeue deletes the value at the front
 of the queue, and copies it into the variable
 passed as an argument.
 *~**/
template <class T>
bool Queue<T>::dequeue(T &item)
{
    QueueNode *pDel; // Temporary pointer
    
    // empty queue
    if (count == 0)
        return false;
    
    // delete the value at the front of the queue
    item = front->value;
    pDel = front;
    
    if( count == 1 )
        rear = front = NULL;
    else
        front = front->next;
    
    count--;
    delete pDel;
    
    return true;
}

/**~*~*
 Member function queueFront copies the value at the front
 of the queue into the variable passed as an argument.
 *~**/
template <class T>
bool Queue<T>::queueFront(T &item)
{
    if( front == NULL )
        return false;
    
    item = front->value;
    
    return true;
}

/**~*~*
 Member function queueRear copies the value at the rear
 of the queue into the variable passed as an argument.
 *~**/
template <class T>
bool Queue<T>::queueRear(T &item)
{
    if( rear == NULL )
        return false;
    
    item = rear->value;
    return false;
}

#endif

```

### employees.txt
```cpp
3022 Duo Xue
3099 Adriana Ho
1022 John Plemmons
2077 Bill Twain
2066 Sophia Williams
3088 Josh Smith
1011 Ashley McMullen
3055 Tim Nguyen
5044 Debbie Lancaster
4033 Dale Mehta
```


### BST_Output.txt
```cpp
**********************************************************************************
						Binary Search Trees Program
Course: CIS 22C De Anza College Fall 2016                Developer: Xia Hua       
**********************************************************************************
 S. Search by a unique key (employee identification number)
 D. Recursive Depth-First Traversals: inorder, preorder, postorder
 B. Tree Breadth-First Traversal: Print by level
 T. Print tree as an indented list (show level numbers)
 G. Delete the leaves
 M. Display Menu
 Q. Quit
**********************************************************************************

Please Enter Your Choice: D
Inorder Traversals
1011 Ashley McMullen
1022 John Plemmons
2066 Sophia Williams
2077 Bill Twain
3022 Duo Xue
3055 Tim Nguyen
3088 Josh Smith
3099 Adriana Ho
4033 Dale Mehta
4033 Dale Mehta
5044 Debbie Lancaster


Postorder Traversals
1011 Ashley McMullen
2066 Sophia Williams
2077 Bill Twain
1022 John Plemmons
3055 Tim Nguyen
3088 Josh Smith
4033 Dale Mehta
4033 Dale Mehta
5044 Debbie Lancaster
3099 Adriana Ho
3022 Duo Xue


Preorder Traversals
3022 Duo Xue
1022 John Plemmons
1011 Ashley McMullen
2077 Bill Twain
2066 Sophia Williams
3099 Adriana Ho
3088 Josh Smith
3055 Tim Nguyen
5044 Debbie Lancaster
4033 Dale Mehta
4033 Dale Mehta


Please Enter Your Choice: S 3022
Enter the unique key : Found the data: 3022 Duo Xue

Please Enter Your Choice: S 1022
Enter the unique key : Found the data: 1022 John Plemmons

Please Enter Your Choice: M
**********************************************************************************
						Binary Search Trees Program
Course: CIS 22C De Anza College Fall 2016                Developer: Xia Hua       
**********************************************************************************
 S. Search by a unique key (employee identification number)
 D. Recursive Depth-First Traversals: inorder, preorder, postorder
 B. Tree Breadth-First Traversal: Print by level
 T. Print tree as an indented list (show level numbers)
 G. Delete the leaves
 M. Display Menu
 Q. Quit
**********************************************************************************


Please Enter Your Choice: B
3022 Duo Xue
1022 John Plemmons
3099 Adriana Ho
1011 Ashley McMullen
2077 Bill Twain
3088 Josh Smith
5044 Debbie Lancaster
2066 Sophia Williams
3055 Tim Nguyen
4033 Dale Mehta
4033 Dale Mehta

Please Enter Your Choice: T

												3. 5044 Debbie Lancaster
																				5. 4033 Dale Mehta
																4. 4033 Dale Mehta
								2. 3099 Adriana Ho
												3. 3088 Josh Smith
																4. 3055 Tim Nguyen
1. 3022 Duo Xue
												3. 2077 Bill Twain
																4. 2066 Sophia Williams
								2. 1022 John Plemmons
												3. 1011 Ashley McMullen
Please Enter Your Choice: G3022 
Enter the unique key :  Entry not in tree.


												3. 5044 Debbie Lancaster
																				5. 4033 Dale Mehta
																4. 4033 Dale Mehta
								2. 3099 Adriana Ho
												3. 3088 Josh Smith
																4. 3055 Tim Nguyen
1. 3022 Duo Xue
												3. 2077 Bill Twain
																4. 2066 Sophia Williams
								2. 1022 John Plemmons
												3. 1011 Ashley McMullen
Please Enter Your Choice: G 3022
Enter the unique key : Done.


												3. 5044 Debbie Lancaster
																				5. 4033 Dale Mehta
																4. 4033 Dale Mehta
								2. 3099 Adriana Ho
												3. 3088 Josh Smith
1. 3055 Duo Xue
												3. 2077 Bill Twain
																4. 2066 Sophia Williams
								2. 1022 John Plemmons
												3. 1011 Ashley McMullen
Please Enter Your Choice: G 3055
Enter the unique key : Done.


												3. 5044 Debbie Lancaster
																				5. 4033 Dale Mehta
																4. 4033 Dale Mehta
								2. 3099 Adriana Ho
1. 3088 Duo Xue
												3. 2077 Bill Twain
																4. 2066 Sophia Williams
								2. 1022 John Plemmons
												3. 1011 Ashley McMullen
Please Enter Your Choice: G 3088
Enter the unique key : Done.


								2. 5044 Debbie Lancaster
																4. 4033 Dale Mehta
												3. 4033 Dale Mehta
1. 3099 Duo Xue
												3. 2077 Bill Twain
																4. 2066 Sophia Williams
								2. 1022 John Plemmons
												3. 1011 Ashley McMullen
Please Enter Your Choice: M
**********************************************************************************
						Binary Search Trees Program
Course: CIS 22C De Anza College Fall 2016                Developer: Xia Hua       
**********************************************************************************
 S. Search by a unique key (employee identification number)
 D. Recursive Depth-First Traversals: inorder, preorder, postorder
 B. Tree Breadth-First Traversal: Print by level
 T. Print tree as an indented list (show level numbers)
 G. Delete the leaves
 M. Display Menu
 Q. Quit
**********************************************************************************


Please Enter Your Choice: A
____Developer Information_____

|Developer Information
|Name: Xia Hua
|Class: CIS 22C
|Quater: Fall
|Year: 2016
|College: De Anza College
______________________________


Please Enter Your Choice: Q
Thanks using our program. Your file will be saved on BST_Output.txt at the same folder!
```

## Lab-5
### main.cpp
```cpp
//
//  Customer.h
//  HW5
//
//  Created by Rednik Tony on 12/2/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//
#include <vector>
#include <iostream>
#include <fstream>
#include <string>


#include "priorityQueue.h"
#include "Customer.h"

using namespace std;

void readData(Customer,priorityQueue *);

int main()
{
    Customer customers;
    priorityQueue *heap = new priorityQueue;
    readData(customers,heap);
    cout << endl;
    cout << "================================================================="<<endl;
    cout << "\nFinal Sorted Priority List(based on serial number): \n";
    //here is the main process of the function
    heap->print();
    heap->treeGraph();
    //interface ends
    cout << "****************************************************************************************************************************************************************************************"<<endl;
    cout << "Thanks for using this program.\n";
    cout << "****************************************************************************************************************************************************************************************"<<endl;
    delete heap;
    return 0;
}

void readData(Customer customers,priorityQueue *heap)
{
    const string fileName = "overbooked.txt";
    ifstream inFile;
    inFile.open(fileName);
    //default setting
    int year = 0;
    int mile = 0;
    int sequence = 1;
    
    string name;
    int priority;
    
    if (!inFile)
    {
        cout << "File error. Check your file is on correct location!"<<endl;
        cout << "========================================================="<<endl;
        exit(111);
    }
    while (!inFile.eof())
    {
        inFile >> year;
        inFile >> mile;
        priority = mile/1000+year-sequence;
        int serialNumber = priority * 100 + (100 - sequence);
        getline(inFile, name);
        //call setters
        customers.setPriority(priority);
        customers.setSerialNumber(serialNumber);
        customers.setYears(year);
        customers.setName(name);
        customers.setMileage(mile);
        //insert to queue
        heap->enqueue(customers);
        //counter add
        sequence++;
    }
    inFile.close();
}

//output
/*
 
 Now Inserting........
 
 Customer Name:  Robert Hill Priority Number: 57 Serial Number: 5799
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.       Robert Hill			 57				5799
 =================================================================
 Now Inserting........
 
 Customer Name:  Amanda Trapp Priority Number: 90 Serial Number: 9098
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.      Amanda Trapp			 90				9098
 2.       Robert Hill			 57				5799
 =================================================================
 Now Inserting........
 
 Customer Name:  Jonathan Nguyen Priority Number: 93 Serial Number: 9397
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.       Robert Hill			 57				5799
 3.      Amanda Trapp			 90				9098
 =================================================================
 Now Inserting........
 
 Customer Name:  Tom Martin Priority Number: 54 Serial Number: 5496
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.       Robert Hill			 57				5799
 3.      Amanda Trapp			 90				9098
 4.        Tom Martin			 54				5496
 =================================================================
 Now Inserting........
 
 Customer Name:  Mary Lou Gilley Priority Number: 13 Serial Number: 1395
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.       Robert Hill			 57				5799
 3.      Amanda Trapp			 90				9098
 4.        Tom Martin			 54				5496
 5.   Mary Lou Gilley			 13				1395
 =================================================================
 Now Inserting........
 
 Customer Name:  Bob Che Priority Number: 86 Serial Number: 8694
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.       Robert Hill			 57				5799
 3.      Amanda Trapp			 90				9098
 4.        Tom Martin			 54				5496
 5.   Mary Lou Gilley			 13				1395
 6.           Bob Che			 86				8694
 =================================================================
 Now Inserting........
 
 Customer Name:  Warren Rexroad Priority Number: 72 Serial Number: 7293
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.       Robert Hill			 57				5799
 3.      Amanda Trapp			 90				9098
 4.        Tom Martin			 54				5496
 5.   Mary Lou Gilley			 13				1395
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 =================================================================
 Now Inserting........
 
 Customer Name:  Vincent Gonzales Priority Number: 59 Serial Number: 5992
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.   Mary Lou Gilley			 13				1395
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 =================================================================
 Now Inserting........
 
 Customer Name:  Paula Hung Priority Number: 28 Serial Number: 2891
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.   Mary Lou Gilley			 13				1395
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 9.        Paula Hung			 28				2891
 =================================================================
 Now Inserting........
 
 Customer Name:  Lou Masson Priority Number: 17 Serial Number: 1790
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.        Lou Masson			 17				1790
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 =================================================================
 Now Inserting........
 
 Customer Name:  Steve Che Priority Number: 35 Serial Number: 3589
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 =================================================================
 Now Inserting........
 
 Customer Name:  Linda Lee Priority Number: 80 Serial Number: 8088
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 =================================================================
 Now Inserting........
 
 Customer Name:  Dave Lightfoot Priority Number: 53 Serial Number: 5387
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 =================================================================
 Now Inserting........
 
 Customer Name:  Sue Andrews Priority Number: 44 Serial Number: 4486
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 14.       Sue Andrews			 44				4486
 =================================================================
 Now Inserting........
 
 Customer Name:  Joanne Brown Priority Number: 20 Serial Number: 2085
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.  Vincent Gonzales			 59				5992
 3.      Amanda Trapp			 90				9098
 4.       Robert Hill			 57				5799
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.        Tom Martin			 54				5496
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 14.       Sue Andrews			 44				4486
 15.      Joanne Brown			 20				2085
 =================================================================
 Now Inserting........
 
 Customer Name:  Paul Ng Priority Number: 90 Serial Number: 9084
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.           Paul Ng			 90				9084
 3.      Amanda Trapp			 90				9098
 4.  Vincent Gonzales			 59				5992
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.       Robert Hill			 57				5799
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 14.       Sue Andrews			 44				4486
 15.      Joanne Brown			 20				2085
 16.        Tom Martin			 54				5496
 =================================================================
 Now Inserting........
 
 Customer Name:  Steven Chen Priority Number: 41 Serial Number: 4183
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.           Paul Ng			 90				9084
 3.      Amanda Trapp			 90				9098
 4.  Vincent Gonzales			 59				5992
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.       Robert Hill			 57				5799
 9.        Paula Hung			 28				2891
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 14.       Sue Andrews			 44				4486
 15.      Joanne Brown			 20				2085
 16.        Tom Martin			 54				5496
 17.       Steven Chen			 41				4183
 =================================================================
 Now Inserting........
 
 Customer Name:  Vladimir Johnson Priority Number: 49 Serial Number: 4982
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.           Paul Ng			 90				9084
 3.      Amanda Trapp			 90				9098
 4.  Vincent Gonzales			 59				5992
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.       Robert Hill			 57				5799
 9.  Vladimir Johnson			 49				4982
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 14.       Sue Andrews			 44				4486
 15.      Joanne Brown			 20				2085
 16.        Tom Martin			 54				5496
 17.       Steven Chen			 41				4183
 18.        Paula Hung			 28				2891
 =================================================================
 Now Inserting........
 
 Customer Name:  Peter Edwards Priority Number: 60 Serial Number: 6081
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.           Paul Ng			 90				9084
 3.      Amanda Trapp			 90				9098
 4.     Peter Edwards			 60				6081
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.       Robert Hill			 57				5799
 9.  Vincent Gonzales			 59				5992
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 14.       Sue Andrews			 44				4486
 15.      Joanne Brown			 20				2085
 16.        Tom Martin			 54				5496
 17.       Steven Chen			 41				4183
 18.        Paula Hung			 28				2891
 19.  Vladimir Johnson			 49				4982
 =================================================================
 
 =================================================================
 
 Final Sorted Priority List(based on serial number):
 
 Customer List
 Name       		Priority	 SerialNumber
 =================================================================
 1.   Jonathan Nguyen			 93				9397
 2.           Paul Ng			 90				9084
 3.      Amanda Trapp			 90				9098
 4.     Peter Edwards			 60				6081
 5.         Steve Che			 35				3589
 6.           Bob Che			 86				8694
 7.    Warren Rexroad			 72				7293
 8.       Robert Hill			 57				5799
 9.  Vincent Gonzales			 59				5992
 10.   Mary Lou Gilley			 13				1395
 11.        Lou Masson			 17				1790
 12.         Linda Lee			 80				8088
 13.    Dave Lightfoot			 53				5387
 14.       Sue Andrews			 44				4486
 15.      Joanne Brown			 20				2085
 16.        Tom Martin			 54				5496
 17.       Steven Chen			 41				4183
 18.        Paula Hung			 28				2891
 19.  Vladimir Johnson			 49				4982
 =================================================================
 Here is the Final Sorted Pirority Queue Tree Graph...
 ****************************************************************************************************************************************************************************************
                                                                        Jonathan Nguyen-9397
                                            Paul Ng-9084                                               Amanda Trapp-9098
 
                    Peter Edwards-6081                         Steve Che-3589                         Bob Che-8694                         Warren Rexroad-7293
 
    Robert Hill-5799      Vincent Gonzales-5992      Mary Lou Gilley-1395      Lou Masson-1790      Linda Lee-8088      Dave Lightfoot-5387      Sue Andrews-4486      Joanne Brown-2085
 
 Tom Martin-5496  Steven Chen-4183  Paula Hung-2891  Vladimir Johnson-4982
 
 ****************************************************************************************************************************************************************************************
 Thanks for using this program.
 ****************************************************************************************************************************************************************************************
 All value in vector has been deleted
 ****************************************************************************************************************************************************************************************
 Program ended with exit code: 0
 
 */

```

### priorityQueue.cpp
```cpp
//
//  Customer.h
//  HW5
//
//  Created by Rednik Tony on 12/2/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//

#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <iomanip>

#include "priorityQueue.h"
#include "Customer.h"

using namespace  std;
//using vector for generating customers tables
vector<Customer> customers;

//main output function
void priorityQueue::print() const
{
    cout << "\n \t\t\t\t\tCustomer List"<<endl;
    cout << "\t\t\tName"<<setw(17)<< "\t\tPriority" << "\t SerialNumber"<<endl;
    cout << "================================================================="<<endl;
    for(int i = 0; i < customers.size(); i++)
    {
        cout << i+1 <<". "<<setw(17);
        cout << customers[i].getName()<< "\t\t\t " <<customers[i].getPriority()<<"\t\t\t\t"<< customers[i].getSerialNumber() << endl;
    }
    cout << "================================================================="<<endl;
}

//read queue from buttom to top
void priorityQueue::readHeapUp(int bottom)
{
    Customer temp;
    
    if (bottom > 0)
    {
        int parentbranch = (bottom - 1) / 2;
        
        if(customers[bottom].getSerialNumber() > customers[parentbranch].getSerialNumber())		        {
            temp = customers[bottom];
            customers[bottom] = customers[parentbranch];
            customers[parentbranch] = temp;
            
            readHeapUp(parentbranch);
        }
    }
}

// read quque from top to buttom
void priorityQueue::readHeapDown(int root, int bottom)
{
    Customer temp;
    int biggestchild, rightChild, leftChild;
    leftChild	= getLeftChildIndex(root);
    rightChild	= getRightChildIndex(root);
    
    if(leftChild <= bottom)
    {
        if(leftChild == bottom)
            biggestchild = leftChild;
        else
        {
            if(customers[leftChild].getSerialNumber() <= customers[rightChild].getSerialNumber())
                biggestchild = rightChild;
            else
                biggestchild = leftChild;
        }
        if(customers[root].getSerialNumber() < customers[biggestchild].getSerialNumber())
        {
            temp = customers[root];							
            customers[root] = customers[biggestchild];
            customers[biggestchild] = temp;
            readHeapDown(biggestchild, bottom);
        }
    }
}

//inserting new elements in to queue
bool priorityQueue::enqueue(Customer c)
{
    customers.push_back(c);
    cout << "Now Inserting........"<< endl;
    cout << "\n Customer Name: " << customers[count].getName()<< " Priority Number: " << customers[count].getPriority()<< " Serial Number: " << customers[count].getSerialNumber() << endl;
    readHeapUp(count);
    count++;
    print();
    return true;
}

//pop out the items in the queue.
bool priorityQueue::dequeue()
{
    cout << "Now deleting........" << endl;
    if(customers.size() == 0)
    {
        return false;
    }
    cout << "\nRemoving Customer: " << customers[0].getName() << " Serial Number:" << customers[0].getSerialNumber() << endl;
    customers[0] = customers[customers.size() - 1];
    customers.pop_back();
    readHeapDown(0, customers.size() - 1.00);
    count--;
    return true;
}

//Check the queue is empty
bool priorityQueue::isEmpty() const
{
    if(count == 0)
    {
        return true;
    }
    else
    {
        return false;
    }
}

//At the end of this program destruct all data.
void priorityQueue::destruct()
{
    while (count > 0)
    {
        customers.pop_back();
        count--;
    }
    
    cout << "All value in vector has been deleted\n";
    cout << "****************************************************************************************************************************************************************************************"<<endl;
}

//This is a graph function showing how tree it is.
void priorityQueue::treeGraph()
{
    cout << " \t\t\t\t\t\t\t\t\t\t\t\t\t\t\tHere is the Final Sorted Pirority Queue Tree Graph..."<<endl;
    cout << "****************************************************************************************************************************************************************************************"<<endl;
    cout <<"                                                                        " <<customers[0].getName()<<"-"<<customers[0].getSerialNumber() << endl;
    for(int i = 1; i < 3; i++)
    {
        cout <<"                                              " <<customers[i].getName()<<"-"<<customers[i].getSerialNumber();
    }
    cout << endl<<endl;
    for(int i = 3; i < 7; i++){
        cout <<"                        " <<customers[i].getName()<<"-"<<customers[i].getSerialNumber();
    }
    cout << endl<<endl;
    for(int i = 7; i < 15; i++){
        cout <<"     " <<customers[i].getName()<<"-"<<customers[i].getSerialNumber();
    }
    cout << endl<<endl;
    for(int i = 15; i < 19; i++){
        cout <<" " <<customers[i].getName()<<"-"<<customers[i].getSerialNumber();
    }
    cout << endl<<endl;
}
```

### priorityQueue.h
```cpp
//
//  Customer.h
//  HW5
//
//  Created by Rednik Tony on 12/2/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//

#ifndef PRIORITY_QUEUE_H
#define PRIORITY_QUEUE_H
#include "Customer.h"

class priorityQueue
{
private:
    int count;
    int getLeftChildIndex(int root) { return root * 2 + 1; };
    int getRightChildIndex(int root) { return root * 2 + 2; };
    
public:
    //insert and delete
    bool enqueue(Customer c);
    bool dequeue();
    //read direction
    void readHeapUp(int);
    void readHeapDown(int, int);
    //print& checkEmpty
    bool isEmpty() const;
    void print() const;
    //count & output
    void treeGraph(); 
    void setCount(int aCount)
    {
        count = aCount;
    }
    //destory queue
    void destruct();
    
    int getCount() const {
        return count;
    }
    
    //defalt constructor
    priorityQueue()
    {
        count = 0;
    }
    ~priorityQueue(){destruct();}
};

#endif
```

### Customer.h
```cpp
//
//  Customer.h
//  HW5
//
//  Created by Rednik Tony on 12/2/16.
//  Copyright © 2016 Xia Hua. All rights reserved.
//

#ifndef Customer_h
#define Customer_h

#include <string>

using namespace std;

class Customer
{
private:
    string name;
    int mileage;
    int years;
    int priority;
    int serialNumber;
    
public:
    Customer()
    {
        name = "";
        mileage = 0;
        years = 0;
        priority = 0;
        serialNumber = 0;
    }

    // Getter
    string getName(){return name;} const
    int getMileage(){return mileage;} const
    int getYears(){return years;} const
    int getSerialNumber(){return serialNumber;} const
    int getPriority(){return priority;} const
    
    //=============================================================
    //Setter
    void setName(string aName)
    {
        name = aName;
    }
    void setMileage(int aMileage)
    {
        mileage = aMileage;
    }
    void setYears(int aYears)
    {
        years = aYears;
    }
    void setPriority(int aPriority)
    {
        priority = aPriority;
    }
    void setSerialNumber(int aSerialNumber)
    {
        serialNumber = aSerialNumber;
    }
    // Constructor and Destructor
        ~Customer(){}
};

#endif /* Customer_h */

```

### overbooked.txt
```cpp
5 53000 Robert Hill
3 89000 Amanda Trapp
3 93000 Jonathan Nguyen
5 53000 Tom Martin
1 17000 Mary Lou Gilley
3 89000 Bob Che
7 72000 Warren Rexroad
2 65000 Vincent Gonzales
3 34000 Paula Hung
6 21000 Lou Masson
4 42000 Steve Che
3 89000 Linda Lee
3 63000 Dave Lightfoot
5 53000 Sue Andrews
2 33000 Joanne Brown
7 99000 Paul Ng
5 53000 Steven Chen
2 65000 Vladimir Johnson
7 72000 Peter Edwards
```