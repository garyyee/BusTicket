/*
 ============================================================================
 Name        : ACS126 C Programming Assignment-007
 Author      : Gary Yee Siew Wah
 Copyright   : 2016
 Reg. No.    : 150144216
 Date        : 11th May 2016
 Description : This program helps to book bus ticket and book by using file 
               and print the ticket as text file.
 ============================================================================
 */

/*List of Libraries */
#include<stdio.h>
#include<stdlib.h>

/*Struct prototype */
struct transport{
	char dloc[50],aloc[50];           // hold the location name
	char ndriver[50];                 // hold the driver's name
	int aTime;                        // hold value for the time 
    int	aMin;                         // hold value for min
	char nbus[50];                    // hold for the bus number
	int date;                         // hold for date 
	int month;                        // hold for month
	int seat[10][10];                 // creat the seats for the bus
	int nrows,ncols;                  // hold the bus column and row
	int num2;                         // display the seat number
};

/*List of functions */
void detail(struct transport *bus);
void process(struct transport *bus);
void display(struct transport *bus);
void sort(struct transport *bus);
void checkCondition(struct transport *bus);
void passanger(struct transport *bus);
void pay(struct transport *bus, int *price);
void receipt(struct transport *bus);

/*The main funciton*/
int main()    
{  /*List and initialise of variables*/
	struct transport bus;
	int price;
	int money;
	
	detail(&bus);                         // help to display the detail of the bus
	process(&bus);                        // help to sort the procress of booking
	display(&bus);                        // help to display the booking function
	sort(&bus);                           // help to sort the booking function
    checkCondition(&bus);                 // help to display the booking function
    passanger(&bus);                      // name the passanger     
	pay(&bus,&price);                      // pay the receipt
    receipt(&bus);                        // print the receipt
	printf("\nYour receipt is confirm at book.txt, please be sure to check it out :D ");    // print the description
	system("pause");     // pause the program                                                 
}

////////////////////////////////////////////////////////////////////////////////////
/*The detail functiton */
void detail(struct transport *bus)
{
	printf("\t\t\t**********Bus for Tour*************\n");              // print the description 
	puts("");                                                           // print new line
	
	printf("Please enter bus number with alpahets also can: ");         // print the description 
    fgets(bus->nbus,50,stdin);                                          // enter the bus number 
	puts("");                                                           // print new line
	
	printf("Please enter Driver's name: ");                             // print the description 
    fgets(bus->ndriver,50,stdin);                                       // enter the bus driver name
	puts("");                                                           // print new line
	
	
	printf("Travel from fictional location:\t");                        // print the description 
    fgets(bus->dloc,50,stdin);                                          // enter frictional location name
	puts("");                                                           // print new line
	
	printf("Travel to fictional location:\t");                          // print the description 
	fgets(bus->aloc,50,stdin);                                          // enter frictional location name
	puts("");                                                           // print new line
	
	
	/*List and intialiase of variables*/
	int value;
	char buffer[100];
	char *pff;
	printf("If enter the float number, the program will only take integer and will not round off\n");   // print the description
	do{                                                                 
		printf("Choose Departure Date(from 1 to 31):");                 // print the description 
        fflush(stdout);                                                 // enter the date 

   if (fgets(buffer, sizeof buffer, stdin) != NULL)                     // check the entered non-int
   { 
    bus->date = (int) strtol(buffer, &pff, 10);                         // this will convert to the int 
   }
   }while( bus->date < 1 || bus->date  > 31);                           // check the range
   
   
   	puts("");                                                          // print new line
   	
 	do{
   	printf("Choose Departure Month( from 1 to 12 ):");                // print the description 
	fflush(stdout);                                                     // enter the month 

   if (fgets(buffer, sizeof buffer, stdin) != NULL)                     // check the entered non-int
   {
    bus->month = (int) strtol(buffer, &pff, 10);                        // this will convert to the int 
   }
	}while(bus->month<1 || bus->month > 12);                            // check the range 
	
	
	printf("\nThe daprture date is %d/%d/2016\n",bus->date,bus->month);       // print the description with bus->date and bus->month
	
	printf("Please selected the Departure time ( bus start at 07.00 and ends at 17.00):\n");    // print the description 

    do{
          puts("Please enter hour with 24 hour formst");                    // print the description 
          fflush(stdout);                                                   // enter the 24 hour format

   if (fgets(buffer, sizeof buffer, stdin) != NULL)                         // check the entered non-int
  {
    bus->aTime = (int) strtol(buffer, &pff, 10);                             // this will convert to the int 
  }
	}while(bus->aTime<7 || bus->aTime > 17);                                // check the range 

      do{
    	puts("Please enter min with 60 min format");                    // print the description  	
    while (fgets(buffer, sizeof buffer, stdin)) {                       // continue looping the input
        bus->aMin = strtol(buffer, &pff, 10);                           // assign input as struct variable
        if (pff == buffer || *pff != '\n') {                            // check the selection if the varible equal to new line
            puts("Please enter min with 60 min format ");              // print the decription
        } else break;                                                   // break the loop and return to do while loop
    }
}while( bus->aMin<0 ||  bus->aMin >60 );                                // check the out of range

   printf("Your departure time will be %d:%2d\n",bus->aTime,bus->aMin);     // print the description 
   printf("Your expected  time  arrival will be %d:%2d\n",bus->aTime+4,bus->aMin);   // print the description 
   
   puts("This is your booking system for seat below and book.txt");        // print the description 

return;                                                                     // return the time and name
}

