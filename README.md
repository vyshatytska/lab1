Лабораторна 2-3
# lab1
1.	Написати програму, що реалізує пошук НСД методом 1 і 2, а також методом Евкліда для двох чисел. Числа вибирати восьми- або дев’ятицифровими.
Визначити середній час виконання алгоритмів шляхом автоматичного запуску алгоритмів по 10-20 раз.

1 спосіб

#include <iostream>
#include<ctime>

using namespace std;

int main()
{
    int t = time(NULL);

    srand(time(NULL));
    long int a = rand() % 9 + 1;
    long int b = rand() % 9 + 1;
    bool res = false;

    for (int j = 0; j < 10; j++)
    {
        cout << "\n";
        a = rand() % 9 + 1;
        b = rand() % 9 + 1;
        bool res = false;

        for (int k = 0; k < 8; k++)
        {
            a = a * 10 + rand() % 10;
            b = b * 10 + rand() % 10;

            if (a == b)
            {
                cout << "a=" << a << "b=" << b << "NDs=" << a << "\n";
                bool res = true;
            }
            else if (a % b == 0)
            {
                cout << "a=" << a << "b=" << b << "NDs=" << b << "\n";
                bool res = true;
            }
            for (long i = a; i > 0; i--)
            {
                if (res)
                {
                    continue;
                }
                if (a % i == 0 && b % i == 0)
                {
                    cout << "a=" << a << "b=" << b << "NDs=" << i << "\n";
                    bool res = true;
                    break;
                }
            }



        }
    }
    cout << "\n time=" << (time(NULL) - t);
}
2 спосіб
#include <iostream>
#include<ctime>

using namespace std;

int main()
{
    int t = time(NULL);
    srand(time(NULL));
    long int a = rand() % 14 + 1; // збільшено з 9 до 14 
    long int b = rand() % 14 + 1; ; // збільшено з 9 до 14 
    for (int j = 0; j < 15; j++); // збільшено з 10 до 15 
    {
        a = rand() % 14 + 1; // збільшено з 9 до 14 
        b = rand() % 14 + 1; // збільшено з 9 до 14 
        bool res = false;
        for (int k = 0; k < 13; k++) // збільшено з 8 до 13 
        {
            cout << "\n";
            a = a * 15 + rand() % 15; // збільшено з 10 до 15 
            b = b * 15 + rand() % 15; // збільшено з 10 до 15 
            res = false;
            if (a == b)
            {
                cout << "a=" << a << "b=" << b << " NDs=" << a;
                res = true;
            }
            else if (a % b == 0)
            {
                cout << "a=" << a << "b=" << b << " NDs=" << b;
                res = true;
            }
            for (long i = a; i > 0; i--)
            {
                if (res) continue;
                if (a % i == 0 && b % i == 0)
                {
                    cout << "a=" << a << "b=" << b << " NDs=" << i;
                    res = true;
                    break;
                }
            }

        }
    }
    cout << "\n time=" << (time(NULL) - t);
}
Алгоритм Евкліда
#include <iostream>
#include<ctime>
#include<algorithm>

using namespace std;

int gcd(int a, int b) {
    if (b == 0) return a;
    else return gcd(b, a % b);
}

int main() {
    int t = time(NULL);
    srand(time(NULL));

    int a, b;
    cin >> a >> b;
    cout << gcd(a, b);
    return 0;

    cout << "\n time=" << (time(NULL) - t);

}
2.	Написати програму, яка реалізує алгоритм Дейкстри. Відкомпілювати та відлагодити програму. Протестувати роботу програми використовуючи різні вхідні дані:
 
За початкову точку вибрати вершину 3.
#include<iostream>


using namespace std;

