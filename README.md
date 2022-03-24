# C-learning
learning C++ (loops, basics of object-oriented approach)


przyg.egz

//Zad. 1

// Example program
#include <iostream>
#include <string>
#include <vector>
using namespace std;

class Pomiary
{
    public:
    vector<int> pom;
    void dodaj(int wartosc);
    int ilePomiarow();
    double srednia();
    int najwiekszy();
};

void Pomiary::dodaj(int wartosc)
{
    pom.push_back(wartosc);
}

int Pomiary::ilePomiarow()
{
    return pom.size();
}    

double Pomiary::srednia()
{
    double s=0;
    for(int i=0; i<ilePomiarow(); i++) s+=pom[i];
    return s/ilePomiarow();
}

int Pomiary::najwiekszy()
{
    int m=pom[0];
    for(int i=1; i<ilePomiarow(); i++)
    {
        if(pom[i]>m) m = pom[i];
    }
    return m;
}

int main()
{
    Pomiary a;
    a.dodaj(4);
    a.dodaj(5);
    
    cout << a.pom[0] << endl;
    cout << a.pom[1] << endl;
    cout << a.ilePomiarow() << endl;
    cout << a.srednia() << endl;
    cout << a.najwiekszy() << endl;
}

//zad. 2

class Napis
{
    string s;
    public:
    Napis()
    {
        s="";
    }
    Napis(char* s1)
    {
        s=s1;
    }
    void dolacz(char znak);
    char znak(int pozycja);
    void wypisz();
    
};

void Napis::dolacz(char znak)
{
    s.push_back(znak);
}

char Napis::znak(int pozycja)
{
    return s[pozycja];
}

void Napis::wypisz()
{
    cout << s << endl;
}

int main()
{
   Napis s="Honorata";
   s.wypisz();
   s.dolacz('B');
   s.wypisz();
   cout << s.znak(1) << endl;
}

//zad. 3

struct Punkt 
{
     double x;
     double y;
};

class Trojkat
{
    Punkt a, b, c;
    public:
    Trojkat(Punkt p1, Punkt p2, Punkt p3)
    {
        a=p1;
        b=p2;
        c=p3;
    }
    void przesun(double dx, double dy);
    bool nalezy(Punkt p);
    bool operator==(Trojkat t);
};

bool Trojkat::operator==(Trojkat t)
{
    if(a.x==t.a.x) return 1;
    return 0;
}

// trzeba sprawdzić też pozostałe współrzędne

void Trojkat::przesun(double dx, double dy)
{
    a.x+=dx;
    b.x+=dx;
    c.x+=dx;
    a.y=+dy;
    b.y+=dy;
    c.y+=dy;
}

bool Trojkat::nalezy(Punkt p)
{
    double xmax, ymax, xmin, ymin;
    if(a.x>=b.x && a.x>=c.x)
    {
        xmax=a.x;
        if(b.x<c.x) xmin=b.x;
        else xmin=c.x;
    }
    else if(b.x>=a.x && b.x>=c.x)
    {
        xmax=b.x;
        if(a.x<c.x) xmin=a.x;
        else xmin=c.x;
    }
    else
    {
        xmax=c.x;
        if(a.x>b.x) xmin=b.x;
        else xmin=a.x;
    }
    if(p.x<=xmin || p.x >= xmax) return 0;
    
    if(a.y>=b.y && a.y>=c.y)
    {
        ymax=a.y;
        if(b.y<c.y) ymin=b.y;
        else ymin=c.y;
    }
    else if(b.y>=a.y && b.y>=c.y)
    {
        ymax=b.y;
        if(a.y<c.y) ymin=a.y;
        else ymin=c.y;
    }
    else
    {
        ymax=c.y;
        if(a.y>b.y) ymin=b.y;
        else ymin=a.y;
    }
    cout << xmin << endl << xmax << endl << ymin << endl << ymax << endl;
    if(p.y<=ymin || p.y >= ymax) return 0;
  return 1;
}

int main()
{
    Punkt a;
    a.x=0;
    a.y=0;
    Punkt b;
    b.x=1;
    b.y=1;
    Punkt c;
    c.x=0;
    c.y=1;
    Trojkat s(a,b,c);
    Punkt p;
    p.x=0.5;
    p.y=0.5;
   // cout << s.nalezy(p) << endl;
    //s.przesun(100,100);
    //cout << s.nalezy(p);
    Trojkat t(a,b,c);
    if(t==s) cout << "ok";
}

