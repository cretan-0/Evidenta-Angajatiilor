# Evidenta-Angajatiilor

#include<iostream>
#include<conio.h>
#include<stdio.h>
#include<stdlib.h>
#include<cstdlib>
#include<fstream>
using namespace std;

class Angajat //cl bz
{

    friend class Modificari;

private:
    int ID_angajat, salariu,salariu_baza, ID_sectie, test_ID;
    string nume, prenume, date_personale, data_angajarii, postul_ocupat;
    fstream file, file1, file2, file3;
    int found=0;
    double spor_vechime;
    double spor_stres;
    double spor_pericol;
    double CAS;
    double CASS;
    double CFS;
    double Impozit;

public:
    void angajare();
    void afisare_angajati();
    void cautare_angajat();
    void modificare_angajat();
    void concediere_angajat();
    void sectie();
    void cautare_sectie();
};
void Angajat::angajare()
{
    int test_id,found=0;
    fstream file,file1;
    cout<<"\n\n\t\t\t\tAngajare persoana!";
    cout<<"\n\ID angajat: ";
    cin>>ID_angajat;
    cout<<"Nume angajat: ";
    cin>>nume;
    cout<<"Prenume angajat: ";
    cin>>prenume;
    cout<<"Salariu de baza angajat: ";
    cin>>salariu_baza;
    cout<<"Spor periculozitate[%]: ";
    cin>>spor_pericol;
    cout<<"Spor de stres[%]: ";
    cin>>spor_stres;
    cout<<"Spor de vechime[%]: ";
    cin>>spor_vechime;
    cout<<"CAS[%]: ";
    cin>>CAS;
    cout<<"CASS[%]: ";
    cin>>CASS;
    cout<<"CFS[%]: ";
    cin>>CFS;
    cout<<"Impozit[%]: ";
    cin>>Impozit;
    salariu = salariu_baza + (salariu_baza*(spor_pericol+spor_stres+spor_vechime)/100) - (salariu_baza*(CAS+CASS+CFS+Impozit)/100);
    cout<<"Salariu net: "<<salariu;
    cout<<"\nDate personale: ";
    cin>>date_personale;
    cout<<"Data angajarii: ";
    cin>>data_angajarii;
    cout<<"Postul ocupat: ";
    cin>>postul_ocupat;
    cout<<"ID sectie: ";
    cin>>ID_sectie;
    file.open("Angajati.txt",ios::out|ios::app);
    file<<" "<<ID_angajat<<" "<<nume<<" "<<prenume<<" "<<salariu<<" "<<date_personale<<" "<<data_angajarii<<" "<<postul_ocupat<<" "<<ID_sectie<<"\n";
    file.close();
    file1.open("Sectie.txt",ios::out|ios::app);
    file1<<" "<<ID_sectie<<" "<<ID_angajat<<" "<<salariu<<"\n";
    file1.close();
    file.open("Sectieid.txt",ios::in);
    if(!file)
    {
        file1.open("Sectieid.txt",ios::app|ios::out);
        file1<<" "<<ID_sectie<<"\n";
        file1.close();
    }
    else
    {
        file>>test_id;
        while(!file.eof())
        {
            if(test_id == ID_sectie)
                found++;
            file>>test_id;
        }
        file.close();
        if(found == 0)
        {
            file1.open("Sectieid.txt",ios::app|ios::out);
            file1<<" "<<ID_sectie<<"\n";
            file1.close();
        }
    }
    cout<<"\n\nAngajarea s-a realizat!";
}
void Angajat::afisare_angajati()
{
    system("cls");
    fstream file;
    cout<<"\n\n\t\t\t\tAfisare angajat!";
    file.open("Angajati.txt",ios::in);
    if(file.eof())
    {
        cout<<"\n\nEroare deschidere fisier!afisare";
        getch();
    }
    file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;
    while(!file.eof())
    {


        cout<<"\n\nAngajat ID: "<<ID_angajat;
        cout<<"\nNume angajat: "<<nume;
        cout<<"\nPrenume angajat: "<<prenume;
        cout<<"\nSalariu angajat (net): "<<salariu;
        cout<<"\nDate personale angajat: "<<date_personale;
        cout<<"\nData angajarii: "<<data_angajarii;
        cout<<"\nPostul ocupat: "<<postul_ocupat;
        cout<<"\nID sectie: "<<ID_sectie;

        file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;
    }
    file.close();
}