const int points = 6;
int main()
{
	int graph[points][points] = {
		{0, 10, 3, 3, 7, 1},
		{10, 0, 13, 8, 13, 11},
		{3, 13, 0, 6, 5, 4},
		{3, 8, 6, 0, 5, 2},
		{7, 13, 5, 5, 0, 6},
		{1, 11, 4, 2, 6, 0}
	};

	int st; //старт

	cout << "start point =";
	cin >> st;

	st = st - 1;

	int dis[points]; //для визн. відстані
	bool visit[points]; //для позн. відвіданих
	int index; //індекс мін. відстані

	//ініціалізація
	for (int i = 0; i < points; i++) {
		dis[i] = 65535;
		visit[i] = false;
	}
	dis[st] = 0;

	for (int j = 0; j < points - 1; j++)
	{
		int min = 65535;
		for (int i = 0; i < points; i++) {

			if (!visit[i] && dis[i] <= min) {
				min = dis[i];
				index = i;
			}

		}
	
	visit[index] = true;

	for (int i = 0; i < points; i++) 
	  {
		if (!visit[i] && dis[index] + graph[index][i] < dis[i] && dis[index] != 65535 && graph[index][i]) 
		{
			dis[i] = dis[index] + graph[index][i];
		}
	  }
    }
	
	cout << " from point " << st + 1 << "to other points are \n";
	for (int i = 0; i < points; i++) 
	{
		cout << st + 1 << " --> " << i + 1 << " d= " << dis[i] << " \n";
	}
}

Лабораторна 4

#include <iostream>
#include <cstdlib>
#include <ctime>

template<typename T>
void Initialize(T arr[], int size);

template<typename T>
void Show(const T arr[], int size);

template<typename T>
void QuickSort(T arr[], int first, int last);

int main()
{
    srand(static_cast<unsigned>(time(nullptr)));

    const int SIZE1 = 10, SIZE2 = 20;
    int arr1[SIZE1];
    long arr2[SIZE2];

    Initialize(arr1, SIZE1);
    Initialize(arr2, SIZE2);

    std::cout << "arr1 before sorting: ";
    Show(arr1, SIZE1);
    std::cout << "arr2 before sorting: ";
    Show(arr2, SIZE2);

    QuickSort(arr1, 0, SIZE1 - 1);
    QuickSort(arr2, 0, SIZE2 - 1);

    std::cout << "arr1 after sorting: ";
    Show(arr1, SIZE1);
    std::cout << "arr2 after sorting: ";
    Show(arr2, SIZE2);

    return 0;
}

template<typename T>
void Initialize(T arr[], int size)
{
    for (int i = 0; i < size; i++)
        arr[i] = rand() % 100;
}

template<typename T>
void Show(const T arr[], int size)
{
    for (int i = 0; i < size; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;
}

template<typename T>
void QuickSort(T arr[], int first, int last)
{
    T middle = arr[(first + last) / 2];
    int i = first;
    int j = last;

    do
    {
        while (arr[i] < middle)
            i++;
        while (arr[j] > middle)
            j--;

        if (i <= j)
        {
            std::swap(arr[i], arr[j]);
            i++;
            j--;
        }

    } while (i <= j);

    if (i < last)
        QuickSort(arr, i, last);
    if (j > first)
        QuickSort(arr, first, j);
}

Лабораторна 5


Завдання 1
 
  
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    double a;
    double b;
    double c;
    cout << "A ="; cin >> a;
    cout << "B ="; cin >> b;

    c = sqrt(a * a + b * b);
    cin.get();
    cout << "C = " << c << endl;
}

 
Завдання 2
 
 
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    double a;
    double n;
    double i;
    int c;
    cout << "N ="; cin >> n;

    a = (n/2)+(n/3)+(n/5)+(n/30)-(n/6)-(n/10)-(n/15);
    cin.get();
    c = n - a;
    cout << "C = " << c << endl;

}

 
Завдання 3
  
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    double a;
    double b;
    double c, d, e, k, m, n;

    cout << "A ="; cin >> a;
    cout << "B ="; cin >> b;
    cout << "C ="; cin >> c;
    cout << "D ="; cin >> d;

    e = c - a;
    m= d - b;
    n = (e);
    k = (e, " ", m);
    cout << "N = " << n  << "  " << k << endl;
   
}
 
Завдання 4
 
 
#include <iostream>
#include <cmath>
#include <stdio.h>
using namespace std;

int Suma(int n) {
	int s = 0;
	while (n != 0) {
		s += n % 10;
		n /= 10;
	}
	return s;
}
int main() {
	int N, s;
	printf("N: ");
	scanf_s("%d", &N);

	s = Suma(N);
	printf("Suma: %d", s);
	return 0;
}

 
Завдання 5
 
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int n;
    cout << "N ="; cin >> n;
    cout << "The next number for the number " << n << " is " << n + 1 << endl;
    cout << "The previous number for the number "<< n << " is " << n - 1 << "." << endl;
    
}

 

Завдання 6
 
 
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int n,v;
    {cout << "V ="; cin >> v;
    n = v / 3;
    cout << "N = " << n << endl;
    }
}