//zad. 4

class Osoba
{
    public:
    string i, n;
    int w;
    Osoba(char* imie, char* nazwisko)
    {
        i=imie;
        n=nazwisko;
    }
    void ustawWiek(int wiek);
    bool starszaNiz(const Osoba& osoba);
    bool imiennik(const Osoba& osoba);
    
};

void Osoba::ustawWiek(int wiek)
{
    w=wiek;
}

bool Osoba::starszaNiz(const Osoba& osoba)
{
    if(w>osoba.w) return 1;
    return 0;
}

bool Osoba::imiennik(const Osoba& osoba)
{
    if(i==osoba.i) return 1;
    return 0;
}

int main()
{
    Osoba A("Honorata", "Bogusz");
    Osoba B("Julia", "Wittlieb");
    A.ustawWiek(21);
    B.ustawWiek(22);
    cout << A.starszaNiz(B) << endl;
    cout << A.imiennik(B) << endl;
}

//zad. 5

class tablica
{
    public:
    int r;
    vector<int> t;
    tablica(int maksymalnyRozmiar)
    {
        r=maksymalnyRozmiar;
    }
    void dodaj(int war);
    bool usun(int war);
    void wyswietl()
    {
        for(int i=0; i<t.size(); i++) cout << t[i];
        cout << endl;
    }
    
};

void tablica::dodaj(int war)
{
    t.push_back(war);
    
    int rozmiar=t.size();
    for(int k=0;k<rozmiar;k++)
    {
        for(int i=0;i<rozmiar;i++)
        {
            int x=0;
            if(t[i]>t[i+1])
            {
                x=t[i+1];
                t[i+1]=t[i];
                t[i]=x;
            }
            for(int j=0;j<rozmiar;j++)
            {
                //cout << t[j];
            }
            //cout << endl;
        }
    }
}

bool tablica::usun(int war)
{
    bool jest=0;
    int p;
    for(int i=0; i<t.size() && !jest; i++)
    {
        if(t[i]==war) {jest=1; p=i;}
    }
    
    for(int i=p; i<t.size()-1; i++)
    {
        t[i]=t[i+1];
    }
    if(jest) t.pop_back();
    
    return jest;
}

int main()
{
    tablica a(5);
    a.dodaj(1);
    a.wyswietl();
    a.dodaj(3);
    a.wyswietl();
    a.dodaj(2);
    a.wyswietl();
    a.t.push_back(3);
    a.wyswietl();
    cout << a.usun(2) << endl;
}

//zad. 6

class Konto
{
    public:
    vector <int> v;
    int stanKonta();
    void zmien(int oIle);
    int sumaUznan();
    int sumaObciazen();

};

int Konto::stanKonta()
{
    int suma=0;
    for(int i=0;i<v.size();i++)
    {
        suma+=v[i];
    }
    return suma;
}

void Konto::zmien(int oIle)
{
    v.push_back(oIle);
}

int Konto::sumaUznan()
{
    int suma=0;
    for(int i=0;i<v.size();i++)
    {
        if(v[i]>0) suma+=v[i];
    }
    return suma;
}

int Konto::sumaObciazen()
{
    int suma=0;
    for(int i=0;i<v.size();i++)
    {
        if(v[i]<0) suma+=v[i];
    }
    return suma;
}

int main()
{
    Konto A;
    A.zmien(-50);
    cout << A.stanKonta() << endl;
}

//zad. 12

class Znajomi
{
    int **t;
    int n;
public:
    Znajomi(int n1)
    {
        n = n1;
        t = new int*[n];
        for(int i=0; i<n; i++) t[i] = new int[n];
        for(int i=0; i<n; i++)
            for(int j=0; j<n; j++) t[i][j]=0;
    }
    bool zna(int a, int b);
    void poznaj(int a, int b);
    void wspolniZnajomi(int a, int b);
    void spotkanie(int a);
    int max();
    void wypisz();
};

bool Znajomi::zna(int a, int b)
{
    if(t[a][b]==true) return 1;
    return 0;
}

void Znajomi::poznaj(int a, int b)
{
    t[a][b] = 1;
    t[b][a] = 1;
}

void Znajomi::wspolniZnajomi(int a, int b)
{
    cout << "Wspolni znajomi: ";
    for(int i=0; i<n; i++)
    {
        if(t[a][i] == 1 && t[b][i] == 1 && i!= a && i!=b) cout << i << " ";
    }
    cout << endl;
}

