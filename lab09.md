# “Top-down”—至顶向下的设计方法
今天要分享一种解决问题的方法—-“top-down”方法。     
这是一种“至顶向下，逐步求精”的解决问题的思路。   
以洗衣机控制程序为例，分解洗衣过程      
注水–浸泡–漂洗-排水–脱水      
我们用伪代码再细分一下   

### 假设洗衣机可执行的基本操作如下：<br> 
water_in_switch(open_close)  // open 打开上水开关，close关闭    
    water_out_switch(open_close)  // open 打开排水开关，close关闭    
        get_water_volume()  //返回洗衣机内部水的高度    
motor_run(direction) // 电机转动。left左转，right右转，stop停    
time_counter() // 返回当前时间计数，以秒为单位    
halt(returncode) //停机，success 成功 failure 失败      

### 注水:       
  SET now=timecounter();   
  WHILE getwatervolume()< volume   
    water_in_switch(open)   
    IF time_counter()=now+timeout   
      halt(failure)   
      BREAK   
    ENDIF   
  ENDWHILE   
  waterinswitch(close)    
### 浸泡：   
SET now=timecounter();   
WHILE timecounter()<=now+time   
ENDWHILE  
ENDIF   
### 漂洗：   
motor_run(oneside)   
WHILE  time_counter() = x   //x为单方向转动时间     
motor_run(anotherside)    
IF  time_counter()>y     //y为浸泡总时间   
motor_run(stop)   
ENDWHILE   
### 排水：   
SET now=time_counter();   
WHILE get_water_volume()>0    
water_out_switch(open)    
    IF time_counter()=now+timeout   
    halt(failure)   
    BREAK   
    ENDIF   
IF get_water_volume()=0   
water_out_switch(close)   
ENDIF    
END WHILE     
### 脱水：   
SET now=time_counter();  
water_out_switch(open)   
motor_run(rightorleft)   
IF time_counter()= now+timeout     
motor_run(stop)   
ENDIF   

可以看到程序又被细分为了打开进（排）水口和电机转动之类更具体的操作   

总之，当我们将问题逐步地分解，至顶向下，我们最终就会得到最基本最清晰的部分。这样问题就容易解决得多了. 
