# POLYNOMIALDRAFT1
CREATES POLYNOMIAL ADDS EXPRESSION CHANGES EXPRESSION 
//Jonathan Sessom
// Console Application creates a polynomial, finds the degree of the polynomial, changes a certain coefficient and adds two polynomials
//does sparse implementation and traversal
#include <iostream>
#include <math.h>
#include <stdlib.h>
using namespace std;
struct node
{
	int coefficient;
	int exponent;
	struct node *next;
};

struct node *memorypointer, memorypointer2;
bool isEmpty(node *head)
{
	if (head == NULL)
		return true;
	else
		return false;
}
void displaypoly(node *p)
{
	cout << " The sum of the two polynomials P(x)=	";
	while (p != NULL)
	{
		cout << p->coefficient;
		cout << "x^";
		cout << p->exponent;
		p = p->next;
		cout << "+ ";

	}
	cout << endl;
}
void addpoly(node *poly1, node *poly2, node *poly)
{
	node *ptr1, *ptr2, *ptr;
	ptr1 = poly1, ptr2 = poly2, ptr = new node, poly = ptr;
	while (ptr1->next != NULL && ptr2->next != NULL)
	{

		if (ptr1->exponent > ptr2->exponent)// compares two exponent at specific nodes and then assigns our ptr to greatest one
		{
			ptr->coefficient = ptr1->coefficient;
			ptr->exponent = ptr1->exponent;
			ptr1 = ptr1->next;
		}
		else if (ptr1->exponent < ptr2->exponent)// compares two exponent at specific nodes and then assigns our ptr to greatest one
		{
			ptr->coefficient = ptr2->coefficient;
			ptr->exponent = ptr2->exponent;
			ptr2 = ptr2->next;
		}
		else// if two exponents are equal we add the coefficient and store them in ptr
		{
			ptr->coefficient = ptr1->coefficient + ptr2->coefficient;
			ptr->exponent = ptr1->exponent;
			ptr1 = ptr1->next, ptr2 = ptr2->next;
		}
		ptr->next = new node(), ptr = ptr->next;// creates a new node
	}
	node *ptrr = new node();//checks to see if there are extras then creates a new node to hold extra polynomials
	if (ptr1->next)ptrr = ptr1;
	if (ptr2->next)ptrr = ptr2;
	while (ptrr->next)
	{
		ptr->coefficient = ptrr->coefficient;
		ptr->exponent = ptrr->exponent;
		ptr->next = new node();
		ptr = ptr->next;
		ptrr = ptrr->next;

	}
	
	ptr->next = NULL;
	displaypoly(poly);
	cout << endl;
	cout << endl;
}
void creatPloynomial(node* head, int coffval, int expval)
{
	if (coffval == 0)
	{
		return;
	}
	node* newNode = new node();
	node *last = head;
	newNode->coefficient = coffval;
	newNode->exponent = expval;
	newNode->next = NULL;
	if (head == NULL)
	{
		head = newNode;
		return;
	}
	while (last->next != NULL)
		last = last->next;
	last->next = newNode;
	return;
}
void addTwoPolynomial(node *list1, node* list2, node *newPolynomial)
{

	node *node1 = list1;

	while (node1 != NULL)
	{
		int flag = 0;
		node *node2 = list2;
		while (node2 != NULL)
		{
			if (node1->exponent == node2->exponent)
			{

				if (node1->coefficient + node2->coefficient == 0)
				{

				}

				else

				{
					creatPloynomial(newPolynomial, node1->coefficient + node2->coefficient, node1->exponent);
				}
				flag = 1;

			}
			node2 = node2->next;
		}
		if (flag == 0)
		{

			creatPloynomial(newPolynomial, node1->coefficient, node1->exponent);
		}
		node1 = node1->next;
	}

	node *temp4 = list2;
	while (temp4 != NULL)
	{
		int flag1 = 0;
		node *temp3 = list1;
		while (temp3 != NULL)
		{
			if (temp4->exponent == temp3->exponent)
			{
				flag1 = 1;
			}
			temp3 = temp3->next;
		}
		if (flag1 == 0)
		{
			creatPloynomial(newPolynomial, temp4->coefficient, temp4->exponent);
		}
		temp4 = temp4->next;
	}

}