class Modificari: public Angajat
{

public:
    void cautare_angajat()
    {
        system("cls");
        fstream file;
        int IDD_angajat,found=0;
        cout<<"\n\nCautare angajat";
        file.open("Angajati.txt",ios::in);
        if(!file)
        {
            cout<<"\n\nEroare deschidere fisier...";
            getchar();

        }
        cout<<"\n\nID Angajat pentru cautare: ";
        cin>>IDD_angajat;

        file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;
        while(!file.eof())
        {
            if(IDD_angajat == ID_angajat)
            {
                system("cls");
                cout<<"\n\n\t\t\t Cautare angajat";
                cout<<"\n\nID Angajat: "<<ID_angajat;
                cout<<"\nNume Angajat: "<<nume;
                cout<<"\nPrenume Angajat: "<<prenume;
                cout<<"\nSalariu angajat (net): "<<salariu;
                cout<<"\nDate personale Angajat: "<<date_personale;
                cout<<"\nData angajarii: "<<data_angajarii;
                cout<<"\nPostul ocupat: "<<postul_ocupat;
                cout<<"\nID sectie: "<<ID_sectie;
                found++;
            }
            file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;
        }
        file.close();
        if(found == 0)
            cout<<"\n\nID-ul angajatului nu a fost gasit, incearca alt ID";
    }
    void modificare_angajat()
    {
        int salariu1,salariu_baza1, test_ID, found=0;
        string nume1, prenume1, date_personale1, data_angajarii1, postul_ocupat1;
        fstream file, file1, file2, file3;
        cout<<"\n\nModificare angajat\n";
        file.open("Angajati.txt", ios::in);
        file1.open("Sectie.txt", ios::in);
        cout<<"ID-ul angajatului pe care dorim sa-l modificam: ";
        cin>>test_ID;
        file2.open("Angajati1.txt", ios::app | ios::out);
        file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;
        while(!file.eof())
        {
            if(test_ID == ID_angajat)
            {
                cout<<"Acum modificam datele angajatului:";
                cout<<endl;
                cout<<"Nume angajat: ";
                cin>>nume1;
                cout<<"Prenume angajat: ";
                cin>>prenume1;
                cout<<"Salariu de baza angajat: ";
                cin>>salariu_baza1;
                cout<<"Spor periculozitate[%]: ";
                cin>>spor_pericol;
                cout<<"Spor de stres[%]: ";
                cin>>spor_stres;
                cout<<"Spor de vechime[%]: ";
                cin>>spor_vechime;
                cout<<"CAS[%]: ";
                cin>>CAS;
                cout<<"CASS[%]: ";
                cin>>CASS;
                cout<<"CFS[%]: ";
                cin>>CFS;
                cout<<"Impozit[%]: ";
                cin>>Impozit;
                salariu1 = salariu_baza1 + (salariu_baza1*(spor_pericol+spor_stres+spor_vechime)/100) - (salariu_baza1*(CAS+CASS+CFS+Impozit)/100);
                cout<<"Salariu net: "<<salariu1;
                cout<<"\nDate personale angajat: ";
                cin>>date_personale1;
                cout<<"Data angajarii angajat: ";
                cin>>data_angajarii1;
                cout<<"Postul ocupat angajat: ";
                cin>>postul_ocupat1;
                cout<<"ID sectie: ";
                cin>>ID_sectie;
                file2<<" "<<ID_angajat<<" "<<nume1<<" "<<prenume1<<" "<<salariu1<<" "<<date_personale1<<" "<<data_angajarii1<<" "<<postul_ocupat1<<" "<<ID_sectie<<"\n";
                found++;

            }
            else
            {
                file2<<" "<<ID_angajat<<" "<<nume<<" "<<prenume<<" "<<salariu<<" "<<date_personale<<" "<<data_angajarii<<" "<<postul_ocupat<<" "<<ID_sectie<<"\n";
            }
            file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;

        }
        file.close();
        file2.close();
        remove("Angajati.txt");
        rename("Angajati1.txt", "Angajati.txt");
        file3.open("Sectie1.txt", ios::app|ios::out);
        file1>>ID_sectie>>ID_angajat>>salariu;
        while(!file.eof())
        {
            if(test_ID == ID_angajat)
                file3<<" "<<ID_sectie<<" "<<ID_angajat<<" "<<salariu1<<"\n";
            else
                file3<<" "<<ID_sectie<<" "<<ID_angajat<<" "<<salariu<<"\n";
            file1>>ID_sectie>>ID_angajat>>salariu;
        }
        file1.close();
        file3.close();
        remove("Sectie.txt");
        rename("Sectie1.txt", "Sectie.txt");
        if(found==0)
            cout<<"\n\nID-ul angajatului nu a fost gasit!";
        else
            cout<<"\n\nAngajat modificat cu succes!";
    }
    void concediere_angajat()
    {
        system("cls");
        cout<<"\n\nConcediere Angajat!";
        file.open("Angajati.txt", ios::in);
        file1.open("Sectie.txt",ios::in);
        cout<<"\n\nID-ul angajat pentru concediere: ";
        cin>>test_ID;
        file2.open("Angajati1.txt", ios::app|ios::out);
        file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;
        while(!file.eof())
        {
            if(test_ID==ID_angajat)
            {
                cout<<"\n\nAngajatul este concediat!";
                //found++;
            }
            else
            {
                file2<<" "<<ID_angajat<<" "<<nume<<" "<<prenume<<" "<<salariu<<" "<<date_personale<<" "<<data_angajarii<<" "<<postul_ocupat<<" "<<ID_sectie<<"\n";
            }
            file>>ID_angajat>>nume>>prenume>>salariu>>date_personale>>data_angajarii>>postul_ocupat>>ID_sectie;
        }
        file.close();
        file2.close();
        remove("Angajati.txt");
        rename("Angajati1.txt", "Angajati.txt");
        file3.open("Sectie1.txt",ios::app|ios::out);
        file1>>ID_sectie>>ID_angajat>>salariu;
        while(!file.eof())
        {
            if(test_ID != ID_angajat)
                file3<<" "<<ID_sectie<<" "<<ID_angajat<<" "<<salariu<<"\n";
            file1>>ID_sectie>>ID_angajat>>salariu;
        }
        file1.close();
        file3.close();
        remove("Sectie.txt");
        rename("Sectie1.txt", "Sectie.txt");
        if(found==0)
            cout<<"\n\nID-ul angajatului nu a fost gasit!";


    }

};
class Grup: public Angajat, public Modificari
{

private:
    int ID_sectie, ID_angajat, salariu;
    int test_ID, found=0, nr_angajati=0, nr_salariu=0;

public:
    void sectie()
    {
        system("cls");
        fstream file;
        cout<<"Sectia angajatului: ";
        file.open("Sectie.txt", ios::in);
        if(!file)
        {
            cout<<"\n\nEroare deschidere fisier!";
            getch();
        }
        file>>ID_sectie>>ID_angajat>>salariu;
        while(!file.eof())
        {
            cout<<"\n\nID Sectie: "<<ID_sectie;
            cout<<"\nID Angajat: "<<ID_angajat;
            cout<<"\nSalariu Angajat: "<<salariu;
            file>>ID_sectie>>ID_angajat>>salariu;
        }
        file.close();
    }
    void cautare_sectie()
    {
        cout<<"\n\nCautare sectie angajati!";
        fstream file;
        file.open("Sectie.txt", ios::in);
        if(!file)
        {
            cout<<"Eroare deschidere fisier!";
            getch();
        }
        cout<<"\n\nID-ul sectiei pentru cautare: ";
        cin>>test_ID;
        system("cls");
        cout<<"\n\nCautare sectie angajat:";
        cout<<endl;
        file>>ID_sectie>>ID_angajat>>salariu;
        while(!file.eof())
        {
            if(test_ID==ID_sectie)
            {
                cout<<"ID Sectie: "<<ID_sectie<<"\n\n";
                cout<<"ID Angajat: "<<ID_angajat<<"\n\n";
                cout<<"Salariu Angajat: "<<salariu<<"\n\n";
                found++;
                nr_angajati++;
                nr_salariu = nr_salariu + salariu;
            }
            file>>ID_sectie>>ID_angajat>>salariu;
        }
        file.close();
        if(found != 0)
        {
            cout<<"ID Sectie: "<<test_ID<<"\n";
            cout<<"Total angajati: "<<nr_angajati<<"\n";
            cout<<"Total salariu sectie: "<<nr_salariu<<"\n";
        }
        else
        {
            cout<<"ID-ul sectiei nu a fost gasit!";
        }

    }


};
int main()
{
    Angajat e;
    Modificari r;
    Grup p;


    int x;
    do
    {
        cout<<"\nMeniul de comanda!";
        cout<<endl;
        cout<<"Alege o comanda[1-8]: ";
        cout<<endl;
        cout<<"[1] Angajare";
        cout<<endl;
        cout<<"[2] Afisare";
        cout<<endl;
        cout<<"[3] Cautare angajat";
        cout<<endl;
        cout<<"[4] Modificare angajat";
        cout<<endl;
        cout<<"[5] Concediere angajat";
        cout<<endl;
        cout<<"[6] Sectia angajatului";
        cout<<endl;
        cout<<"[7] Cautare sectie";
        cout<<endl;
        cout<<"[8] Iesire";
        cout<<endl;
        cin>>x;
        switch(x)
        {
        case 1:
            e.angajare();
            break;
        case 2:
            e.afisare_angajati();
            break;
        case 3:
            r.cautare_angajat();
            break;
        case 4:
            r.modificare_angajat();
            break;
        case 5:
            r.concediere_angajat();
            break;
        case 6:
            p.sectie();
            break;
        case 7:
            p.cautare_sectie();
            break;
        case 8:
            cout<<"Iesire cu succes din program!";
            exit(0);
        default:
            cout<<"\n\n[Eroare]\nIncearca alta valoare.\n";

        }
    }
    while(x!=8);
}
