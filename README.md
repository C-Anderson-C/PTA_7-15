# PTA_7-15
# 计算圆周率
# 根据下面关系式，求圆周率的值，直到最后一项的值小于给定阈值。pi/2=1+(1/3)+(2！/3*5)+(3！/3*5*7)+...+(n!/3*5*7*...*(2n+!))

# 输入格式：输入在一行中给出小于1的阈值。

# 输出格式：在一行中输出满足阈值条件的近似圆周率，输出到小数点后6位。
```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    double eps;
    cin >> eps;

    // 第一项 n=0 为 1
    double halfPi = 1.0;
    double term = 1.0; // 当前项的值
    int n = 1; // 从第一项（即 n=1）开始计算后续项

    while (term >= eps) {
        // 计算分子 n!
        double numerator = 1.0;
        for (int i = 1; i <= n; ++i) {
            numerator *= i;
        }

        // 计算分母 3 × 5 × 7 × ... × (2*n + 1)
        double denominator = 1.0;
        for (int i = 1; i <= n; ++i) {
            denominator *= (2 * i + 1);
        }

        // 计算当前项的值
        term = numerator / denominator;
        
        // 所有项均为正值，直接累加
        halfPi += term;

        ++n; // 进入下一项
    }

    // 根据公式，圆周率 = 2×(π/2)
    double pi = halfPi * 2;

    // 输出结果，保留小数点后6位
    cout << fixed << setprecision(6) << pi << endl;

    return 0;
}
