//# cpp
//Clock Display
#include <iostream>

using namespace std;


string formatNumbersAsTwoDigits(int number) { //we need to make the numbers two digits that means if they put 7, it should be 07. 
    if (number < 10) { //we use an if statement. if the number is less than 10
        return "0" + to_string(number); //we add a 0 then the number so that its 2 digits. This is taken in as a string
    }
    return to_string(number); //if the number is greater than or equal to 10, we just return the value as a string.
}

 string repeatAstericsFormat(int count) { // we make a new function that repeats the * for as many digits as the output has. 
     return string(count, '*'); // we return the * that is equal to the count length.
 }

string outputTime12HourTimeFormat(int hours, int minutes, int seconds) { //we need a function for the 12 hour format
   string timePeriod; // add a varible for the time period (am or pm)
    if(hours>=12) { //we start by indicating if its PM or AM
        timePeriod = "PM"; }  // set timePeriod to PM
    else { //if its not >= 12 it is AM
        timePeriod = "AM"; // set timePeriod to AM
      }
    
    if (hours % 12 == 0) { //Now that we have if its AM or PM, we need to set the hour
        hours = 12; //hour / 12 does not leave a remainder then the hour is 12
    }
    else { //if hour does have a remainder when divided by 12 then we set the hour equal to the module of that hour / 12
        hours = hours % 12;
    }
    return formatNumbersAsTwoDigits(hours) + ":" + //now we print the results and use the function to get 2 digits 
           formatNumbersAsTwoDigits(minutes) + ":" +
           formatNumbersAsTwoDigits(seconds) + timePeriod; // we need to include the timePeriod (AM or PM) 
}

string outputTime24HourTimeFormat(int hours, int minutes, int seconds) { //this is for a function that outputs time in a 24 hour format. 
    return formatNumbersAsTwoDigits(hours) + ":" +  // we call the function we made previously to print out the given hours as 2 numbers incase its below 10
           formatNumbersAsTwoDigits(minutes) + ":" +  // we call the function we made previously to print out the given minutes as 2 numbers incase its below 10
           formatNumbersAsTwoDigits(seconds); // we call the function we made previously to print out the given seconds as 2 numbers incase its below 10
} 

void printOutMenu() { //we need to add a menu where the user can add a second, minute, hour, and or leave by entering a specific number
    cout << "1. Add a second" << endl; //option 1 add a second
    cout << "2. Add a minute" << endl; //option 2 add a mintue
    cout << "3. Add a hour" << endl; //option 3 add a hour
    cout << "4. Exit" << endl; // option 4 exit 
}


int processesUserInputFromMenuChoice() { //we need to make a function that takes the users input as a choice for the menu section
    int choice; //sets choice as a int variable
    cin >> choice; //takes in the users input and stores it into choice
    return choice; //returns the choice value that was given
}

void displayBoth12And24HourTimeFormats(int hours, int minutes, int seconds) { //function for the display of both clocks
   
    cout << "12-hour format: " << outputTime12HourTimeFormat(hours, minutes, seconds) << endl; // 12 hour format
    cout << "24-hour format: " << outputTime24HourTimeFormat(hours, minutes, seconds) << endl; // 24 hour format
}

int main() {
    int hours = 0;  //make variable for hours, minutes, seconds, and choice.
    int minutes = 0; 
    int seconds = 0;
    int choice;

    do { //we need a do while loop so we can ensure the clock works correctly and doesnt excede how many seconds are in a minute and how many minutes are in an hour and how many hours there are in am and pm
        displayBoth12And24HourTimeFormats(hours, minutes, seconds);
        printOutMenu(); // this calls up the printoutmenu function 
        choice = processesUserInputFromMenuChoice(); //this sets choice equal to the user input in the processesuserinputmenuchoice

        
        if (choice == 1) { // we are programming the users choices 1 is add second
            seconds ++; // add 1 to seconds
            if(seconds >= 60) { //if to make sure seconds doesnt excede 60
                seconds = 0; // sets seconds to 0
                minutes ++; // adds 1 minute
                if(minutes >= 60) { //checks to see in minute is over 60
                    minutes = 0; //sets minute to 0
                    hours = (hours +1) % 24; // adds 1 to hour 
                }
            }
        } else if (choice == 2) { // 2 is add minute
            minutes ++; // this adds a minute
            if (minutes >= 60) { // this is to make sure minutes doesnt excede 60.
                minutes = 0; //sets minute to 0 is its >= 60
                hours = (hours + 1) % 24; // this adds the hour
            }
        } else if (choice == 3) { // 3 is add hour
          hours = (hours + 1) % 24; // this adds an hour
        }
    } while (choice != 4); // 4 is any other choice which ends the program

    return 0;
}