void Znajomi::spotkanie(int a)
{
    for(int i=0; i<n; i++)
    {
        if(t[a][i] == 1)
        {
            for(int j=0; j<n; j++)
            {
                if(t[a][j] == 1) t[i][j] = 1;
            }
        }
    }
}
        
int Znajomi::max()
{
    int m=0;
    int mi=0;
    int p;
    
    for(int i=0; i<n; i++)
    {
        p=0;
        for(int j=0; j<n; j++)
        {
            if(i!=j && t[i][j] == 1) p++;
        }
        if(p>m) {m=p; mi=i;}
    }
    return mi;
}

void Znajomi::wypisz()
{
    for(int i=0; i<n; i++)
    {
        for(int j=0; j<n; j++)
            cout << t[i][j];
        cout << endl;
    }
}

int main()
{
    Znajomi z(5);
    z.poznaj(0,1);
    z.poznaj(0,2);
    cout << z.zna(0,1) << endl;
    z.spotkanie(0);
    cout << z.zna(1,2) << endl;
    cout << z.max() << endl;
    z.wypisz();
    z.wspolniZnajomi(1,2);
}

//zad. 13

class Karta { public: int kolor; int ranga; };

class ZbiorKart
{
    public:
    vector<Karta> k;
    void dodaj(Karta k);
    int ileWKolorze(int kolor);
    Karta losowa();
};

void ZbiorKart::dodaj(Karta kn)
{
    k.push_back(kn);
}

int ZbiorKart::ileWKolorze(int kolor1)
{
    int liczba=0;
    for(int i=0;i<k.size();i++)
    {
        if(k[i].kolor==kolor1) liczba++;
    }
    return liczba;
};

Karta ZbiorKart::losowa()
{
    srand(time(NULL));
    int n=rand()%k.size();
    return k[n];
}


int main()
{
    ZbiorKart A;
    Karta B;
    B.kolor=1;
    B.ranga=13;
    A.dodaj(B);
    cout << A.ileWKolorze(1) << endl;
    Karta C=A.losowa();
    cout << C.kolor << " ," << C.ranga << endl;
}

zad. 14

class Kolo
{
    public:
    double x,y,r;
    Kolo(double x1, double y1, double r1)
    {
        x=x1;
        y=y1;
        r=r1;
    }
    void przesun(double dx, double dy);
    bool zawiera(double a, double b);
    bool zawiera1(Kolo k);
    Kolo przechodzace(double x, double y);
    
};

void Kolo::przesun(double dx, double dy)
{
    x+=dx;
    y+=dy;
}

bool Kolo::zawiera(double a, double b)
{
    if(sqrt((x-a)*(x-a)+(y-b)*(y-b))<+r) return 1;
    return 0;
}

bool Kolo::zawiera1(Kolo k)
{
    double odl=sqrt((x-k.x)*(x-k.x)+(y-k.y)*(y-k.y));
    if( odl+k.r<=r) return 1;
    return 0;
}

Kolo Kolo::przechodzace(double x2, double y2)
{
    double R=sqrt((x-x2)*(x-x2)+(y-y2)*(y-y2));
    Kolo N(x,y,R);
    return N;
}

int main()
{
    Kolo A(0,0,1);
    A.przesun(1,1);
    cout << A.x << "," << A.y << " " << A.r << endl;
    cout << A.zawiera(-1,-1) << endl;
    Kolo B(1,1,0.5);
    cout << A.zawiera1(B) << endl;
    Kolo C=A.przechodzace(5,5);
    cout << C.x << "," << C.y << "," << C.r << endl;
}

zad. 23

class Plansza
{
    int n;
    int **t;
    Plansza(int r)
    {
        t = new int*[r];
        for(int i=0; i<r; i++) t[i] = new int[r];
// te dwie linijki zawsze piszemy przy wskaźnikach,gdy nie mamy rozmiaru i musimy go nadać
        for(int i=0;i<r;i++)
        {
            for(int j=0;j<r;j++)
            {
                t[i][j]=0;
            }
        }
        n=r;
    }
    void umiesc(int x, int y);
    int ile();
    int sasiedzi(int x, int y);
    void usun();
};

void Plansza::umiesc(int x, int y)
{
    t[x][y]=1;
}

