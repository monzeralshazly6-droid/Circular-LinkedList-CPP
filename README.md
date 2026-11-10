# circular linked list #

#include<iostream>

using namespace std;

struct Node {

    int data;
    Node* next;
    
};

Node* head = nullptr;

void createfirstNode(int data) {

    Node *newnode = new Node();
    newnode->data = data;
    newnode->next = newnode;
    head = newnode;

}

//e = add it in the end and b = add it in the biginig

void insert(int data, char letter)
{

    if (letter == 'e') {
        if (head==nullptr) {
            createfirstNode(data);
            return;
        }
        Node *temp = head;
        while (temp->next != head) {
            temp = temp->next;
        }
        Node *newnode = new Node();
        newnode->data = data;
        temp->next = newnode;
        newnode->next = head;
        return;

    }

    else if (letter == 'b') {
        if (head==nullptr) {
            createfirstNode(data);
            return;
        }
        Node *temp = head;
        Node *newnode = new Node();
        newnode->data = data;
        newnode->next = head;
        while (temp->next != head) {
            temp = temp->next;
        }
        head = newnode;
        temp->next = newnode;
        return;

    }

}

void display() {

    if (head==nullptr) {
        cout<<"List is empty"<<endl;
        return;
    }
    
    Node *temp = head;


    do {
        cout<<temp->data<<" ";
        temp = temp->next;
    }while (temp != head);
    return;
}

void deletefirstNode() {

    if (head==nullptr) {
        cout<<"List is empty"<<endl;
        return;
    }

    if (head->next == head) {
        Node *temp = head;
        head = nullptr;
        delete temp;
        return;
    }

    Node *temp = head;
    while (temp->next != head) {
        temp = temp->next;
    }
    Node *temp1 = head;
    head = head->next;
    delete temp1;
    temp->next = head;
    return;
}

void deleteLastNode() {

    if (head==nullptr) {
        cout<<"List is empty"<<endl;
        return;
    }

    if (head->next == head) {
        Node *temp = head;
        head = nullptr;
        delete temp;
        return;
    }

    Node *next = head;
    Node *prev = next;
    while (next->next != head) {
        prev = next;
        next = next->next;
    }
    delete next;
    prev->next = head;
}

void deleteByValue(int data) {

    if (head == nullptr) {
        cout<<"List is empty"<<endl;
        return;
    }

// if list was just from 1 node

    if(head->next == head)
    {
        if (head->data == data) {
            Node *temp = head;
            head = nullptr;
            delete temp;
        }
        return;
    }

// if the list was from 2 nodes

    else if (head->next->next == head)
    {   
        if (head->data == data)
        {
            Node *temp = head;
            head = head->next;
            head->next = head;
            delete temp;
            
        }
        else if (head->next->data == data)
        {
            delete head->next;
            head->next = head;
        }
        return;
    }

// if the list was from 3 or more
    
    Node *prev = head;
    Node* curr = head->next;
    Node* next = head->next->next;


    do{ 
        if (data == prev->data)
        {
            cout <<"Found !! \n";
            head = curr;
            delete prev;
            prev = nullptr;
            next->next = head;
            return;
        }

        else if(data == curr-> data)
        {
            cout <<"Found !! \n";
            head->next= next;
            next->next = head;
            delete curr;
            curr = nullptr;
            return;
        }

        else if(next->data == data)
        {
            cout << "Found !! \n"; 
            curr->next = head;
            delete next;
            return;
        }

       if(next->next == head)
            {
                cout <<"Not Found !!!\n";
                return;
            }
        prev = prev->next;
        curr = curr->next;
        next = next->next;

     
    }while(next != head);
    

}

void search(int data) {

    if (head==nullptr) {
        cout<<"List is empty"<<endl;
        return;
    }
    
    Node *temp = head;
    int pos = 0;
    bool found = true;
    Node *after = head;
    
    while (temp->data != data) {
        after = temp->next;
        if (after == head) {
            found = false;
            cout << "Not found !!"<<endl;
            return;
        }
        
        temp = temp->next;
        pos++;

    }
    
    if (found == true) {
        cout<< "your number " <<temp->data <<" Found at postion " << pos <<endl;
        return;
    }
}



int main() {

    insert(10,'e');
    insert(20,'e');
    insert(30, 'e'); 
    display();cout <<endl;
    deleteByValue(10);
    display();cout <<endl<<endl;
    
}
