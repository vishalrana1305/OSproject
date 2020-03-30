# OSproject
Operating system project based on the priority Scheduling algorithm where priority of each process changes after the entry of each process
#include<iostream>
#include<time.h>
#include<stdlib.h>
using namespace std;
int main()
{
	srand(time(NULL));
	int n=10,ct=0,k=0;
	int pr[10],burst[10],CT[10],WT[10],burst2[10];
	char pid[10]={'a','b','c','d','e','f','g','h','i','j'},pid2[10];
	cout<<"All the STUDENTS or PROCESSES arrive at the same time"<<endl;
	cout<<"*-------Menu-------*"<<endl;
	cout<<"1. Enter the Burst time manually"<<endl;
	cout<<"2. Randomly generate the Burst time"<<endl;
	int ch=0;
	cout<<"Enter your choice: ";
	cin>>ch;
	if(ch==1){
		cout<<"Enter the burst time for the 10 Students or processes"<<endl;
		for(int i=0; i<n; i++)
		{
			cout<<"Enter the burst time for "<<char(97+i)<<" : ";
			cin>>burst[i];
		
		}
	}
	else if(ch==2){
		for(int i=0; i<n; i++)
		{
			burst[i]=rand()%10;   // randomly generating the burst time
		}
	}
	else{
		cout<<"Wrong Choice \nProgram Terminated";
		return 0;
	}
	cout<<"Burst Time: ";
	for(int a=0; a<n; a++)
	{
		cout<<pid[a]<<" ";
		cout<<burst[a]<<" | ";
	}
	cout<<endl;
	cout<<"Chocolates Distribution"<<endl;
	for(int a=0; a<n; a++)
	{
		for(int i=0; i<n; i++)
		{
			pr[i]=rand()%100;    //Distribution of chocolates after every entry
		}
		for(int i=0; i<n; i++)
		{
			cout<<pid[i]<<" "<<pr[i]<<" | ";
		}
		cout<<endl;
		int max=pr[0],loc=0;
		for(int i=1; i<n; i++)
		{
			if(pr[i]>max)
			{
				max=pr[i];     //Finding the process or Student with maximum chocolates
				loc=i;
			}
		}
		ct=ct+burst[loc]; //completion time
		CT[k]=ct;   
		pid2[k]=pid[loc];
		burst2[k]=burst[loc];
		WT[k]=ct-burst[loc];
		k++;
		
		for(int b=loc; b<n-1; b++)
		{
			pr[b]=pr[b+1];
			burst[b]=burst[b+1];  
			pid[b]=pid[b+1];
		}
		n--;
		a--;	
	}
	cout<<"Process ID Arrival time    Burst Time    Completion Time Turn Around Time  Waiting Time"<<endl;
	for(int x=0; x<k; x++)
	{
		cout<<"  "<<pid2[x]<<"\t|\t"<<"0"<<"\t|\t"<<burst2[x]<<"\t|\t"<<CT[x]<<"\t|\t"<<CT[x]<<"\t|\t"<<WT[x]<<endl;	
	}
	float sum=0;
	for(int p=0; p<k; p++)
	{
		sum=sum+CT[p];   //total turn around time
	}
	cout<<"Average Turn Around time : "<<(sum/k)<<endl;
	sum=0;
	for(int p=0; p<k; p++)
	{
		sum=sum+WT[p];
	}
	cout<<"Average waiting time : "<<(sum/k);
	return 0;
}
