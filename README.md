# studend-database-
#include<stdio.h>
#include<string.h>
char filepath[50]="student.txt";
///Answer to the qsn no 1(c)
struct student
{
    char firstN[15],lastN[10],MatId[9],MobileNo1[20],MobileNo2[20];
    double cgpa[10];
    int sem;

};
void error()
{
    printf("File openning error\n Please try again or contact distributor\n\n");
}



///Answer to the qsn no 1(a)
void showInfo()
{

    FILE *studentDB;
    struct student s[100] ;
    int i,nos;
    studentDB=fopen(filepath,"r");
    if(!studentDB)
    {
        error();
        return;
    }
    i=0;
    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf ",&s[i].cgpa[j]);
        i++;

    }
    nos=i;
    fclose(studentDB);
    for(i=0; i<nos; i++)
    {
        printf("\n\n") ;
        printf("\t%s\n",s[i].firstN);
        printf("\t%s\n",s[i].lastN);
        printf("\t%s\n",s[i].MatId);
        printf("\t%s ",s[i].MobileNo1);
        printf("%s\n",s[i].MobileNo2);
        printf("\t%d\n",s[i].sem);
        printf("\tCGPA : ");
        for(int j=1; j<=s[i].sem; j++)
            printf("%.2lf ",s[i].cgpa[j]);
    }
}


///Answer to the qsn no 1(b)
void addInfo()
{

    FILE *studentDb;
    struct student s;
    studentDb = fopen(filepath,"a");
    if(!studentDb)
    {
        error();
        return;
    }
    printf("Enter First Name : ");
    scanf("%s",s.firstN);
    printf("Enter last Name : ");
    scanf("%s",s.lastN);
    printf("Enter Matric ID : ");
    scanf("%s",s.MatId);
    printf("Mobile No : ");
    scanf("%s %s\n",s.MobileNo1,s.MobileNo2);
    scanf("%d",&s.sem);
    printf("Enter CGPA of semester completed : ");
    for(int i=1; i<=s.sem; i++)
        scanf("%lf",&s.cgpa[i]);

    fprintf(studentDb,"%s\n%s\n%s\n%s %s\n%d\n",s.firstN,s.lastN,s.MatId,s.MobileNo1,s.MobileNo2,s.sem);
    for(int i=1; i<=s.sem; i++)
    {
        fprintf(studentDb,"%.2lf ",s.cgpa[i]);
    }
    fprintf(studentDb,"\n");

    printf("**********Data added successfully**********\n\n");
    fclose(studentDb);
}

///Answer to the qsn no 2(a)(i)

void deleteInfo()
{
    FILE *studentDB;
    struct student s[100] ;
    int i,nos,cmp;
    char delroll[10];
    studentDB=fopen(filepath,"r");
    if(!studentDB)
    {
        error();
        return;
    }
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }
    fclose(studentDB);
    nos=i;
    printf("Carefully enter the Metric ID you want to delete :");
    scanf("%s",delroll);
    studentDB=fopen(filepath,"w");
    for(i=0; i<nos; i++)
    {
        cmp= strcmp(delroll,s[i].MatId);
        if(cmp)
        {

            fprintf(studentDB,"%s\n%s\n%s\n%s %s\n%d\n",s[i].firstN,s[i].lastN,s[i].MatId,s[i].MobileNo1,s[i].MobileNo2,s[i].sem);
            for(int j=1; j<=s[i].sem; j++)
            {
                fprintf(studentDB,"%.2lf ",s[i].cgpa[j]);
            }
            fprintf(studentDB,"\n");
        }
    }
    fclose(studentDB);
    printf("**********Data delete successfully**********\n\n");
}

