# 큐 - queue
큐는 한쪽 끝에서 원소를 넣고 반대쪽 끝에서 원소를 뺄 수 있는 자료구조입니다.  
큐에서는 먼저 들어간 원소가 먼저 나오게 됩니다. (FIFO = First In First Out)  
공항에서 입국수속을 하는 줄과 같은 상황.  
  
## 큐의 성질
1. 원소의 추가가 O(1)  
2. 원소의 제거가 O(1)  
3. 제일 앞/뒤의 원소 확인이 O(1)  
4. 제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능  
  
큐에서는 추가되는 곳을 rear, 즉 뒤쪽이라고 하고 제거되는 쪽을 front, 즉 앞쪽이라고 합니다.  
  
## 큐의 구현
head = 가장 앞에 있는 원소의 인덱스  
tail = 가장 뒤에 있는 원소의 인덱스 + 1  
dat[head]부터 dat[tail-1]번지까지가 큐의 원소들이 들어있는 자리. 큐의 크기는 tail - head로 계산 가능  
push 할때 tail이 증가하고, pop할 때 head가 증가한다. 원소들이 점점 오른쪽으로 밀린다.  
  
앞쪽에 사용하지 않고 있는 공간이 많음에도 불구하고 더 이상 삽입을 할 수 없다.  
이 문제를 해결하는 방법은 큐의 원소가 들어갈 배열을 원형으로 만드는 것.  
관념적으로는 배열이 원형인거고, 실제 구현을 할 땐 head나 tail이 7인 상태에서 1이 더해질 때 0번지로 다시 오도록 만들면 된다.  
  
코딩 테스트에서는 어차피 push의 최대 횟수가 정해져있다.  
배열의 크기를 push의 최대 횟수보다 크게 둬서 굳이 원형 큐를 만들지 않아도 되게끔 할 수 있다.  
```c++
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
    return dat[tail-1];
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
## STL queue
```c++
#include <bits/stdc++.h>

using namespace std;
#define X first
#define Y second
typedef pair<int, int> pii;

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    queue<int> q;
    q.push(10);
    q.push(20);
    q.push(30);
    cout << q.size() << '\n';
    if (q.empty()) cout << "Q is empty\n";
    else cout << "Q is not empty\n";
    q.pop(); // 20 30
    cout << q.front() << '\n';
    cout << q.back() << '\n';
    q.push(40); // 20 30 40
    q.pop(); // 30 40
    cout << q.front() << '\n';
}
```
큐가 비어있는데 front나 back이나 pop을 호출하면 런타임에러가 발생할 수 있습니다.  