//////////////////////////////////////////////////////////////////////////////
/*The process functiton */
void process(struct transport *bus)
{
   /*List of variables*/
	int ncols,nrows;
	int i,j;
	puts("");           // print new line

    bus->nrows=8;       // assign the bus rows is 8
    bus->ncols=4;       // assign the bus column is 
        
	for(i=0;i<bus->nrows;i++)     // incretment the bus rows 
	{
	for(j=0;j<bus->ncols;j++)     // incretment the bus column
	{
	bus->seat[i][j]=0;            // creat the seat is 0 which is empty
	}
}
return; // return to main function
}

/////////////////////////////////////////////////////////////////////////////////
/*The display  functiton */
void display(struct transport *bus)
{
     /*List of variables*/
	int i,j;
	
	for(i=0;i<bus->nrows;i++)   // increament the bus rows
	{ printf("||");             // print the description 
	for(j=0;j<bus->ncols;j++)   // increament the bus cols
	{
		printf("   %d   ",bus->seat[i][j]);     // print the description with bus seat
	}	printf("||");printf("\n");     // print the description 
    }
    
    FILE *fout;                        // initialise the file 
	fout=fopen("book.txt","w");        // clear the book.txt
	
	for(i=0;i<bus->nrows;i++)         // increament the bus norws
	{
	for(j=0;j<bus->ncols;j++)         // increament the bus cols
	{
		fprintf(fout,"%d     ",bus->seat[i][j]);    // print the matrix to the file
	}	fprintf(fout,"\n");                         // print the new line
    }
   
    fclose(fout);             // close the file
    
    puts("Now!!!! Please look a booking system at text file");             // print the description
    puts("The zero means empty seat and to book just input any number");    // print the description
    puts("");                                                                // print the description
    system("pause");                                                        // pause the program
	return;                                                                 // return to the main function
}

//////////////////////////////////////////////////////////////////////////////////
/*The sort functiton */
void sort(struct transport *bus)
{
	/*List of variables*/
	FILE *fin;
    int i,j;
	char r[50];
	int num;
	 
	fin=fopen("book.txt","r");  // this  helps to read the file

	printf("\nThis is read from file\n");   // print the description

    for(i=0;i<bus->nrows;i++)   // increment the bus rows
	{
	for(j=0;j<bus->ncols;j++)   // increment the bus cols
	{
		fscanf(fin,"%d",&num);  // scanf the modifield matric
		bus->seat[i][j]=num;    // insert the number into the matric
	}
    }

      
    for(i=0;i<bus->nrows;i++)   // increment the bus rows
	{printf("||");              // print the description
	for(j=0;j<bus->ncols;j++)   // increment the bus cols
	{
		printf("   %d   ",bus->seat[i][j]);   // print the seat with modified seats
	}printf("||");	printf("\n");             // print  the description
    }
    
   puts("");    // print new line

   fin=fopen("book.txt","w"); // reset the booking system or receipt
    
    fclose(fin);         // close the file
    system("pause");     // pause the program
    return;
}

