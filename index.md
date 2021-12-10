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




  


  


  



  

