///Answer to the qsn no 2(a)(ii)
void showAvg()
{
    FILE *studentDB;
    struct student s[100] ;
    int i,nos,cmp;
    char avgroll[10];
    double y=0;
    printf("Enter the Metric ID you want to see average :");
    scanf("%s",avgroll);
    studentDB=fopen(filepath,"r");
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }
    fclose(studentDB);
    nos=i;

    for(i=0; i<nos; i++)
    {
        cmp= strcmp(avgroll,s[i].MatId);
        if(cmp==0)
        {
            for(int j=1; j<=s[i].sem; j++)
                y+=s[i].cgpa[j] ;
            break ;
        }
    }

    printf("%.2lf",y/s[i].sem);


}
///Answer to the qsn no 2(b)
void updateInfo()
{
    system( "color 02");
    FILE *studentDB;
    struct student s[100] ;
    int i,nos,cmp;
    char uproll[10];
    double upcgpa;

    studentDB=fopen(filepath,"r");
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }
    fclose(studentDB);
    nos=i;
    printf("Carefully enter the Metric ID you want to update :");
    scanf("%s",uproll);
    scanf("%lf",&upcgpa);
    studentDB=fopen(filepath,"w");
    for(i=0; i<nos; i++)
    {
        cmp= strcmp(uproll,s[i].MatId);
        if(cmp)
        {

            fprintf(studentDB,"%s\n%s\n%s\n%s %s\n%d\n",s[i].firstN,s[i].lastN,s[i].MatId,s[i].MobileNo1,s[i].MobileNo2,s[i].sem);
            for(int j=1; j<=s[i].sem; j++)
            {
                fprintf(studentDB,"%.2lf ",s[i].cgpa[j]);
            }
            fprintf(studentDB,"\n");
        }
        else if(cmp==0)
        {
            fprintf(studentDB,"%s\n%s\n%s\n%s %s\n%d\n",s[i].firstN,s[i].lastN,s[i].MatId,s[i].MobileNo1,s[i].MobileNo2,s[i].sem+1);
            for(int j=1; j<=s[i].sem; j++)
            {
                fprintf(studentDB,"%.2lf ",s[i].cgpa[j]);
            }
            fprintf(studentDB,"%.2lf\n",upcgpa);
        }
    }
    fclose(studentDB);
    printf("**********Data update successfully**********\n\n");

}
///for code
double showavg(char avgroll[])
{
    FILE *studentDB;
    struct student s[100] ;
    int i,nos,cmp;
    double y=0;
    studentDB=fopen(filepath,"r");
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }
    fclose(studentDB);
    nos=i;

    for(i=0; i<nos; i++)
    {
        cmp= strcmp(avgroll,s[i].MatId);
        if(cmp==0)
        {
            for(int j=1; j<=s[i].sem; j++)
                y+=s[i].cgpa[j] ;
            break ;
        }
    }
    return y/s[i].sem ;

}


///Answer to the qsn no 2(c)
void showBest()
{
    double  best,max=-0.00;
    FILE *studentDB;
    struct student s[100] ;
    int i,nos,cmp;
    char avgroll[10],maxid[10];

    studentDB=fopen(filepath,"r");
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }

    fclose(studentDB);
    nos=i;

    for(i=0; i<nos; i++)
    {
        best=showavg(s[i].MatId);
        if(best>max)
        {
            max=best;
            strcpy(maxid,s[i].MatId) ;
        }
    }
    for(i=0; i<nos; i++)
    {
        cmp= strcmp(maxid,s[i].MatId);
        if(cmp==0)
        {
            printf("\n\n") ;
            printf("\t%s\n",s[i].firstN);
            printf("\t%s\n",s[i].lastN);
            printf("\t%s\n",s[i].MatId);
            printf("\t%s ",s[i].MobileNo1);
            printf("\t%s\n",s[i].MobileNo2);
            printf("\t%d\n",s[i].sem);
            printf("\tCGPA : ");
            for(int j=1; j<=s[i].sem; j++)
                printf("%.2lf ",s[i].cgpa[j]);
            break ;
        }

    }

}

///Answer to the question no 3a(i) :
void showPG()
{
    FILE *studentDB;
    struct student s[100] ;
    int i,nos,k=1;
    char PGcode1[5]="017",PGcode2[5]="013";

    studentDB=fopen(filepath,"r");
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }
    fclose(studentDB);
    nos=i;
    for(i=0;i<nos;i++)
    {
        if(strcmp(PGcode1,s[i].MobileNo1)==0||strcmp(PGcode2,s[i].MobileNo1)==0)
        {
            printf("%d . %s %s\n",k,s[i].firstN,s[i].lastN);
            k++;
        }
    }

}