/////////////////////////////////////////////////////////////////////////////////////
/*The checkCondition functiton */
void checkCondition(struct transport *bus)  
{
	
    bus->num2=0; // this assign the number of seat that modified from the text file
     int i,j;   // list of integer variables
     
     printf("\n");  // print the description
       
	for(i=0;i<bus->nrows;i++) // increment the bus nrows
	{
	for(j=0;j<bus->ncols;j++) // increment the bus ncols
	{
		if(bus->seat[i][j] !=0)    // check if the seat is not empty
		{
            printf("You have book this seat number [%d:%d]\n",i+1,j+1); // print the dscription  
            bus->num2++;   // check the next seat
        } // end the if statement
	} 
}
printf("\nYou have book %d seat/s\n",bus->num2); // print the description

 return; // return to the main function
}

//////////////////////////////////////////////////////////////////////////////////
/* The passanger function */
void passanger(struct transport *bus)
{    
 /*List of Variables */
    int k;
    char *psg;
     
    psg=(char*)calloc(bus->num2,sizeof(int));  // when number of seat book it will convert to string

    printf("Please enter the name of the passanger\n");   // print the dscription


    for(k=0;k<bus->num2;k++)      // increment for the string to enter
	{
	scanf("%s",&psg[k]);       // input the passanger name
	}
    
    printf("Here is the passager name\n"); // print the description
	
	for(k=0;k<bus->num2;k++)     // increment the num2
	{
		printf("%s \n",&psg[k]);  // print out the passanger's name
	}
	free(psg);      // delocate the memeory
    system("pause"); // pause the program
}

////////////////////////////////////////////////////////////////////////////////
/*The pay function */
void pay(struct transport *bus, int *price)
{   
/*Initialise the variables */
    int money;
	money=(bus->num2*50);
    price=&money;
    
    printf("You had pay $%d\n",money*2);   // print the description
    
    price=&money;     // return to the main function
}

////////////////////////////////////////////////////////////////////////////////
/*The receipt function */
void receipt(struct transport *bus)
{
	/*List of variables */
    FILE *fout;
    int i,j;
     
    printf("Your Receipt is now being processed\n");  // print the description
    printf("Your receipt is at book.txt, please check it out\n"); // print the description
    fout=fopen("book.txt","w"); // reset the book system
     
    fprintf(fout,"\t\tTour Receipt\n");     // print the description into the file
    fprintf(fout,"Bus number: %s\n",bus->nbus);   // print the description into the file
    fprintf(fout,"Route: %s to %s \n",bus->dloc,bus->aloc);   // print the description into the file
 
  
    for(i=0;i<bus->nrows;i++)     // increment the bus nrows
	{
	for(j=0;j<bus->ncols;j++)    // increment the bus ncols
	{
		if(bus->seat[i][j] !=0)  // check the selection if the seat is empty
		{
            fprintf(fout,"You have book this seat number [%d:%d]\n",i+1,j+1);  // print the description into the file
            bus->num2++; // increment the modified seat
        }
	}
}
    fprintf(fout,"Price :$%d.00\n",bus->num2*50);   // print the description into the file
    fprintf(fout,"\t\tIssue by %s\n",bus->ndriver);  // print the description into the file
    fprintf(fout,"\t\tIssue on %d/%d/2016\n",bus->date,bus->month);  // print the description into the file
    fclose(fout); // close the file
    system("pause");  // puase the system
    return;   // return to main function
    }
