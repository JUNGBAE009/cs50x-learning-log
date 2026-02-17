# 1. Arrays란 무엇인가?
배열(Array)은 
같은 자료형(type)의 값들을 연속된 메모리 공간에 저장하는 자료 구조 입니다.

ex: 
```
int scores[3];
```
의미 : 정수형(int), 3개의 공간, 연속된 메모리 주소에 저장 

## 왜 배열(Array)이 필요한가?
배열이 없으면 
```
int s1, s2, s3;
```
값이 100개 = 변수 100개 -> 비효율적
배열을 쓰면
```
int scores[100]; 
```
간단하고 깔끔하게 코드 작성 가능

# 2. 메모리 관점에서 이해하기

```
int scores[3] = {72, 85, 90};
```
## 가상의 예시 주소 
int = 4바이트
<br>
시작 주소 = 0x1000

| 메모리주소  | 오프셋(offset)  | 저장 값  | 배열 인덱스  | 설명  |
|---|---|---|---|---|
| 0x1000  | +0 byte  | 72  | scores[0]  | 첫 번째  |
| 0x1004  | +4 bytes  | 85  | scores[1]  | 두 번째  |
| 0x1008  | +8 bytes  | 90  | scores[2]  | 세 번째  |

## ⚠️배열 범위 초과 시 메모리 위험
scores[3] : 0x100C 접근 시도
내 배열에 속하지 않은 메모리에 접근하는 것은 위험합니다.

C 언어는 배열 경계 검사를 자동으로 수행하지 않기 때문에,
범위를 벗어난 접근은 Undefined Behavior를 유발합니다.

# 3. 배열을 다루는 기본 패턴 (반복문)

배열은 대부분 for문으로 다룹니다.
```
for (int i = 0; i < 3; i++)
{
    printf("%i\n", scores[i]);
}
```
간단 해석 :
i를 0부터 시작해서 3보다 작을 동안 반복하고 
매번 i를 1씩 증가시키면서
scores[i] 를 출력 

## 합계/평균 

### 합계
```
int sum = 0;

for (int i = 0; i < 3; i++)
{
    sum += scores[i];
}
```
### 평균 (나눗셈과 float)
```
float avg = (float) sum / 3;
```

왜 float가 필요한가?
sum과 3이 둘 다 정수면 정수 나눗셈이 되어 소수점이 잘림
따라서 float가 필요 

## 배열 길이는 어떻게 관리하는 가?
보통 길이를 변수로 관리
```
int length = 3;

for (int i = 0; i < length; i++)
{
    ...
}
```

## 배열을 함수에 넘기면 주소만 넘어간다
```
float average(int length, int array[])
{
    int sum = 0;
    for (int i = 0; i < length; i++)
    {
        sum += array[i];
    }
    return (float) sum / length;
}
```
##  호출
```
float result = average(3, scores);
```

핵심 : 배열을 함수에 넘길 때 배열 전체가 복사되지 않음 
시작 주소(첫 칸 위치)만 전달 
그래서 lenght를 꼭 같이 넘겨야 한다.

# 4. 문자열(string)은 사실 문자 배열 이다 
ex: 
```
char name[] = "text";
```

| 인덱스  | 값  |
|---|---|
| 0  | 't'  |
| 1  | 'e'  |
| 2  | 'x'  |
| 3  | 't'  |
| 4  | '\0' |

#### \0 은 문자열의 끝을 표시