///Answer to the question no 3a(ii) :
void addNumCode()
{
   FILE *studentDB;
    struct student s[100] ;
    int i,nos,cmp;
    char addCode[10]="+88",code[10];

    studentDB=fopen(filepath,"r");
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }
    fclose(studentDB);

    nos=i;
    for(i=0;i<nos;i++)
    {
        strcpy(code,addCode);
        strcat(code,s[i].MobileNo1);
        strcpy(s[i].MobileNo1,code);
       //printf("%s ",s[i].MobileNo1);
    }
    for(i=0; i<nos; i++)
    {
        printf("\n\n") ;
        printf("\t%s\n",s[i].firstN);
        printf("\t%s\n",s[i].lastN);
        printf("\t%s\n",s[i].MatId);
        printf("\t%s ",s[i].MobileNo1);
        printf("%s\n",s[i].MobileNo2);
        printf("\t%d\n",s[i].sem);
        printf("\tCGPA : ");
        for(int j=1; j<=s[i].sem; j++)
            printf("%.2lf ",s[i].cgpa[j]);
    }
   /* studentDB=fopen(filepath,"w");
    for(i=0; i<nos; i++)
    {
           fprintf(studentDB,"%s\n%s\n%s\n%s %s\n%d\n",s[i].firstN,s[i].lastN,s[i].MatId,s[i].MobileNo1,s[i].MobileNo2,s[i].sem);
            for(int j=1; j<=s[i].sem; j++)
            {
                fprintf(studentDB,"%.2lf ",s[i].cgpa[j]);
            }
            fprintf(studentDB,"\n");
    }
    fclose(studentDB);
    showInfo();*/

}

///Answer to the question no 3b :
void sortShow()
{
    FILE *studentDB;
    struct student s[100],tamp ;
    int i,nos,cmp,k;
    double best[100];
    studentDB=fopen(filepath,"r");
    i=0;

    while(fscanf(studentDB,"%s",&s[i].firstN)==1)
    {
        fscanf(studentDB,"%s%s%s%s\n%d",&s[i].lastN,&s[i].MatId,&s[i].MobileNo1,&s[i].MobileNo2,&s[i].sem);

        for(int j=1; j<=s[i].sem; j++)
            fscanf(studentDB,"%lf",&s[i].cgpa[j]);
        i++;
    }
    fclose(studentDB);
    nos=i;


    for(i=0; i<nos; i++)
    {
        best[i]=showavg(s[i].MatId);
    }
    for(i=0; i<nos; i++)
        for(k=i+1; k<nos; k++)
        {
            if(best[i]<best[k])
            {
                tamp=s[i];
                s[i]=s[k];
                s[k]=tamp;
            }
        }

    studentDB=fopen(filepath,"w");
    for(i=0; i<nos; i++)
    {

        fprintf(studentDB,"%s\n%s\n%s\n%s %s\n%d\n",s[i].firstN,s[i].lastN,s[i].MatId,s[i].MobileNo1,s[i].MobileNo2,s[i].sem);
        for(int j=1; j<=s[i].sem; j++)
        {
            fprintf(studentDB,"%.2lf ",s[i].cgpa[j]);
        }
        fprintf(studentDB,"\n");
    }

    fclose(studentDB);

    showInfo();

}


int showchoice()
{

    int choice ;
    printf("\n\n\nIIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC");
    printf("\n\n\t\t\tWelcome to IIUC");
    printf("\n\n\t1.Show Information\n");
    printf("\t2.Add new Information\n");
    printf("\t3.Delete a Information\n");
    printf("\t4.Show your average CGPA \n");
    printf("\t5.Update Information \n");
    printf("\t6.Best Student  \n");
    printf("\t7.Show GP operator   \n");
    printf("\t8.Add Number Code(+88)  \n");
    printf("\t9.Serial by result  \n");
    printf("\t10.Exit \n");
    printf("IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC IIUC\n");
    printf("Enter your choice : ");
    scanf("%d",&choice);

    return choice;
}


///main program
int main()
{
    int choice ;
    do
    {
        choice=showchoice() ;
        switch(choice)
        {
        case 1 :
            showInfo() ;
            break;
        case 2:
            addInfo() ;
            break;
        case 3 :
            deleteInfo() ;
            break;
        case 4:
            showAvg() ;
            break ;
        case 5 :
            updateInfo() ;
            break;
        case 6 :
            showBest() ;
            break;
        case 7 :
            showPG();
            break;
        case 8:
            addNumCode();
            break;
        case 9:
            sortShow();
            break ;
        }

    }
    while(choice!=10);



    return 0;
}

