# TFP와 JFP
* uniprocessor scheduling 알고리즘 은 크게 TFP(Task-level fixed-priority)와 JFP(Job-level fixed-priority)로 나눌 수 있다
* TFP의 경우 Task를 기준으로 priority를 정하며 optimal한 알고리즘으로 RM(Rate monotonic)이 있으며 각 Task의 Period에 의해 priority가 정해지며 한 번  정해진 Task별 Priority는 변하지 않는다.
* JFP의 경우 Job을 기준으로 priority가 정해지며 optimal한 알고리즘으로 EDF(Earliest daedline first)가 있으며 각 Job에 대한 현재 남아있는 deadline을 기준으로 priority가 정해지기 때문에 priority에 따라 실행중인 job이 바뀐다

# RTA for RM
* TFP에서 가장 optimal 한 알고리즘인 RM에 대한 Exact한 Analysis중 하나인 RTA(Response Time Analysis)가 있는데 
* 이는 deadline miss에 대하여 보장할 수 있다. 즉, RTA에서 deadline miss가 일어난다면 해당 Task set은 무조건 deadline miss가 나며 RTA에서 deadline miss가 안 날 경우 deadline miss가 무조건 없다.
ddd
![image](https://user-images.githubusercontent.com/77715064/167279662-9ad20679-94f5-4a98-9246-dbd2e5bccc82.png)

* 위의 식을 성립시키는 값이 response time이며 response time<=deadline을 만족시키는지 여부를 판단하면 된다