​       学习计算机专业的学生，比如说像本人这样的零基础小白，在刚开始写代码时都难免会遇到觉得编程问题过于复杂，坐在电脑前许久不知如何下手的情况。下面介绍的方法就是针对缓解这种问题的。

## 自顶向下，逐步求精

​        Top-down design（自顶向下）,指不直接从大问题着手，而是先把大问题向下一层一层分解成小问题，方便我们找到问题的关键、突破口所在，从而对问题逐个击破。

​       逐步求精指将现实问题经过几次抽象（细化）处理，最后到求解域中只是一些简单的算法描述和算法实现问题。即将系统功能按层次进行分解，每一层不断将功能细化，到最后一层都是功能单一、简单易实现的模块。求解过程可以划分为若干个阶段，在不同阶段采用不同的工具来描述问题。![点击查看源网页](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1541740268080&di=0de172985397e3fb2f3275bc2820540c&imgtype=0&src=http%3A%2F%2Fp.ananas.chaoxing.com%2Fstar%2F1024_0%2F1389060374566hrlcx.jpg)

简单点说就是把任务分得觉得再分就是浪费时间为止，这样处理问题就看起来容易下手得多。

下面我们以洗衣机为实例介绍这一方法：

![微信图片_20181109102643.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20181109102643.png?raw=true)

我们可以看到洗衣机上的按键，可以选择水量，洗衣模式，洗衣机会根据这两个选项决定洗衣时间。

#### 洗衣机的程序需要控制完成下列事情：

用户选择洗衣模式，输入水量，决定洗衣时间

打开上水开关注水，实时返回洗衣机内部水的高度，达到预定水量时停止

根据洗衣模式、时间分配浸泡、漂洗、脱水时间

浸泡规定时间后进行漂洗，每周期内电机往左转动n次，往右转动n次，实时返回当前时间计数

漂洗规定时间后，打开排水开关直至水排开，即水高度为0

开始脱水，每周期内电机往左转动n次，往右转动n次

脱水规定时间后，停机

#### 相对应伪代码：

Read(mod,water_ volume，wash_time)

WHILE get_water_volume <=water_volume 

water_in_switch(open)

IF time_counter>timeout

water_in_switch(close)

halt(failure)

ELSE

ENDWHILE

water_in_switch(close)

time_assign(soak,rinse,spin-dry)

WHILE time_counter>=time_assign(soak)

ENDWHILE

calculate how many circuits of time_assign(rinse) has

REPEAT

in every single circuit

motor_run(left) for n times,motor_run(stop)

motor_run(right) for n times,motor_run(stop)

UNTIL  time_counter<=time_assign(rinse)

WHILE get_water_volume>=0

water_out_switch(open)

ENDWHILE

water_out_switch(close)

REPEAT

in every single circuit

motor_run(left) for n times,motor_run(stop)

motor_run(right) for n times,motor_run(stop)

UNTIL  time_counter<=time_assign(spin-dry)

halt(success)