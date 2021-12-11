# Welcome to Mengyuan Li's Emscripten Product Series Website

## If you want to download all the code for these labs,[click here](https://github.com/MengyuanL/CS7345-Lab-Mengyuan-Li).

## Lab1 Emscripten installation and 2 programs(Hello World and algorithm)

### Ⅰ. Emscripten installation

#### Step1（Preparation work）:

Install git, CMake, Python, Visual Studio 2019 and configure environment variables. Here are some configuration screenshots if they are installed successfully.

Git:
[![1.png](https://i.postimg.cc/NfxVdBhX/1.png)](https://postimg.cc/4mmBdCx4)

Cmake and python:
[![2.png](https://i.postimg.cc/9fxwb4bk/2.png)](https://postimg.cc/McQGKph0)

System environment variables(git and CMake)
[![3.png](https://i.postimg.cc/2ySHJBNB/3.png)](https://postimg.cc/47jbHydJ)

User environment variables(python)
[![4.png](https://i.postimg.cc/pdMsvStv/4.png)](https://postimg.cc/DS5rdBZp)

#### Step2: Download Emscripten SDK

Create a new folder called “Emscripten SDK”, click the right button and then click “Git Bash here”. Enter “git clone https://github.com/emscripten-core/emsdk.git” to download the Emscripten SDK. After this, enther “cd emsdk” to enther the emsdk folder. 

[![6.png](https://i.postimg.cc/yWqZRwjY/6.png)](https://postimg.cc/T591MNBZ)

#### Step3: Installing and configuring emscripten

Enter “git pull” to fetch the latest registry of available tools. Enter “./emsdk install latest” to download and install the latest SDK tools.

[![7.png](https://i.postimg.cc/Fstp3q7L/7.png)](https://postimg.cc/MXD18906)

#### Step4: Activate the sdk

Enter “./emsdk activate latest” to make the "latest" SDK "active" for the current user. Enter “source ./emsdk_env.sh” to activate path and other environment variables in the current terminal. Finally enter “emcc -v” to verify whether emscripten has been installed successfully.

[![8.png](https://i.postimg.cc/VkJNw7WK/8.png)](https://postimg.cc/hXqnb1wm)
[![9.png](https://i.postimg.cc/Jn5rxSRz/9.png)](https://postimg.cc/ZB0zK79G)

### Ⅱ. Test programs

#### Hello World 

Create a “HelloWorld”.cpp:

```c++
#include <iostream>
  
using namespace std;
  
int main()
  
{
  
    cout << "Hello World!\n";
  
}
```

Enter emcc.bat HelloWorld.cpp to generate a.out.js and a.out.wasm. 
  
Enter emcc.bat HelloWorld.cpp -o helloworld.js to generate helloworld.js and helloworld.wasm. 
 
Enter emcc.bat HelloWorld.cpp -o helloworld.html to generate helloworld.html.
  
[![10.png](https://i.postimg.cc/cHCW7CkX/10.png)](https://postimg.cc/Z9GX4bSd)
 
Two ways of running the code:
  
1️⃣ Node.js
  
Use the following command to test the compiled code: node a.out.js
  
[![11.png](https://i.postimg.cc/L5BhwnRL/11.png)](https://postimg.cc/SYRyzQnx)
  
2️⃣ Browser
  
For the helloworld.html, first enter emrun --no_browser --port 8080 D:\Emscripten SDK\emsdk\helloworld\helloworld.html to start HTTP service.Then start browser and enter in the address bar: http://localhost:8080/helloworld.html.
  
[![16.png](https://i.postimg.cc/sXTNcJGh/16.png)](https://postimg.cc/62Gc6n0W)
[![12.png](https://i.postimg.cc/WzKfRbnp/12.png)](https://postimg.cc/Zv8Lpm2X)
  
A few important things to remember:
  
① Every time you start the git terminal, you need to git bash on the emsdk folder. Otherwise the command won’t work.
  
② Evert time after you start the git terminal, you need to enter “source ./emsdk_env.sh” to activate path and other environment variables in the current terminal. 
  
③ I create a helloworld folder on the emsdk folder in order to manage those transcompiled files so I first git bash on the emsdk folder and then enter “source ./emsdk_env.sh” to activate path and other environment variables in the current terminal. After that, I enter “cd helloworld” to go to the helloworld folder and then enter those transcompiling command.
  
#### Algorithm(given a string s and return the longest palindromic substring in s)
  
```c++
#include <iostream>
#include <string>
#include <vector>
#include<iomanip>
#include<ctime>
using namespace std;
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        if (n < 2) {        
            return s; 
        }    
        int maxLen = 1;     
        int begin = 0;      
        vector<vector<int>> dp(n, vector<int>(n));
        for (int i = 0; i < n; i++) {                  
            dp[i][i] = true;         
        }                 
        for (int L = 2; L <= n; L++) {
            for (int i = 0; i < n; i++) {             
                int j = L + i - 1;         
                if (j >= n) {
                    break;
                }
                if (s[i] != s[j]) {
                    dp[i][j] = false;
                }
                else {
                    if (j - i < 3) {          
                        dp[i][j] = true;   
                    }         
                    else {                                  
                        dp[i][j] = dp[i + 1][j - 1];                              
                    }                              
                }                                 
                if (dp[i][j] && j - i + 1 > maxLen) {
                    maxLen = j - i + 1;
                    begin = i;
                }
            }
        }
        return s.substr(begin, maxLen);
    }
};
  
int main() {
    Solution solution;
    string test =
  "acbdefsdgasdgasdgsdgsddcgsadfvsdgbsfdgsadgdfhadfgsdayhgafasdfasgsdgasdjkhfgvsadhuvbsaduiafgshdgbsajdbvsadjkgbsdjkgbasdkjgasdsdagasdfhafdhashgbadfhnadfvsadfgasdgasdhsah";
    string answer = "";
    clock_t startTime, endTime;
    startTime = clock();
    answer = solution.longestPalindrome(test);
    endTime = clock();
    cout << answer << " The execution time is: " << (double)(endTime - startTime) / CLOCKS_PER_SEC << "s";
}
```

##### Result and Analysis

[![13.png](https://i.postimg.cc/qMrdv1Xk/13.png)](https://postimg.cc/7bKRBMWc)
[![14.png](https://i.postimg.cc/4xLCwsCd/14.png)](https://postimg.cc/xXzF1r1D)

Analysis:

  For web results, the 95% confidence interval is [0.004644268,0.012355732]. And the possibility of data are not in this interval is 2/30(0.013 and 0.014) which is nearly 6.67%. This means that the possibility of data are in this interval is 93.33%. So this possibility is less than 95% which means that the results are not statistically significant.
  
  For native results, the 95% confidence interval is [0.002242515,0.004290819]. And the possibility of data are not in this interval is 1/30(0.005) which is nearly 3.33%. This means that the possibility of data are in this interval is 96.67%. So this possibility is more than 95% which means that are statistically significant.
Besides, the average execution time of web code(0.0085s) is much slower than that of native code(0.003266667s). 
Above all, native code is more reliable and runs faster than the transcompiled web code.

## Lab2 Advanced Application

### UML for the native code

[![Lab2.jpg](https://i.postimg.cc/5t8JfrZz/Lab2.jpg)](https://postimg.cc/CZMXNcMM)

#### Ticket Code

``` c++
#pragma once
class Ticket {
private:
	int num;
	double price;
	int FlightNumber;
public:
	Ticket(int n, double p, int FlightNumber);
	int getNum();
	double getPrice();
	int getFlightNumber();
	void reservation();
};

#include"Ticket.h"
Ticket::Ticket(int n,double p,int fn) {
	num = n;
	price = p;
	FlightNumber = fn;
}

int Ticket::getNum() {
	return num;
}

double Ticket::getPrice() {
	return price;
}

int Ticket::getFlightNumber() {
	return FlightNumber;
}

void Ticket::reservation() {
	num--;
}
```

#### ReservationSystem code

```c++
#pragma once
class ReservationSystem{
    private:
    int total;
    public:
    ReservationSystem(int t);
};

#include"ReservationSystem.h"
ReservationSystem::ReservationSystem(int t){
    total=t;
}
```

#### Main Program

```c++
#include"Ticket.cpp"
#include"ReservationSystem.cpp"
#include<iostream>
#include<ctime>
using namespace std;
int main(){
    Ticket tickets[10]={Ticket(1000, 77.7, 7360),Ticket(800, 99.9, 8362),Ticket(600, 33.3, 4571),Ticket(500, 42.7, 1651),Ticket(900, 88.6, 1546),Ticket(300, 252.6, 6841),Ticket(777, 180.0, 4862),Ticket(700, 155.0, 9742),Ticket(888, 92.0, 5200),Ticket(200, 46.5, 6349)};
	cout << "      Flight Information Board\n" << endl;
	cout << "Flight Number    Tickets       Price" << endl;
	clock_t start,end;
	start=clock();
	for (int i = 0; i < 10; i++) {
		cout <<"     " <<tickets[i].getFlightNumber()<<"         "<< tickets[i].getNum()<<"          "<< tickets[i].getPrice()<<endl;
	}
	end=clock();
	cout<<"The execution time of showing information is: "<<(double)(end-start)/CLOCKS_PER_SEC<<"s";
    double sale[10]={0.0};
	int diff[10];
	start=clock();
	for (int i = 0; i < 10; i++) {
		int count=0;
		for(int j=0;j<tickets[i].getNum()/2;j++){
			tickets[i].reservation();
			count++;
		}
		diff[i]=count;
	}
	for(int i=0;i<10;i++){
		sale[i]=tickets[i].getPrice()*diff[i];
	}
	cout << "\nInformation updated after reservation" << endl;
	cout << "\nFlight Number    Tickets       Price      Sales volume" << endl;
	for (int i = 0; i < 10; i++) {
		cout << "     " << tickets[i].getFlightNumber() << "         " << tickets[i].getNum() << "          " << tickets[i].getPrice()<<"          "<<sale[i] << endl;
	}
	end=clock();
	cout<<"The execution time of showing information after reservation is: "<<(double)(end-start)/CLOCKS_PER_SEC<<"s";
	return 0;
}
```

### Explaination

For the Ticket class, it represents all the tickets of one specific flight so it should contains the specific flight number, number of remaining tickets and price. Besides, it should contains the corresponding “get mehtod” which are getNum(), getPrice() and getFlightNumber(). Also, it should contain a reservation() method for passenger to book tickets: after a ticket is booked, then the num of object of Ticket with specific flight number would minus 1. 

For the ReservationSystem class, it represents the reservation system and it contains a constructor to initialize the number of flights in the system.

### Result

Native:

[![1.jpg](https://i.postimg.cc/yNJGSdjF/1.jpg)](https://postimg.cc/mcsjvT0D)

Web:

[![2.jpg](https://i.postimg.cc/k4kr1S1M/2.jpg)](https://postimg.cc/zbSP3yY4)

### Comparison

For native main.cpp, I use the Coder Runner plug-in to run the code. 

For index.html, I use the live server and Microsoft Edge to run the code.

Native results

[![Lab2.jpg](https://i.postimg.cc/mgbpP5zM/Lab2.jpg)](https://postimg.cc/4mSQMw1N)

Web results

[![Lab2-1.jpg](https://i.postimg.cc/fbVKXnw3/Lab2-1.jpg)](https://postimg.cc/HJCXDN8H)

#### Comparison before reservation

For native results, the 95% confidence interval is [5.910678068,15.889321932]. And the possibility of data are not in this interval is 1/30(23) which is nearly 3.33%. This means that the possibility of data are in this interval is 96.67%. So this possibility is more than 95% which means that the results are statistically significant.

For web results, the 95% confidence interval is [1.289092805,2.257573861]. And the possibility of data are not in this interval is 1/30(2.8) which is nearly 3.33%. This means that the possibility of data are in this interval is 96.67%. So this possibility is more than 95% which means that are not statistically significant.

#### Comparison after reservation

For native results, the 95% confidence interval is [5.910678068,15.889321932]. And the possibility of data are not in this interval is 1/30(23) which is nearly 3.33%. This means that the possibility of data are in this interval is 96.67%. So this possibility is more than 95% which means that the results are statistically significant.

For web results, the 95% confidence interval is [1.289092805,2.257573861]. And the possibility of data are not in this interval is 1/30(2.8) which is nearly 3.33%. This means that the possibility of data are in this interval is 96.67%. So this possibility is more than 95% which means that are not statistically significant.

Besides, the average execution time of web code(1.773333333ms) is much faster than that of native code(10.9ms). And the standard deviation of web code(0.242120264) is much smaller than that of native code(2.494660966), which means that the result of web code is more concrete and stable than that of native code.

#### Conclusion

Above all, web code that utilizes the compiled js library is more faster and stable than the native C++ code that uses the native C++ library.

## Lab3 Multithread Program

### UML 

[![3.jpg](https://i.postimg.cc/cLwKJzM4/3.jpg)](https://postimg.cc/5X997nRZ)

#### Ticket 

```c++
#pragma once
class Ticket {
    friend class ReservationThread;
    friend class System;
private:
	int num;
	double price;
	int FlightNumber;
public:
	Ticket(int n, double p, int fn);
	int getNum();
	double getPrice();
	int getFlightNumber();
	void reservation();
};

#include"Ticket.hpp"
#include<iostream>
using namespace std;
Ticket::Ticket(int n,double p,int fn) {
	num = n;
	price = p;
	FlightNumber = fn;
}

int Ticket::getNum() {
	return num;
}

double Ticket::getPrice() {
	return price;
}

int Ticket::getFlightNumber() {
	return FlightNumber;
}

void Ticket::reservation() {
	num--;
	cout<<"One ticket of the Flight "<<FlightNumber<<" has been sold"<<endl;
}
```

#### ReservationThread

```c++
#pragma once
#include<mutex>
#include<map>
#include<deque>
#include<thread>
#include"Ticket.hpp"
using namespace std;
class ReservationThread{
    friend class ReservationSystem;
    public:
    ReservationThread(int num,int flightNumber,Ticket* ticket);
    void Startup();
    void Work();
    static void ReservationThreadMain(void* ReservationThreadObject);

    private:
    int                   ticket_num=0;
    int                   ticket_flightNumber=0;
    Ticket*               ticket_ticket=nullptr;
    thread*               ticket_thread=nullptr;
    mutable mutex         ticket_ReservationStatusMutex;
};

#include<mutex>
#include<map>
#include<deque>
#include<vector>
#include<thread>
#include<iostream>
#include"ReservationThread.hpp"
#include"ReservationSystem.hpp"
using namespace std;
ReservationThread::ReservationThread(int num,int flightNumber,Ticket* ticket){
    ticket_num=num;
    ticket_flightNumber=flightNumber;
    ticket_ticket=ticket;
}

void ReservationThread::Startup(){
    ticket_thread=new thread(ReservationThreadMain,this);
}

void ReservationThread::Work(){
    int num=ticket_ticket->getNum();
    while(num>50){
        ticket_ReservationStatusMutex.lock();
        ticket_ticket->reservation();
        num--;
        ticket_ReservationStatusMutex.unlock();
    }
}

void ReservationThread::ReservationThreadMain(void* ReservationThreadObject){
    ReservationThread* thisReservation=(ReservationThread*)ReservationThreadObject;
    thisReservation->Work();
}
```

#### ReservationSystem

```c++
#pragma once
#include<mutex>
#include<map>
#include<deque>
#include<thread>
#include<vector>
using namespace std;
class ReservationThread;
class Ticket;
class ReservationSystem{
    friend class ReservationThread;
    public:
    ReservationSystem();
    static ReservationSystem* CreateOrGet();
    void CreateReservationThread(int num,int FlightNumber,Ticket* ticket);

    static ReservationSystem*    ticket_ReservationSystem;
    vector<ReservationThread*>   ticket_ReservationThreads;
    mutable mutex                ticket_ReservationThreadsMutex;
    vector<Ticket*>              ticket_Tickets;
    mutex                        ticket_ReservastionMutex;
};

#include<iostream>
#include<vector>
#include<cstring>
#include"ReservationSystem.hpp"
#include"ReservationThread.hpp"
ReservationSystem* ReservationSystem::ticket_ReservationSystem=nullptr;

ReservationSystem::ReservationSystem(){
}

ReservationSystem* ReservationSystem::CreateOrGet(){
    if(!ticket_ReservationSystem){
        ticket_ReservationSystem=new ReservationSystem();
    }
    return ticket_ReservationSystem;
}

void ReservationSystem::CreateReservationThread(int num,int FlightNumber,Ticket* ticket){
        ReservationThread* newReservation=new ReservationThread(num,FlightNumber,ticket);
        ticket_ReservationThreadsMutex.lock();
        ticket_ReservationThreads.push_back(newReservation);
        newReservation->Startup();
        ticket_ReservationThreadsMutex.unlock();
}
```

#### Main Program

```c++
#include<iostream>
#include<string>
#include<vector>
#include"ReservationSystem.hpp"
#include"ReservationThread.hpp"
#include<ctime>
#include<chrono>
using namespace std;
int main(void){
    clock_t start,end;
    cout<<"Creating Reservation System"<<endl;
    ReservationSystem* rs=ReservationSystem::CreateOrGet();
    cout<<"Create Tickets"<<endl;
    Ticket t1=Ticket(300,122.5,7220);
    Ticket t2=Ticket(160,242.8,6245);
    Ticket t3=Ticket(150,322.5,9132);
    Ticket t4=Ticket(100,62.6,3220);
    Ticket t5=Ticket(250,420.0,3637);
    Ticket t6=Ticket(280,334.6,2108);
    Ticket t7=Ticket(220,122.5,7220);
    Ticket t8=Ticket(240,122.5,7220);
    vector<Ticket*> tickets;
    tickets.push_back(&t1);
    tickets.push_back(&t2);
    tickets.push_back(&t3);
    tickets.push_back(&t4);
    tickets.push_back(&t5);
    tickets.push_back(&t6);
    tickets.push_back(&t7);
    tickets.push_back(&t8);
    tickets.push_back(&t8);
    cout<<"Creating Reservation Threads"<<endl;
    rs->CreateReservationThread(300,7220,tickets[0]);
    rs->CreateReservationThread(160,6245,tickets[1]);
    rs->CreateReservationThread(200,4231,tickets[2]);
    rs->CreateReservationThread(150,9132,tickets[3]);
    rs->CreateReservationThread(100,3220,tickets[4]);
    rs->CreateReservationThread(250,3637,tickets[5]);
    rs->CreateReservationThread(280,2108,tickets[6]);
    rs->CreateReservationThread(220,9267,tickets[7]);
    start=clock();
    rs->ticket_ReservationThreads[0]->Work();
    rs->ticket_ReservationThreads[1]->Work();
    rs->ticket_ReservationThreads[2]->Work();
    rs->ticket_ReservationThreads[3]->Work();
    rs->ticket_ReservationThreads[4]->Work();
    rs->ticket_ReservationThreads[5]->Work();
    rs->ticket_ReservationThreads[6]->Work();
    rs->ticket_ReservationThreads[7]->Work();
    end=clock();
    cout<<"The execution time of reservation with multithread is "<<(double)(end-start)/CLOCKS_PER_SEC<<"s"<<endl;
    int running = 1;

#ifdef __EMSCRIPTEN__
    this_thread::sleep_for(chrono::microseconds(5 * 1000000));
    cout << "Finishing Tickets Reservation" << endl;
    cout<<"The execution time of reservation with multithread is "<<(double)(end-start)/CLOCKS_PER_SEC<<"s"<<endl;
#else
    while (running)
    {
        std::string command;
        std::cout << "Enter stop, finish ";
        std::cin >> command;

        if (command == "stop")
        {
            running = 0;
        }
        else if (command == "finish")
        {
            cout << "Total Tickets Reserved: " << rs->ticket_Tickets.size()<< std::endl;
        }
        else
        {
            std::cout << "Unknown Command" << std::endl;
        }
    }
    #endif
}
```

#### Important note:
To run the code you need to first put all the files and folders in the code folder to the folder ” emsdk\upstream\bin”.

For native main.cpp, I use the make file and enter make in the terminal of vscode to run the code.

For web, I use node.js to run the code. First git bash and activate the emsdk using “source ./emsdk_env.sh”. Then enter “emcc -std=c++14 -pthread -s PROXY_TO_PTHREAD -s ALLOW_MEMORY_GROWTH=1 -s NO_DISABLE_EXCEPTION_CATCHING -s LLD_REPORT_UNDEFINED -s ERROR_ON_UNDEFINED_SYMBOLS=1 Ticket.cpp ReservationThread.cpp ReservationSystem.cpp -o main.html” to compile the native C++ code to web code. Finally, enter “node --experimental-wasm-threads main.js” in the git terminal to run the code.

#### Result

Native 

[![4.jpg](https://i.postimg.cc/xjP7Hj5W/4.jpg)](https://postimg.cc/14fJ1QLH)

Web

[![5.jpg](https://i.postimg.cc/m22nSx6h/5.jpg)](https://postimg.cc/mhJVbn4G)

#### Comparison

For native results, the 95% confidence interval is [0.85364015,0.89175985]. And the possibility of data are not in this interval is 21/30 which is nearly 76.67%. This means that the possibility of data are in this interval is 23.33%. So this possibility is less than 95% which means that the results are not statistically significant.

For web results, the 95% confidence interval is [0.41908404,0.460782626]. And the possibility of data are not in this interval is 23/30 which is nearly 6.67%. This means that the possibility of data are in this interval is 93.33%. So this possibility is less than 95% which means that are not statistically significant.

Besides, the average execution time of web code(0.439933333s) is much faster than that of native code(0.8727s). And the standard deviation of web code(0.055835433) is bigger than that of native code(0.051043217), which means that the result of web code is less concrete and stable than that of native code. 

#### Conclusion

Above all, web code that utilizes the compiled multithread is more faster and less stable than the native C++ code that uses the compiled multithread.















































