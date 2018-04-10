# minios
#include<iostream>
//#include<unistd.h>
#include<windows.h>
#include<stdlib.h>
using namespace std;
int m[1024]={0};
int c=0,sb[10],len[10];
string fn[10];
void display()
{
    int j=0;
    for(int i=0;i<1024;i++)
    {
        if(j%50==0)
            cout<<endl;
        cout<<m[i];
        j++;
    }
}
void allocate(string n,int s,int sp)
{
    for(int i=sp;i<(sp+s);i++)
    {
            m[i]=1;
    }
    sb[c]=sp;
}
int search(string n,int s)
{
    int j,e=0,l=0,i;
    for( i=0;i<1024;i++)
    {
        if(m[i]==0)
        {
            j=i;
            e=0;
            //cout<<"Empty at "<<i;
            while(m[i]!=1)
            {
                i++;
                if(i==50)
                    break;
                e++;
                if(e==s)
                {
                   // cout<<"Can be stored here";
                    allocate(n,s,j);
                    l++;
                    break;
                }
            }
        }
        if(l==1)
            break;
    }
    return l;
}
void delet(int z)
{
    for(int i=sb[z];i<(sb[z]+len[z]);i++)
        m[i]=0;
    for(int i=z;i<c-1;i++)
    {
        fn[i]=fn[i+1];
        sb[i]=sb[i+1];
        len[i]=len[i+1];
    }
    c--;
    cout<<"File Deleted!\n";
}
int main()
{
    for(int i=0;i<50;i++){
       // if(i>=20 && i<25)
       // m[i]=1;
       // else if(i>=35 && i<40)
       //     m[i]=1;
       // else
            m[i]=0;
    }
    display();
    int ch=0;
    while(ch!=4)
    {
        cout<<"\n1.Create a File\n2.Generate Table\n3.Retrieve a File\n4.Exit\nEnter you choice:";
        cin>>ch;
        if(ch==1){
            cout<<"Enter the name of the File:";
            cin>>fn[c];
            cout<<"Enter the length of the File:";
            cin>>len[c];
            int p=search(fn[c],len[c]);
            if(p==0)
                cout<<"\nFile Cannot be Stored";
            else{
                cout<<"\nFile Stored.";
                c++;
            }
           // display();
        }
        if(ch==2)
        {
            cout<<"File Name\t Start Block\t Length of File";
            cout<<endl;
            for(int i=0;i<c;i++)
                cout<<fn[i]<<"\t\t"<<sb[i]<<"\t\t"<<len[i]<<endl;
        
        if(ch==3)
        {
            string n;
            int i;
            cout<<"Enter the file to be searched:";
            cin>>n;
            for( i=0;i<c;i++)
            {
                if(fn[i]==n){
                    cout<<"File found at block "<<sb[i];
                    break;}
            }
                if(i==c)
                {
                    cout<<"File Not Found!";
                }
                else{
                int x=0;
                cout<<"\nEnter 1 to delete the file:";
                cin>>x;
                if(x==1)
                {
                    delet(i);
                }
                }
            }
        display();
        if(ch<1 || ch>4)
            cout<<"Wrong Input!";
        }
}
