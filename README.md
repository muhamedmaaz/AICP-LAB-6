# AICP-LAB-6
This is my Aicp lab-6 task 

#include <iostream>
using namespace std;

void checkSack(char contents, double weight, int& rejectedSacks, double& totalWeight) {
    if (contents != 'C' && contents != 'G' && contents != 'S') {
        cout << "Rejected: Invalid contents. Please enter C(cement), G(gravel), or S(sand)." << endl;
        rejectedSacks++;
        return;
    }

    if ((contents == 'C' && (weight <= 24.9 || weight >= 25.1)) ||
        ((contents == 'G' || contents == 'S') && (weight <= 49.9 || weight >= 50.1))) {
        if (contents == 'C') {
            cout << "Rejected: Cement sack weight should be between 24.9 and 25.1 kilograms." << endl;
        } else {
            cout << "Rejected: Gravel/sand sack weight should be between 49.9 and 50.1 kilograms." << endl;
        }
        rejectedSacks++;
        return;
    }

    totalWeight += weight;
}

void checkOrder() {
    int numCementSacks, numGravelSacks, numSandSacks;
    int rejectedSacks = 0;
    double totalWeight = 0.0;

    cout << "Enter the number of Cement sacks: ";
    cin >> numCementSacks;

    cout << "Enter the number of Gravel sacks: ";
    cin >> numGravelSacks;

    cout << "Enter the number of Sand sacks: ";
    cin >> numSandSacks;

    for (int i = 0; i < numCementSacks; ++i) {
        cout << "\nCement Sack " << i + 1 << ":" << endl;
        checkSack('C', i*10 + 5.0, rejectedSacks, totalWeight);
    }

    for (int i = 0; i < numGravelSacks; ++i) {
        cout << "\nGravel Sack " << i + 1 << ":" << endl;
        checkSack('G', i*10.0, rejectedSacks, totalWeight);
    }

    for (int i = 0; i < numSandSacks; ++i) {
        cout << "\nSand Sack " << i + 1 << ":" << endl;
        checkSack('S', i*10 + 1.0, rejectedSacks, totalWeight);
    }

    cout << "\nTotal weight of the order: " << totalWeight << " kilograms" << endl;

    cout << "Number of sacks rejected from the order: " << rejectedSacks << endl;

    double regularPriceCement = numCementSacks * 3.0;
    double regularPriceGravel = numGravelSacks * 2.0;
    double regularPriceSand = numSandSacks * 2.0;

    double totalRegularPrice = regularPriceCement + regularPriceGravel + regularPriceSand;

    int numSpecialPacks = numCementSacks;

	if (numGravelSacks / 2 < numSpecialPacks) {
    	numSpecialPacks = numGravelSacks / 2;
	}

	if (numSandSacks / 2 < numSpecialPacks) {
    	numSpecialPacks = numSandSacks / 2;
	}


    double discountPrice = numSpecialPacks * 10.0;
    double amountSaved = totalRegularPrice - discountPrice;

    cout << "\nRegular price for the order: $" << totalRegularPrice << endl;

    if (numSpecialPacks > 0) {
        cout << "Special packs in the order: " << numSpecialPacks << endl;
        cout << "New price for the order after discount: $" << discountPrice << endl;
        cout << "Amount saved: $" << amountSaved << endl;
    }
}

int main() {
    checkOrder();
    return 0;
}