int Plansza::ile()
{
    int suma=0;
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            if(t[i][j]==1) suma++;
        }
    }
    return suma;
}

int Plansza::sasiedzi(int x, int y)
{
    int r=n;
    int liczba=0;
    if(t[x-1][y-1]==1 && (x-1)>=0 && (y-1)>=0) liczba++;
    if(t[x-1][y]==1 && (x-1)>=0) liczba++;
    if(t[x-1][y+1]==1 && (x-1)>=0 && (y+1)<r) liczba++;
    if(t[x][y-1]==1 && (y-1)>=0) liczba++;
    if(t[x][y+1]==1 && (y+1)<r) liczba++;
    if(t[x+1][y-1]==1 && (x+1)<r && (y-1)>=0) liczba++;
    if(t[x+1][y]==1 && (x+1)<r) liczba++;
    if(t[x+1][y+1]==1 && (x+1)<r && (y+1)<r) liczba++;
    return liczba;
}

void Plansza::usun()
{
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            if(sasiedzi(i,j)>2) t[i][j]=0;
        }
    }
}

zad. 20/21

class Liczby
{
    public:
    int r;
    int *t;
    Liczby(int n)
    {
        t = new int[n];
        for(int i=0;i<n;i++)
        {
            t[i]=0;
        }
        r=n;
    }
    int sumaElementow();
    void dodaj(int a, int b);
    bool zawiera(Liczby& z);
    Liczby suma(Liczby& z);
};

int Liczby::sumaElementow()
{
    int suma=0;
    for(int i=0;i<r;i++)
        if(t[i]==1) suma+=i;
    return suma;
}

void Liczby::dodaj(int a, int b)
{
    for(int i=a; i<=b-1; i++)
        t[i]=1;
}

bool Liczby::zawiera(Liczby& z)
{
    for(int i=0;i<r && i<z.r;i++)
        if(t[i]==0 && z.t[i]==1) return 0;
    if(z.r<r) return 1;
    for(int i=r;i<z.r;i++) 
        if(z.t[i]==1) return 0;
    return 1;
}

Liczby Liczby::suma(Liczby& z)
{
    int p;
    if(z.r<r) p=r;
    else p=z.r;
    Liczby a(p);
    for(int i=0;i<r;i++)
    {
        if(t[i]==1) a.t[i]=1;
    }
    for(int i=0;i<z.r;i++)
    {
        if(z.t[i]==1) a.t[i]=1;
    }
    return a;
}
 
int main()
{
    Liczby A(10);
    cout << A.sumaElementow() << endl;
    A.dodaj(1,3);
    Liczby B(12);
    cout << A.zawiera(B) << endl;
    B.dodaj(1,2);
    Liczby C=A.suma(B);
    for(int i=0;i<C.r;i++)
    {
        cout << C.t[i] << " ";
    }
}

//zad. 16

class Macierz
{
    public:
    int t**;
    Macierz(int r): rozm(r)
    {
        t=new int*[r];
        for(int i=0;i<r;i++)
        {
            t[i]=new int[r];
            for(int j=0;j<r;j++)
            t[i][j]=0;
        }
    }
    Macierz(int r, int x): rozm(r)
    {
        t=new int*[r];
        for(int i=0;i<r;i++)
        {
            t[i]=new int[r];
            for(int j=0;j<r;j++)
            if(i==j) t[i][j]=x;
            else t[i][j]=0;
        }
    }
    Macierz suma(Macierz& m)
    {
        Macierz c(rozm);
        for(int i=0;i<rozm;i++)
        {
            for(int j=0;j<rozm;j++)
            {
                c.t[i][j]=m.t[i][j]+t[i][j];
            }
        }
        return c;
    }
    double slad();
    void trans();
    double min();
    private:
    int rozm;
}

double Macierz::slad()
{
    int suma=0;
    for(int i=0;i<rozm;i++)
    {
        for(int j=0;j<rozm;j++)
        {
            if(i==j) suma+=t[i][j];
        }
    }
    return suma;
}

void Macierz::trans()
{
    for(int i=0;i<rozm;i++)
    {
        for(int j=0;j<i;j++)
        {
            int pom=t[i][j];
            t[i][j]=t[j][i];
            t[j][i]=pom;
        }
    }
}

double Macierz::min()
{
    int min1=t[0][0];
    for(int i=0;i<rozm;i++)
    {
        for(int j=0;j<rozm;j++)
        {
            if(t[i][j]<min1) min1=t[i][j];
        }
    }
    return min1;
}


