# 작업 스케쥴링(Job Scheduling)

## 1. 작업 스케쥴링이란?

### 작업 스케쥴링(Job Scheduling) 문제는 n개의 작업, 각 작업의 수행 시간 ti, i=1,2,3, ... ,n, 그리고 m개의 동일한 기계가 주어질 때, 모든 작업이 가장 빨리 종료되도록 작업을 기계에 배정하는 문제이다. 단, 한 작업은 배정된 기계에서 연속적으로 수행되어야 한다. 또한 기계는 1번에 하나의 작업만을 수행한다.



## 2. 알고리즘 설명

### 아래에 있는 코드는 주어진 교재를 기초를 하여 만들어졌습니다.

#### 1) n개의 작업, 작업하는 기계의 개수 m을 입력받고 각 작업의 시간의 경우 1과 10사이의 난수를 입력받는다.

```
 System.out.println("몇 개의 작업을 수행하나요?");
        int n=scanner.nextInt();
        int t[]=new int [n];

        for(int i=0;i<n;i++) {
            t[i]=(int)((Math.random()*10)+1); //1과 10사이
        }

        System.out.println("몇 개의 기계가 주어지나요? ");
        int m=scanner.nextInt();
```



#### 2) 난수의 값을 확인시키기 위해 배열에 입력되어있던 t를 출력한다.

```
System.out.println("각 작업의 수행시간은: ");
        for(int i=0;i<n;i++) {
            System.out.printf("%d ",t[i]);
        }
```



#### 3)Approx_Jobscheduling 함수를 작성한다.

#####  우선 기계에 배정된 작업의 종료 시간 배열 L을 0으로 초기화 시킨다. 이 때 주의해야 하는 점은 교재의 경우  for 반복문에서 j가 1부터 시작해 m까지 반복했는데 주어진 코드는 0부터 시작했기에 m-1까지 반복한다.

```
  public void Approx_JobScheduling(int n,int m,int t[]) {
        int L[]=new int [m];
        int min;

        System.out.println("가장 늦게 끝나는 작업시간은(마지막 값) \n");
        for(int j=0;j<m;j++) {
            L[j]=0;
        }
```

#####  다음 일찍 끝나는 기게의 번호 min을 0으로 초기화 시키고 각 기계의 작업 시간을 비교해 최소시간을 정하고(L[min])을 i의 수행시간을 더하여 갱신한다. 최종적으로 가장 늦게 끝나는 작업의 종료 시간을 출력한다.

```
        for(int i=0;i<n;i++) {
            min=0;
            for(int j=1;j<m;j++) {
                if(L[j]<L[min]) {
                    min=j;
                }
            }
            L[min]=L[min]+t[i];
            System.out.printf("%d\n",L[min]);
        }
```



#### 아래의 실행 결과에서 n=8이고 기계의 수가 2일 때 작업의 수행과정은 다음 그림과 같다

<img width="1348" alt="스케쥴4" src="https://user-images.githubusercontent.com/80919306/118995393-127e6780-b9c2-11eb-84c1-7f78cf7ed039.PNG">




## 3. 전체 코드

```
import java.util.Scanner;

public class Job {

    public void Approx_JobScheduling(int n,int m,int t[]) {
        int L[]=new int [m];
        int min;

        System.out.println("가장 늦게 끝나는 작업시간은(마지막 값) \n");
        for(int j=0;j<m;j++) {
            L[j]=0;
        }

        for(int i=0;i<n;i++) {
            min=0;
            for(int j=1;j<m;j++) {
                if(L[j]<L[min]) {
                    min=j;
                }
            }
            L[min]=L[min]+t[i];
            System.out.printf("%d\n",L[min]);
        }

    }

    public static void main(String[] args) {
        long beforeTime = System.currentTimeMillis();
        Scanner scanner=new Scanner(System.in);
        Job s=new Job();

        System.out.println("몇 개의 작업을 수행하나요?");
        int n=scanner.nextInt();
        int t[]=new int [n];

        for(int i=0;i<n;i++) {
            t[i]=(int)((Math.random()*10)+1);
        }

        System.out.println("몇 개의 기계가 주어지나요? ");
        int m=scanner.nextInt();

        System.out.println("각 작업의 수행시간은: ");
        for(int i=0;i<n;i++) {
            System.out.printf("%d ",t[i]);
        }
        System.out.println("\n");
        s.Approx_JobScheduling(n,m,t);

        long afterTime = System.currentTimeMillis(); // 코드 실행 후에 시간 받아오기
        long secDiffTime = (afterTime - beforeTime)/1000; //두 시간에 차 계산
        System.out.println("시간차이(m) : "+secDiffTime);




    }
}
```



## 4. 실행 결과

<img width="584" alt="스케쥴1" src="https://user-images.githubusercontent.com/80919306/118995460-21fdb080-b9c2-11eb-8d64-b6f34ebef543.PNG">




