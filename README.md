#include <iostream>
#include <string>
#include <unordered_set>
 
using namespace std;
 
struct Node {
    string name;
    Node* next;
};
 
class IceCreamSet {
    Node* head = nullptr;
 
public:
    void addStudent(const string& name) {
        head = new Node{name, head};
    }
 
    void display() {
        for (Node* curr = head; curr; curr = curr->next)
            cout << curr->name << endl;
    }
 
    IceCreamSet unionWith(IceCreamSet& other) {
        IceCreamSet result;
        unordered_set<string> names;
 
        for (Node* curr = head; curr; curr = curr->next) {
            names.insert(curr->name);
            result.addStudent(curr->name);
        }
 
        for (Node* curr = other.head; curr; curr = curr->next) {
            if (names.insert(curr->name).second) {
                result.addStudent(curr->name);
            }
        }
 
        return result;
    }
 
    IceCreamSet intersectWith(IceCreamSet& other) {
        IceCreamSet result;
        unordered_set<string> otherNames;
 
        for (Node* curr = other.head; curr; curr = curr->next)
            otherNames.insert(curr->name);
 
        for (Node* curr = head; curr; curr = curr->next) {
            if (otherNames.count(curr->name)) {
                result.addStudent(curr->name);
            }
        }
 
        return result;
    }
};
 
int main() {
    IceCreamSet setA, setB;
    int n;
    string name;
 
    cout << "Enter students for Vanilla Ice-cream (0 to stop):\n";
    while (true) {
        cout << "Name: ";
        cin >> name;
        if (name == "0") break;
        setA.addStudent(name);
    }
 
    cout << "Enter students for Butterscotch Ice-cream (0 to stop):\n";
    while (true) {
        cout << "Name: ";
        cin >> name;
        if (name == "0") break;
        setB.addStudent(name);
    }
 
    cout << "\nSet A (Vanilla):\n"; setA.display();
    cout << "\nSet B (Butterscotch):\n"; setB.display();
 
    cout << "\nUnion:\n"; setA.unionWith(setB).display();
    cout << "\nIntersection:\n"; setA.intersectWith(setB).display();
 
    return 0;
}