//zad. 19

class Odcinek
{
    public:
    Odcinek(double x1, double y1, double x2, double y2): a(x1), b(x2), c(y1), d(y2) {}
    double a, b, c, d;
    void przesun(double dx, double dy);
    double dlugosc();
    bool rownolegly(Odcinek o);
    bool przecina(Odcinek o);
};

void Odcinek::przesun(double dx, double dy)
{
    a=a+dx;
    b=b+dx;
    c=c+dy;
    d=d+dy;
    cout << a << "," << b << "," c << "," << d << endl;
}

double Odcinek::dlugosc()
{
    double dl=0;
    dl=sqrt((a-b)*(a-b)+(c-d)*(c-d));
    cout << dl << endl;
    return dl;
}

bool Odcinek::rownolegly(Odcinek o)
{
    double tango=abs(a-b)/abs(c-d);
    double tango2=abs(o.a-o.b)/abs(o.c-o.d);
    if(tango==tango2) return 1;
    return 0;
}

//zad. 7

class Histogram
{
    public:
    int ile=0;
    int *t; // t to tablica przedziałów, nie wartości !!!
    Histogram(double min, double max, int i): min1(min), max1(max), n(i)
    {
        t=new int [i];
        for(int j=0;j<ile;j++)
            t[j]=0;
    }
    double min1,max1;
    int n;
    void dodaj(double wartosc);
    int ileWPrzedziale(int numer);
    int ilePozaZakresem();
};

void Histogram::dodaj(double wartosc)
{
     int dl=(max1-min1)/n;
     if(wartosc>max1 || wartosc<min1)
     {
         ile++;
         return;
     }
     for(int i=0;i<n;i++)
     {
         if(wartosc>=min1+dl*i && wartosc<min1+dl*(i+1)) t[i]++;
     }
}

int Histogram::ileWPrzedziale(int numer)
{
    return t[numer-1];
}

int Histogram::ilePozaZakresem()
{
    return ile;
}

int main()
{
    Histogram A(1,10,2);
    A.dodaj(2);
    cout << "Talica po dodaniu 2 ";
    for(int i=0;i<A.n;i++) cout << A.t[i] << " ";
    cout << endl;
    cout << A.ileWPrzedziale(2) << endl;
    A.dodaj(11);
    cout << A.ilePozaZakresem();
}

//zad. 15

class Prostokat
{
    Prostokat(double x1, double y1, double x2, double y2): a(x1), b(x2), c(y1), d(y2) {}
    double a,b,c,d;
    Prostokat(double x, double y, double p): a(x-p/2), b(y-p/2), c(x+p/2), d(y+p/2) {}
    double pole();
    Prostokat czescWspolna(Prostokat p);
    void powieksz(double c);
};

double Prostokat::pole()
{
    int pole=0;
    pole=abs(b-a)*abs(d-c);
    return pole;
}

Prostokat Prostokat::czescWspolna(Prostokat p)
{
    Prostokat C;
    if(p.a>=a && p.a=<b && p.c>=c && p.c<=d)
    {
        C.a=p.a;
        C.c=p.c;
    }
    else
    {
        C.a=a;
        C.c=c;
    }
    
    if(p.b>=a && p.b=<b && p.d>=c && p.d<=d)
    {
        C.b=p.b;
        C.d=p.d;
    }
    else
    {
        C.b=b;
        C.d=d;
    }
    return C;
}

void Prostokat::powieksz(double t)
{
    c=c*t;
    d=d*t;
}

zad. 17

class Trojmian
{
    public:
    Trojmian(double a, double b, double c): a1(a), b1(b), c1(c) {}
    double a1, b1, c1;
    Trojmian(double x1, double x2): a1(1), b1(-(x1+x2)), c1(x1*x2) {}
    int ilePierwiastkow();
    void pomnoz(double s);
    void drukuj();
};

int Trojmian:ilePierwiastkow()
{
    double delta=(b1*b1-4*a1*c1);
    if(delta<0) return 0;
    if(delta==0) return 1;
    return 2;
}

void Trojmian::pomnoz(double s)
{
    a1=a1*s;
    b1=b1*s;
    c1=c1*s;
}

void Trojkat::drukuj()
{
    cout << a1 << ", " << b1 << ", " << c1;
}

zad. 10