void printPolynomial(node *list1)
{

	node *node = list1;
	while (node != NULL)
	{
		if (node->exponent == 0)
		{
			cout << node->coefficient << " ";
		}
		else if (node->exponent == 1)
		{
			cout << node->coefficient << "x" << " ";
		}
		else
		{
			cout << node->coefficient << "x" << "^" << node->exponent << " ";
		}

		node = node->next;
		if (node != NULL)
		{
			cout << "+" << " ";
		}
	}
	cout << endl;
}
void degree(node *head)// supposed to show the term that has the highest power.
{
	node *i, *j;
	i = head;
	int maxexpo, coeff;
	maxexpo = i->exponent;

	for (i = head; i != NULL; i = i->next)
	{

		if (i->exponent > maxexpo)
		{
			maxexpo = i->exponent;
			j = i;
			coeff = i->coefficient; //this is not a address this the name of the

		}

	}
	cout << " The coefficient that has the highest power is" << " " << coeff << endl;
}
void changecoeff(node *head, int coeff, int expo)// supposed to show the term that has the highest power.
{
	node *i, *j;
	i = head;

	for (i = head; i != NULL; i = i->next)
	{

		if (i->exponent == expo)
		{
			i->coefficient + coeff;
			i->coefficient = i->coefficient + coeff;

		}

	}

}
void insertfirstnode(node *&head, int coeff, int expo)
{
	struct node *memorypointer, *memorypointer2;


	memorypointer = (struct node *) malloc(sizeof(struct node));// creating a start pointer

	memorypointer->coefficient = coeff;// pointing our pointer to our first node
	memorypointer->exponent = expo;
	memorypointer->next = NULL;// pointing our first node to the next pointer which points to null

	head = memorypointer; // our head pointer is now pointing to the first node.
	memorypointer2 = head;



}
void insertnode(node *head, node *memorypointer2, int numnodes, int coeff, int expo)//parameters
{
	//insertfirstnode(head, coeff, expo);
	struct node *memorypointer, *p;
	p = head;


	for (int i = 1; i < numnodes; i++)
	{

		cout << " Please enter the value of the next nodes coefficient.";
		cin >> coeff;
		cout << endl;
		cout << " Please enter the value of the next nodes exponent.";
		cin >> expo;
		cout << endl;

		memorypointer2 = head->next;

		memorypointer = (struct node *) malloc(sizeof(struct node)); // we are now creating a new node

		memorypointer->coefficient = coeff;
		memorypointer->exponent = expo;
		memorypointer->next = memorypointer2;

		head->next = memorypointer;


	}
	cout << endl;
}
void display(node *p)
{
	while (p != NULL)
	{
		cout << p->coefficient;
		cout << "x^";
		cout << p->exponent;
		p = p->next;
		cout << "+ ";

	}
	cout << endl;
}





int main()
{
	int covalue, exvalue, i, numnodes;
	struct node *p, *q, *head, *next, *memorypointer, *memorypointer2;

	cout << "I made the first three questions to accept any polynomial from the user." << endl;
	cout << endl;

	cout << " Please enter the number of nodes for this polynomial.";
	cin >> numnodes;
	cout << endl;
	cout << " Please enter the value of the head nodes coefficient.";
	cin >> covalue;
	cout << endl;
	cout << " Please enter the value of the head nodes exponent.";
	cin >> exvalue;
	cout << endl;

	insertfirstnode(head, covalue, exvalue);
	memorypointer2 = head;


	insertnode(head, memorypointer2, numnodes, covalue, exvalue);
	p = head;

	cout << endl;

	p = head;

	cout << endl;

	cout << endl;
	display(p);

	cout << endl;

	p = head;
	degree(head);
	cout << endl;

	int expo, coeff;
	cout << "Please enter exponent you would like to change.\n";
	cin >> expo;
	cout << endl;
	cout << " Please enter the number you would like to increase coefficient of exponent X^" << expo << endl;
	cin >> coeff;
	cout << endl;
	changecoeff(head, coeff, expo);
	p = head;
	display(p);
	cout << endl;


	cout << " Please enter  the number of nodes for the first polynomial.";
	cin >> numnodes;
	cout << endl;
	cout << " Please enter the value of the head nodes coefficient.";
	cin >> covalue;
	cout << endl;
	cout << " Please enter the value of the head nodes exponent.";
	cin >> exvalue;
	cout << endl;

	
	insertfirstnode(head, covalue, exvalue);
	memorypointer2 = head;


	insertnode(head, memorypointer2, numnodes, covalue, exvalue);
	display(head);


	cout << " Please enter  the number of nodes for the second polynomial.";
	cin >> numnodes;
	cout << endl;
	cout << " Please enter the value of the head nodes coefficient.";
	cin >> covalue;
	cout << endl;
	cout << " Please enter the value of the head nodes exponent.";
	cin >> exvalue;
	cout << endl;
	node *head2 = new node;

	insertfirstnode(head2, covalue, exvalue);
	memorypointer2 = head2;


	insertnode(head2, memorypointer2, numnodes, covalue, exvalue);

	display(head2);
	cout << endl;
	node *poly = new node;
	addpoly(head, head2, poly);
  }
