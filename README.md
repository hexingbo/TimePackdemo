# TimePackdemo
a many beautiful timepick for android 高仿ios选择器

几乎完美还原iOS 的 AlertViewController ，同时支持Alert和ActionSheet模式，每一个细节都是精雕细琢，并把api封装成懒到极致模式，一行代码就可以进行弹窗.

demo是用Module方式依赖，你也可以使用gradle 依赖:
```java
   implementation 'com.github.hexingbo:TimePackdemo:1.01'
```

### config in java code
####第一种：
```java
 DatePickerDialog dialog = new
                        DatePickerDialog(MainActivity.this, new DatePickerDialog.OnDateSetListener() {
                            @Override
                            public void onDateSet(DatePicker view, int year, int monthOfYear, int
                                    dayOfMonth) {

                                if(monthOfYear<=9){
                                    mouth1="0"+(monthOfYear+1);
                                }else{
                                    mouth1=String.valueOf(monthOfYear+1);
                                }
                                if(dayOfMonth<=9){
                                    day1= "0"+dayOfMonth;
                                }else{
                                    day1=String.valueOf(dayOfMonth);
                                }
                                dateStr = String.valueOf(year)+"-"+mouth1+"-"+day1;
                                button1.setText(dateStr);


                            }
                        }, calender.get(Calendar.YEAR), calender.get(Calendar.MONTH),
                        calender.get(Calendar.DAY_OF_MONTH));
                dialog.show();        
```
####第二种：
```java
 TimePickerDialog dialog = new TimePickerDialog(MainActivity.this, new TimePickerDialog.OnTimeSetListener() {
                    @Override
                    public void onTimeSet(TimePicker view, int hourOfDay, int minute) {

                        button2.setText(String.valueOf(hourOfDay+":"+minute));

                    }
                },calender2.get(Calendar.HOUR),calender2.get(Calendar.MINUTE),false);
                dialog.show();
```
####第三种：
```java
 TimePickerView pvTime = new TimePickerView.Builder(MainActivity.this, new TimePickerView.OnTimeSelectListener() {
                    @Override
                    public void onTimeSelect(Date date2, View v) {//选中事件回调
                        String time = getTime(date2);
                       button3.setText(time);
                    }
                })
                        .setType(TimePickerView.Type.YEAR_MONTH_DAY)//默认全部显示
                        .setCancelText("取消")//取消按钮文字
                        .setSubmitText("确定")//确认按钮文字
                        .setContentSize(20)//滚轮文字大小
                        .setTitleSize(20)//标题文字大小
//                        .setTitleText("请选择时间")//标题文字
                        .setOutSideCancelable(true)//点击屏幕，点在控件外部范围时，是否取消显示
                        .isCyclic(true)//是否循环滚动
                        .setTextColorCenter(Color.BLACK)//设置选中项的颜色
                        .setTitleColor(Color.BLACK)//标题文字颜色
                        .setSubmitColor(Color.BLUE)//确定按钮文字颜色
                        .setCancelColor(Color.BLUE)//取消按钮文字颜色
//                        .setTitleBgColor(0xFF666666)//标题背景颜色 Night mode
//                        .setBgColor(0xFF333333)//滚轮背景颜色 Night mode
//                        .setRange(calendar.get(Calendar.YEAR) - 20, calendar.get(Calendar.YEAR) + 20)//默认是1900-2100年
//                        .setDate(selectedDate)// 如果不设置的话，默认是系统时间*/
//                        .setRangDate(startDate,endDate)//起始终止年月日设定
//                        .setLabel("年","月","日","时","分","秒")
                        .isCenterLabel(false) //是否只显示中间选中项的label文字，false则每项item全部都带有label。
//                        .isDialog(true)//是否显示为对话框样式
                        .build();
                pvTime.setDate(Calendar.getInstance());//注：根据需求来决定是否使用该方法（一般是精确到秒的情况），此项可以在弹出选择器的时候重新设置当前时间，避免在初始化之后由于时间已经设定，导致选中时间与当前时间不匹配的问题。
                pvTime.show();

```
####第四种：
```java
  OptionsPickerView pvOptions = new  OptionsPickerView.Builder(MainActivity.this, new OptionsPickerView.OnOptionsSelectListener() {
                    @Override
                    public void onOptionsSelect(int options1, int option2, int options3 ,View v) {
                        //返回的分别是三个级别的选中位置
                       String s =  options1Items.get(options1);
                        button4.setText(s);

                    }
                })
//                        .setSubmitText("确定")//确定按钮文字
//                        .setCancelText("取消")//取消按钮文字
//                        .setTitleText("城市选择")//标题
                        .setSubCalSize(20)//确定和取消文字大小
//                        .setTitleSize(20)//标题文字大小
//                        .setTitleColor(Color.BLACK)//标题文字颜色
                        .setSubmitColor(Color.BLUE)//确定按钮文字颜色
                        .setCancelColor(Color.BLUE)//取消按钮文字颜色
//                        .setTitleBgColor(0xFF333333)//标题背景颜色 Night mode
//                        .setBgColor(0xFF000000)//滚轮背景颜色 Night mode
//                        .setContentTextSize(18)//滚轮文字大小
//                        .setTextColorCenter(Color.BLUE)//设置选中项的颜色
                        .setTextColorCenter(Color.BLACK)//设置选中项的颜色
//                        .setLineSpacingMultiplier(1.6f)//设置两横线之间的间隔倍数
//                        .setLinkage(false)//设置是否联动，默认true
//                        .setLabels("省", "市", "区")//设置选择的三级单位
//                        .isCenterLabel(false) //是否只显示中间选中项的label文字，false则每项item全部都带有label。
//                        .setCyclic(false, false, false)//循环与否
//                        .setSelectOptions(1, 1, 1)  //设置默认选中项
//                        .setOutSideCancelable(false)//点击外部dismiss default true
//                        .isDialog(true)//是否显示为对话框样式
                        .build();
                pvOptions.setPicker(options1Items);
                pvOptions.show();
```
####第五种：
```java
   final String[] str = new String[10];
   ChangeDatePopwindow mChangeBirthDialog = new ChangeDatePopwindow(MainActivity.this);
   mChangeBirthDialog.setDate("2017", "6", "20");
   mChangeBirthDialog.showAtLocation(main, Gravity.BOTTOM, 0, 0);
    mChangeBirthDialog.setBirthdayListener(new ChangeDatePopwindow.OnBirthListener() {

           @Override
           public void onClick(String year, String month, String day) {
           // TODO Auto-generated method stub
          Toast.makeText(MainActivity.this,year + "-" + month + "-" + day,Toast.LENGTH_LONG).show();
          StringBuilder sb = new StringBuilder();
          sb.append(year.substring(0, year.length() - 1)).append("-").append(month.substring(0, day.length() - 1)).append("-    ").append(day);
          str[0] = year + "-" + month + "-" + day;
          str[1] = sb.toString();

            button5.setText(str[0]);

        }
   });
```
####第六种：
```java
     final String[] str = new String[10];
                final ChangeDatePopwindow2 mChangeBirthDialog = new ChangeDatePopwindow2(MainActivity.this);
                mChangeBirthDialog.setDate("2017", "6", "20");
                mChangeBirthDialog.showAtLocation(main, Gravity.BOTTOM, 0, 0);
                mChangeBirthDialog.setBirthdayListener(new ChangeDatePopwindow2.OnBirthListener() {

                    @Override
                    public void onClick(String year, String month, String day) {
                        // TODO Auto-generated method stub
                        Toast.makeText(MainActivity.this,year + "-" + month + "-" + day,Toast.LENGTH_LONG).show();
                        StringBuilder sb = new StringBuilder();
                        sb.append(year.substring(0, year.length() - 1)).append("-").append(month.substring(0, day.length() - 1)).append("-").append(day);
                        str[0] = year + "-" + month + "-" + day;
                        str[1] = sb.toString();
//                        mChangeBirthDialog.getBgtext().setText(year);
//                        mChangeBirthDialog.update();
                        button6.setText(str[0]);

                    }
                });
```
####第七种：
```java
     TimePickerView pvTime = new TimePickerView.Builder(MainActivity.this, new TimePickerView.OnTimeSelectListener() {
                    @Override
                    public void onTimeSelect(Date date2, View v) {//选中事件回调
                        String time = getTime(date2);
                        button7.setText(time);
                    }
                })
                        .setType(TimePickerView.Type.YEAR_MONTH_DAY)//默认全部显示
                        .setCancelText("取消")//取消按钮文字
                        .setSubmitText("确定")//确认按钮文字
                        .setContentSize(20)//滚轮文字大小
                        .setTitleSize(20)//标题文字大小
//                        .setTitleText("请选择时间")//标题文字
                        .setOutSideCancelable(true)//点击屏幕，点在控件外部范围时，是否取消显示
                        .isCyclic(true)//是否循环滚动
                        .setTextColorCenter(Color.BLACK)//设置选中项的颜色
                        .setTitleColor(Color.BLACK)//标题文字颜色
                        .setSubmitColor(Color.BLUE)//确定按钮文字颜色
                        .setCancelColor(Color.BLUE)//取消按钮文字颜色
//                        .setTitleBgColor(0xFF666666)//标题背景颜色 Night mode
//                        .setBgColor(0xFF333333)//滚轮背景颜色 Night mode
//                        .setRange(calendar.get(Calendar.YEAR) - 20, calendar.get(Calendar.YEAR) + 20)//默认是1900-2100年
//                        .setDate(selectedDate)// 如果不设置的话，默认是系统时间*/
//                        .setRangDate(startDate,endDate)//起始终止年月日设定
//                        .setLabel("年","月","日","时","分","秒")
                        .isCenterLabel(false) //是否只显示中间选中项的label文字，false则每项item全部都带有label。
                        .isDialog(true)//是否显示为对话框样式
                        .build();
                pvTime.setDate(Calendar.getInstance());//注：根据需求来决定是否使用该方法（一般是精确到秒的情况），此项可以在弹出选择器的时候重新设置当前时间，避免在初始化之后由于时间已经设定，导致选中时间与当前时间不匹配的问题。
                pvTime.show();
            }
        });
```
###时间格式化
```java
    public String getTime(Date date) {//可根据需要自行截取数据显示
        SimpleDateFormat format = new SimpleDateFormat("yyyy年MM月dd日");
        return format.format(date);
    }
```

另外还支持窗口界面拓展，更多操作请下载Demo看。

###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/1.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/2.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/3.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/4.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/5.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/6.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/7.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/8.png)
###
![image](https://github.com/PangHaHa12138/TimePackdemo/blob/master/screenshot/9.png)