class Trapez
{
    public:
    Trapez(double  a): a1(a), b1(a), h1(a), kat1(90) {}
    double a1,b1,h1, kat1;
    Trapez(double  a, double b): a1(a), b1(b), h1(a), kat1(90) {}
    Trapez(double  a, double h, double kat) a1(a), b1(a-tan(kat)*2h), h1(h), kat1(kat) {}
    double pole();
    double obwod();
    bool rowne(Trapez& t);
};

double Trapez::pole()
{
    double pole=(a1+b1)*h1/2;
    return pole;
}

double Trapez::obwod()
{
    double c=sqrt(pow((a-b)/2,2)+pow(h,2));
    double obwod=a1+b1+2*c;
    return obwod;
}

bool Trapez::rowne(Trapez& t)
{
    if(t.a1==a1 && t.b1==b1 && t.h1==h1 && t.kat1==kat1) return 1;
    return 0;
}

//zad.9

class Czas
{
    
    public:
    int min;
    int h;
    Czas()
    {
        min=0;
        h=0;
    }
    Czas(int x, int y)
    {
        min=y;
        h=x;
    }
    void wypisz();
    void wypisz2(bool c);
    void dodaj(int m);
    int roznica(Czas c);
    Czas operator+=(int m);
};
// dzięki takiemu zapisowi program wie, że funkcja jest z klasy Czas
void Czas::wypisz()
{
    cout << h << "," << min << endl;
}

void Czas::wypisz2(bool c)
{
    if(c==0)
    {
        cout << h << "," << min << endl;
    }
    else if(c==1 && h<12)
    {
        cout << h << ":" << min << "AM" << endl;
    }
    else if(c==1 && h>=12)
    {
        cout << h-12 << ":" << min << "PM" << endl;
    }
}

void Czas::dodaj(int m)
{
    min=min+m;
    if(min>60)
    {
        h=h+(min/60);
        min=min%60;
    }
    if(h>23) h=h%24;
    cout << h << ":" << min << endl;
}

int Czas::roznica(Czas c)
{
    if(c.h<h) c.h+=24;
    int m1,h1;
    m1=60-min;
    if(c.min!=0)
    h++;
    h1=c.h-h;
    m1+=c.min;
    return 60*h1+m1;
}

Czas Czas::operator+=(int m)
{
    Czas p;
    p.h=h; p.min=min;
    p.min=p.min+m;
    if(p.min>60)
    {
        p.h=p.h+(p.min/60);
        p.min=p.min%60;
    }
    if(p.h>23) p.h=p.h%24;
    return p;
}

int main()
{
    Czas z(1,20);
    //z.wypisz();
    z+=50;
    z.wypisz();
}


//zad. 8

class Set
{
    int x;
    int y;
    public:
    void zdobyciePunktu(bool ktoraDruzyna);
    void drukuj();
    void okreslenie();
    Set()
    {
        x=0;
        y=0;
    }
};

void Set::zdobyciePunktu(bool ktoraDruzyna)
{
    // 0- x, 1- y
    if(ktoraDruzyna==0) x++;
    else y++;
}

void Set::drukuj()
{
    cout << x << "," << y << endl;
}

void Set::okreslenie()
{
    if(x>y) cout << x;
    else if(x==y) cout << "remis" << endl;
    else cout << y;
}

int main()
{
    Set a;
    a.drukuj();
    a.zdobyciePunktu(1);
    a.drukuj();
    a.okreslenie();
}

//zad. 11

class Obraz
{
    public:
    Obraz(double   sz, double wys): szer(sz), wyso(wys)
    {
        t=new int* [szer];
        for(int i=0;i<szer;i++)
            {
                t[i]=new int [wys];
                for(int j=0;j<wys;j++)
                t[i][j]=100;
            }
    }
    Obraz(double   sz, double wys, int jasnosc): szer(sz), wyso(wys)
    {
        t=new int* [szer];
        for(int i=0;i<szer;i++)
        {
            t[i]=new int [wys];
            for(int j=0;j<wys;j++)
            t[i][j]=jasnosc;
        }
    }
    int jasnosc(int x, int y);
    void lustro();
    void wklej(Obraz& o, int x, int y);
    Obraz wytnij(int x, int y, int sz, int wys);

    private:
    int **t;
    double szer, wyso;
};

int Obraz::jasnosc(int x, int y)
{
    return t[x][y];
}

