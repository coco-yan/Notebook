```Python
import time
from apscheduler.schedulers.blocking import BlockingScheduler
def func():
    now = datetime.datetime.now()
    ts = now.strftime('%Y-%m-%d %H:%M:%S')
    print('do func  time :',ts)

def func2():
    #耗时2S
    now = datetime.datetime.now()
    ts = now.strftime('%Y-%m-%d %H:%M:%S')
    print('do func2 time：',ts)
    time.sleep(2)

def dojob():
    #创建调度器：BlockingScheduler
    scheduler = BlockingScheduler()
    #添加任务,时间间隔2S
    scheduler.add_job(func, 'interval', seconds=2, id='test_job1')
    #添加任务,时间间隔5S
    scheduler.add_job(func2, 'interval', seconds=3, id='test_job2')
    scheduler.start()
dojob()

1>triggers（触发器）：触发器包含调度逻辑，每一个作业有它自己的触发器
2>job stores（作业存储）:用来存储被调度的作业，默认的作业存储器是简单地把作业任务保存在内存中,支持存储到MongoDB，Redis数据库中
3> executors（执行器）：执行器用来执行定时任务，只是将需要执行的任务放在新的线程或者线程池中运行
4>schedulers（调度器）：调度器是将其它部分联系在一起,对使用者提供接口，进行任务添加，设置，删除。

https://www.cnblogs.com/fengff/p/11011000.html
```