<img width="551" alt="스케쥴2" src="https://user-images.githubusercontent.com/80919306/118995515-2c1faf00-b9c2-11eb-83ed-c55c793250fc.PNG">




<img width="654" alt="스케쥴3" src="https://user-images.githubusercontent.com/80919306/118995552-33df5380-b9c2-11eb-84a5-f76a4551304e.PNG">




## 5. 시간 복잡도

### Approx_JobScheduling 알고리즘은 n개의 작업을 하나씩 가장 빨리 끝나는 기계에 배정한다.

###  • 이러한 기계를 찾기 위해 알고리즘의 line 5~7의 for-루프가 (m1)번 수행된다. 

### • 즉, 모든 기계의 마지막 작업 종료 시간인 L[j]를 살펴보아야 하므 로 O(m) 시간이 걸린다. 

### • 따라서 시간복잡도는 n개의 작업을 배정해야하고, line 10에서 배 열 L을 탐색해야하므로 nxO(m) +O(m) = O(nm)이다.



### 6. 근사 비율

###### Approx_JobScheduling 알고리즘의 근사해를 OPT'라 하고, 최적해를 OPT라고 할 때, OPT' ≤ 2xOPT 이다.

– 즉, 근사해는 최적해의 2배를 넘지 않는다. 

– 이를 다음 그림을 통해서 이해해보자. 단, ti 는 작업 i의 수행 시간이다.

<img width="517" alt="스케쥴5" src="https://user-images.githubusercontent.com/80919306/118995602-3cd02500-b9c2-11eb-8b03-5f6997b62de9.PNG">


- 위의 그림은 Approx_JobScheduling 알고리즘으로 작업을 배정하였고, 
- 가장 마지막으로 배정된 작업 i가 T부터 수행되며, 
-  모든 작업이 T+ti 에 종료된 것을 보이고 있다. 
-  그러므로 OPT' = T+ti 이다.

<img width="572" alt="스케쥴6" src="https://user-images.githubusercontent.com/80919306/118995633-478aba00-b9c2-11eb-9d37-7f497481adda.PNG">


- 위 그림에서 T’는 작업 i를 제외한 모든 작업의 수행 시간의 합을 기계의 수 m으로 나눈 값이다. – 즉, T'는 작업 i를 제외한 평균 종료 시간이다. 

- 그러면 T ≤ T'이 된다. – 왜냐하면 작업 i가 배정된 (가장 늦게 끝나는) 기계를 제외한 모든 기계에 배정된 작업은 적어도 T 이후에 종료되기 때문이다.

- T와 T'의 관계인, T ≤ T'를 이용한 OPT' ≤ 2xOPT 증명

<img width="629" alt="스케쥴7" src="https://user-images.githubusercontent.com/80919306/118995820-66894c00-b9c2-11eb-9b16-2f2c7b0d26e7.PNG">




# 작업 스케쥴링 (greedy 알고리즘)

그리디 알고리즘을 이용한 코드를 구현하지 못했습니다. 해당 코드는 미완성 코드이며 작업 시간을 입력받고 시작 시간에 따라 정렬된 것 까지하고 while문에 대한 부분을 작성하지 못했습니다.

```
import java.util.Scanner;

public class Job {

    public void JobScheduling(int n,int m,int t[][]) {
        int L[]=new int [m];
        int min;

        for(int i=0;i<n;i++) { //시작 시간을 기준을 오름차순으로 정렬
            for(int j=i+1;j<n;j++) {
                if(t[i][0]>t[j][0]) {
                    int temp0=t[i][0];
                    t[i][0]=t[j][0];
                    t[j][0]=temp0;

                    int temp1=t[i][1];
                    t[i][1]=t[j][1];
                    t[j][1]=temp1;
                }
            }
        }
        

    }

    public static void main(String[] args) {
        long beforeTime = System.currentTimeMillis();
        Scanner scanner=new Scanner(System.in);
        Job s=new Job();

        System.out.println("몇 개의 작업을 수행하나요?");
        int n=scanner.nextInt();
        int t[][]=new int [n][2];

        for(int i=0;i<n;i++) {
            for(int j=0;j<2;j++) {
                t[i][j] = (int) ((Math.random() * 10) + 1);
            }
        }

        System.out.println("몇 개의 기계가 주어지나요? ");
        int m=scanner.nextInt();

        System.out.println("각 작업의 수행시간은: ");
        for(int i=0;i<n;i++) {
            System.out.printf("(%d %d) ",t[i][0],t[i][1]);
        }
        System.out.println("\n");
        s.JobScheduling(n,m,t);

        long afterTime = System.currentTimeMillis(); // 코드 실행 후에 시간 받아오기
        long secDiffTime = (afterTime - beforeTime)/1000; //두 시간에 차 계산
        System.out.println("시간차이(m) : "+secDiffTime);




    }
}
```

## 손작업 (그리디 알고리즘)
![KakaoTalk_20210520_231743144](https://user-images.githubusercontent.com/80919306/118995698-540f1280-b9c2-11eb-8536-6fdbf8654eb2.jpg)