void Obraz::lustro()
{
    for(int i=0;i<wys;i++)
        for(int j=0;j<szer/2;j++)
    {
        int pom=t[i][j];
        t[i][j]=t[i][szer-j-1];
        t[i][szer-j-1]=pom;
    }
}

void Obraz::wklej(Obraz& o, int x, int y)
{
    int szer1=0;
    if(szer>o.szer) szer1=o.szer;
    else szer1=szer;
    int wys1=0;
    if(wys>o.wys) wys1=o.wys;
    else wys1=wys;
    for(int i=x;i<szer1;i++)
    {
        for(int j=y; j<wys1;j++)
        {
            t[i][j]=o.t[i-x][j-y];
        }
    }
}

Obraz Obraz::wytnij(int x, int y, int sz, int wys)
{
    Obraz o(sz,wys);
    int szer1=0;
    if(szer>o.szer) szer1=o.szer;
    else szer1=szer;
    int wys1=0;
    if(wys>o.wys) wys1=o.wys;
    else wys1=wys;
    for(int i=x;i<szer1;i++)
    {
        for(int j=y; j<wys1;j++)
        {
            o.t[i-x][j-y]=t[i][j];
        }
    }
    return o;
}

//zad.18
struct element
{
    int indeks;
    int wartosc;
};
class Tablica
{
    void ustaw(int indeks, int wartosc);
    int wartosc(int indeks);
    int suma();
    void ustaw(int a, int b, int wartosc);
    void przesun();
    vector<element> v;
};

void Tablica::ustaw(int ind, int wart)
{
    element e;
    e.indeks=ind;
    e.wartosc=wart;
    v.push_back(e);
}

int Tablica::wartosc(int inde)
{
    for(int i=0;i<v.size();i++)
    {
        if(v[i].indeks==inde)
        return v[i].wartosc;
    }
}

int Tablica::suma()
{
    int suma=0;
    for(int i=0;i<v.size();i++)
    {
        suma+=v[i].wartosc;
    }
    return suma;
}

void Tablica::ustaw(int a, int b, int war)
{
    bool czy;
    for(int i=a;i<=b-1;i++)
    {
        czy=0;
        for(int j=0;j<v.size();j++)
        {
            if(v[i].indeks==i)
            {
                v[i].wartosc=war;
                czy=1;
            }
        }
        if(czy==0) ustaw(i,war);
    }
}

