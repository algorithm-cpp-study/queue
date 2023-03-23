**큐의 성질**

-   원소의 추가가 O(1)
-   원소의 제거가 O(1)
-   제일 앞/뒤의 원소 확인이 O(1)
-   제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능

**큐의 구현**

```
#include <bits/stdc++.h>
using namespace std;

const int MX = 1000005;
int dat[MX];
int head = 0, tail = 0;

void push(int x){
    dat[tail++] = x;
}

void pop(){
    head++;
}

int front(){
    return dat[head];
}

int back(){
    return dat[tail - 1];
}

void test(){
    push(10); push(20); push(30);
    cout << front() << '\n'; // 10
    cout << back() << '\n'; // 30
    pop(); pop();
    push(15); push(25);
    cout << front() << '\n'; // 30
    cout << back() << '\n'; // 25
}

int main(void) {
    test();
}
```

**STL 큐 활용**

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0);

    queue<int> Q;
    Q.push(10);                  //10
    Q.push(20);                     //10 20
    Q.push(30);                     //10 20 30
    cout << Q.size() << '\n';       //3
    if(Q.empty()) cout << "Q is empty\n";
    else cout << "Q is not empty\n";            //Q is not empty
    Q.pop();                    //20 30
    cout << Q.front() << '\n';              //20
    cout << Q.back() << '\n';               //30
    Q.push(40);                        //20 30 40
    Q.pop();                            //30 40
    cout << Q.front() << '\n';          //30
}
```