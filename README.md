# Hotel_Reservation
##video https://drive.google.com/file/d/1KILe7X07VS0qWI-S3eghtn_lcvNF-vuY/view?usp=drivesdk
#include <iostream>
#include <vector>
#include <string>
#include <iomanip>

using namespace std;


struct HotelOffering {
    int id;
    string name;
    double price;
};

// 
struct ReservationItem {
    string name;
    double price;
};

void showMenu() {
    cout << "\n--- Interactive Smart Hotel Booking System ---" << endl;
    cout << "1. View available hotel offerings" << endl;
    cout << "2. Add offering to Customer Reservation" << endl;
    cout << "3. View current reservation items" << endl;
    cout << "4. Print Final Folio (Bill)" << endl;
    cout << "5. Exit" << endl;
    cout << "Enter your choice: ";
}

int main() {
    // 
    vector<HotelOffering> offerings = {
        {101, "Standard Overnight Room", 150.0},
        {102, "Luxury Suite", 350.0},
        {201, "Spa & Wellness Service", 75.0},
        {202, "Airport Transfer Service", 50.0}
    };

    vector<ReservationItem> currentReservation;
    int choice;
    const double TAX_RATE = 0.14; //  14%

    while (true) {
        showMenu();
        cin >> choice;

        if (choice == 1) {
            // 
            cout << "\nAvailable Offerings:" << endl;
            for (const auto& item : offerings) {
                cout << "[" << item.id << "] " << item.name << " - $" << item.price << endl;
            }
        } 
        else if (choice == 2) {
            //  ID
            int selectedId;
            cout << "Enter the ID of the offering to add: ";
            cin >> selectedId;
            
            bool found = false;
            for (const auto& item : offerings) {
                if (item.id == selectedId) {
                    currentReservation.push_back({item.name, item.price});
                    cout << "Added: " << item.name << endl;
                    found = true;
                    break;
                }
            }
            if (!found) cout << "Invalid ID!" << endl;
        } 
        else if (choice == 3) {
            // 
            if (currentReservation.empty()) {
                cout << "No items in reservation." << endl;
            } else {
                cout << "\nYour Current Reservation:" << endl;
                for (const auto& item : currentReservation) {
                    cout << "- " << item.name << ": $" << item.price << endl;
                }
            }
        } 
        else if (choice == 4) {
            // 
            if (currentReservation.empty()) {
                cout << "Nothing to bill." << endl;
                continue;
            }
            double subtotal = 0;
            cout << "\n--- FINAL FOLIO (BILL) ---" << endl;
            for (const auto& item : currentReservation) {
                cout << left << setw(25) << item.name << "$" << item.price << endl;
                subtotal += item.price;
            }
            double taxes = subtotal * TAX_RATE;
            double total = subtotal + taxes;
            
            cout << "--------------------------" << endl;
            cout << "Subtotal:  $" << subtotal << endl;
            cout << "Taxes (14%): $" << taxes << endl;
            cout << "Grand Total: $" << total << endl;
            cout << "--------------------------" << endl;
        } 
        else if (choice == 5) {
            // 
            cout << "Exiting system. Goodbye!" << endl;
            break;
        } 
        else {
            cout << "Invalid selection. Try again." << endl;
        }
    }

    return 0;
}
