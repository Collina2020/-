# -
上海交大 程序设计 oj 学生管理系统 写得很菜但也是挺不容易才写完的就存个档吧
#include <iostream>
#include<cstring>

using namespace std;

struct stu{
    char name[50];
    long long int number;
    int grade1;
    int grade2;
    int grade3;
    int grades;
}
p[1000];

int z=0;

void swap(stu &m, stu &n)
{
    stu c=m;m=n;n=c;
}


void add()
{   stu j;
    cin>>j.number>>j.grade1>>j.grade2>>j.grade3;
    cin.getline(j.name,50,'\n');

    bool iftihuan=false;
    if (z==0) {p[0]=j;z++;}
    else{
    for (int i=0;i<z;i++)
    {if (p[i].number==j.number) {p[i]=j;iftihuan=true;break;}}
    if (!iftihuan) {p[z]=j;z++;}}
}


void change()
{   stu j;
    cin>>j.number>>j.grade1>>j.grade2>>j.grade3;
    cin.getline(j.name, 50, '\n');

    for (int i=0;i<z;i++)
    {if (p[i].number== j.number) {p[i]=j;break;}}
}


void shanchu()
{   stu j;
    cin>>j.number;
    bool hasdone=false;
    for (int i=0;i<z;i++)
    {
        if (p[i].number== j.number)
    {
        int s=i;
        while (s+1<z)
        {
            p[s]=p[s+1];
            s++;

        }
        z--;
        hasdone=true;
        break;
    }
    if (hasdone) break;
    }

}



void SearchinNumber()
{   long long int numbers;
    cin>>numbers;
    for (int i=0;i<z; i++)
    {
        if (p[i].number==numbers)
        {
            cout<<p[i].number<<p[i].name<<' '<<p[i].grade1<<' '<<p[i].grade2<<' '<<p[i].grade3<<' '<<endl;
        }

    }
}


void  SearchinName()
{
    stu m[50];
    int j=0;
    char names[50];
    cin.getline(names, 50, '\n');
    for (int i=0;i<z; i++)
    {
        if (strcmp(p[i].name, names)==0)
        {
            m[j]=p[i];j++;
        }
    }
        //以下是学号升序的冒泡排序
    for (int i=1;i<j;i++)
        {
            for (int s=i-1;s>=0;s--)
            {
                if (m[s].number==m[s+1].number) swap(m[s],m[s+1]);
                else break;
            }
        }
        //冒泡排序到此结束

    for (int i=0;i<j;i++)
    {
        cout<<m[i].number<<m[i].name<<' '<<m[i].grade1<<' '<<m[i].grade2<<' '<<m[i].grade3<<' '<<endl;
    }
}



void sortinNumber()
{
    if (z==1)  cout<<p[0].number<<p[0].name<<' '<<p[0].grade1<<' '<<p[0].grade2<<' '<<p[0].grade3<<' '<<endl;
    for (int i=1;i<z;i++)
        {
            for (int s=i-1;s>=0;s--)
            {
                if (p[s].number>p[s+1].number) swap(p[s],p[s+1]);
                else break;
            }
        }
    for (int i=0;i<z;i++)  cout<<p[i].number<<p[i].name<<' '<<p[i].grade1<<' '<<p[i].grade2<<' '<<p[i].grade3<<' '<<endl;
}


void sortinGrades()
{
    for (int i=0;i<z;i++)
    {
        p[i].grades=p[i].grade1+p[i].grade2+p[i].grade3;
    }
    if (z==1) cout<<p[0].number<<p[0].name<<' '<<p[0].grade1<<' '<<p[0].grade2<<' '<<p[0].grade3<<' '<<endl;
    else
    {for (int i=1;i<z;i++)
        {
            for (int s=i-1;s>=0;s--)
            {
                if (p[s].grades < p[s+1].grades) swap(p[s+1],p[s]);
                else break;
            }
        }
    int l=1;
    while (l<z)
    {   l++;
        int s=0;
        if (p[l].grades==p[l-1].grades)
        {
            int x=l-1;
            int lenth=1;
            while(p[x].grades==p[x+lenth].grades)
            {lenth++;}
            for (int w=x;w<x+lenth;w++)
            {
                for (int m=w;m>x;m--){
                if (p[m-1].number>p[m].number) swap(p[m-1],p[m]);
                else {l=x+lenth-1;break;}}
            }
        }

    }
    for (int i=0;i<z;i++)  cout<<p[i].number<<p[i].name<<' '<<p[i].grade1<<' '<<p[i].grade2<<' '<<p[i].grade3<<' '<<endl;
}
}






int main()
{
    while (true)
    {    int n;
         cin>>n;
    switch(n)
    {case 1:add();continue;
     case 2:change();continue;
     case 3: shanchu();continue;
     case 4: SearchinNumber();continue;
     case 5: SearchinName();continue;
     case 6:sortinNumber();continue;
     case 7: sortinGrades();continue;
     default: return 0;
    }
    }

}