void Tablica::przesun()
{
    vector<element> p;
    bool czy;
    for(int i=0;i<v.size();i++)
    {
        czy=0;
        for(int j=0;j<p.size();j++)
        {
            if(v[i].indeks==p[j].indeks-1)
            {
                v[i].wartosc=p[j].wartosc;
                czy=1;
        }
        if(czy==0) v[i].wartosc=0;
    }
}

//zad.22
    
class Kolejka
{
    public:
    int p;
    int *t;
    int ile;
    Kolejka(int n)
    {
        t=new int [n];
        for(int i=0;i<n;i++) t[i]=0;
        p=n;
        ile=0;
    }
    void dodaj(int a);
    int usun();
    void ostatniBedaPierwszymi();
    int usunW(int a);
    void wyswietl()
    {
        for(int i=0; i<ile; i++) cout << t[i] << " ";
        cout << endl;
    }
};

void Kolejka::dodaj(int a)
{
    if(ile==p)
    {
        for(int i=0;i<p-1;i++)
        t[i]=t[i+1];
        t[p-1]=a;
    }
    else
    {
        t[ile]=a;
        ile++;
    }
}

int Kolejka::usun()
{
    int pierwsza=t[0];
    for(int i=0;i<p-1;i++)
    t[i]=t[i+1];
    ile--;
    return pierwsza;
}

void Kolejka::ostatniBedaPierwszymi()
{
    int pom;
    for(int i=0;i<ile/2;i++)
    {
        pom=t[i];
        t[i]=t[ile-i-1];
        t[ile-i-1]=pom;
    }
}

int Kolejka::usunW(int a)
{
    for(int i=0;i<ile;i++)
    {
        if(t[i]==a)
        {
            for(int j=i;j<ile-1;j++)
            t[j]=t[j+1];
            ile--;
            i--;
        }
    }
    return a;
}

int main()
{
    Kolejka a(5);
    a.wyswietl();
    a.dodaj(5);
    a.wyswietl();
    a.dodaj(3);
    a.dodaj(3);
    a.dodaj(3);
    a.dodaj(4);
    a.dodaj(4);
    a.wyswietl();
    cout << a.usun() << endl;
    a.wyswietl();
    a.ostatniBedaPierwszymi();
    a.wyswietl();
    cout << a.usunW(4) << endl;
    a.wyswietl();
}

//zad. 25
class Trasa
{
    public:
    Trasa(double wysokosc): h(wysokosc) {}
    void wedruj(double dlugosc, double wysokosc);
    int ileOdcinkow();
    private:
    vector<double> wys;
    vector<double> dl;
    double h;
}
    
void Trasa::wedruj(double dlugosc, double wysokosc)
{
    wys.push_back(wysokosc);
    dl.push_back(dlugosc);
}

double Trasa::dystans()
{
    double suma=0;
    for(int i=0;i<dl.size();i++)
    suma+=dl[i];
    return suma;
}

double Trasa::najwiekszePodejscie()
{
    int naj=wys[0]-h;
    for(int i=0;i<wys.size()-1;i++)
    {
        if(wys[i+1]-wys[i]>naj) naj=wys[i+1]-wys[i];
    }
    return naj;
}

int ileOdcinkow()
{
    int ile=dl.size();
    return ile;
}

//zad. 24

class Drogi
{
    public:
    int **t;
    int dl;
    Drogi(int n): dl(n)
    {
        t=new int*[n];
        for(int i=0;i<n;i++)
        {
            t[i]=new int [n];
            for(int j=0;j<n;j++)
            t[i][j]=0;
        }
    }
    void dodajDroge(int a, int b, int d);
    int sumaDlugosci();
    void usunDroge(int a, int b);
    void drogiZMiasta(int a);
    bool jestTrasa(int a, int b);
}

void Drogi::dodajDroge(int a, int b, int d)
{
    t[a][b]=d;
    t[b][a]=d;
}

void Drogi::usunDroge(int a, int b)
{
    t[a][b]=0;
    t[b][a]=0;
}

int Drogi::sumaDlugosci()
{
    int suma=0;
    for(int i=0;i<dl;i++)
    for(int j=0;j<i;j++)
    {
        suma+=t[i][j];
    }
    return suma;
}

void Drogi::drogiZMiasta(int a)
{
    for(int i=0;i<dl;i++)
    {
        if(t[i][a]>0) cout << t[i][a] << "," << i << endl;
    }
}
//easy
bool Drogi::jestTrasa(int a, int b)
{
    if(t[a][b]!=0) return 1;
    return 0;
}

//zad.26
class Miasto
{
    int indeks;
    double x1,y1;
    int lm;
};

class Mapa
{
    public:
    Mapa();
    void dodaj(int miasto, double x, double y, int mieszk)
    {
        Miasto m;
        m.indeks=miasto;
        m.x1=x;
        m.y1=y;
        m.im=mieszk;
        v.push_back(m);
    }
    void ustawMieszk(int miasto, int mieszk)
    {
        for(int i=0;i<v.size();i++)
        {
            if(v[i].indeks==miasto) m.lm=mieszk;
        }
    }
    int najblizsze(double x, double y);
    int mieszkancy(double x, double y, double r);
    void usun(int miasto);
    vector<Miasto> v;
};

int Mapa::najblizsze(double x, double y)
{
    Miasto m=v[0];
    double odl=0;
    odl=(x-m.x)*(x-m.x)+(y-m.y)*(y-m.y);
    int ind=v[0].indeks;
    for(int i=1;i<v.size();i++)
    {
        if((v[i].x-x)*(v[i].x-x)+(v[i].y-y)*(v[i].y-y)<odl)
        {
            ind=v[i].indeks;
            odl=(v[i].x-x)*(v[i].x-x)+(v[i].y-y)*(v[i].y-y);
        }
    }
    return ind;
}

int Mapa::mieszkancy(double x, double y, double r)
{
    int sumaM=0;
    for(int i=0;i<v.size();i++)
    {
        if((v[i].x-x)*(v[i].x-x)+(v[i].y-y)*(v[i].y-y)<=r) sumaM+=v[i].lm;
    }
    return sumaM;
}

void Mapa::usun(int miasto)
{
    int pom;
    for(int i=0;i<v.size();i++)
    {
        if(v[i].indeks==miasto) pom=i;
    }
    for(int i=pom;i<v.size()-1;i++)
    {
        v[i]=v[i+1];
    }
    v.pop_back();
}
