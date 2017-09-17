<br>
<p>
<center>
###“C++程序设计与训练”课程大作业项目报告
<p>
<p>
####项目名称：餐厅服务与管理系统
</center>
<br>
<br>
<br>
<br>
<p>
<p>
<p>
<center>
####姓名:马天云
####学号:2016011417
####班级:自62
####时间:2017.9.17
</center>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>

#
**目录**

- [1.系统功能设计](#1)
	- [1.1 总体功能设计](#1.1)
		- [登录界面](#1.1.1) 
		- [系统管理员界面](#1.1.2)
		- [经理界面](#1.1.3)
		- [顾客界面](#1.1.4)
		- [服务生界面](#1.1.5)
		- [厨师界面](#1.1.6)
	- [1.2 功能流程描述](#1.2)
	- [1.3 初始内置信息](#1.3)
- [2.系统结构设计](#2)
- [3.系统详细设计](#3)
	- [3.1 类结构设计](#3.1)
	- [3.2 系统界面设计](#3.2)
	- [3.3 关键设计思路](#3.3)
		- [3.3.1 Extern全局变量的使用](#3.3.1)
		- [3.3.2  SQlite3数据库的使用](#3.3.2)
		- [3.3.3  Timer库类的使用](#3.3.3)
- [4.项目总结](#4)
- [5.相关问题说明](#5)
<h1 id="1">1.系统功能设计</h1>
**YRMS餐厅管理系统**旨在实现餐厅管理系统化,使顾客用餐更加方便快捷,同时,实现了,**服务员-厨师-顾客**实时信息沟通,解决**服务员-顾客-厨师**的在现实餐厅中信息交流出错的问题,而且也实现了经理对员工的工作情况查看,以及系统管理员对餐厅信息的管理,从而使得餐厅管理一体化,更加高效的运行。基于数据库的实现,使得整个餐厅的数据可以有效存储下来。


		**本系统模拟设想了未来的一种用餐模式，即在每一个餐桌上会有一个显示屏，并配备一个机器人服务员，二者共用一个应用程序，有一名顾客入座后，相应的机器人服务员会启动并对该桌顾客服务，同时，所有餐桌启动的程序在厨房都会各有一个显示屏，每个餐桌可登入一名厨师，厨师会接收该桌顾客的订单，与该桌顾客进行信息交流，而该显示屏上登录的厨师也可以与相应的机器人服务员进行信息交流。**
<h2 id="1.1">1.1总体功能设计</h2>
具体实现的功能罗列如下:

- <span id="1.1.1">登录界面</span>
	- 不同身份用户登录
	- 注册成为顾客
- <span id="1.1.2">系统管理员界面</span>
	- 菜单管理(增加、删除、修改)
	- 用户信息查看(修改员工信息、增加员工[经理,服务生,厨师])
	**此系统不实现员工删除功能，用意将在[下文](#a)描述**
- <spqn id="1.1.3">经理界面</span>
	- 查看顾客对**所有**服务员和厨师的工作质量，工作效率的评价
	- 查看 顾客的评语
	- 查看服务员的历史服务次数和厨师的历史做菜数量
- <span id="1.1.4">顾客界面</span>
	- 选择座位入座
	- 查看菜单
	- 点菜
	- 查看已点菜
	- 加菜
	- 结账
	- 呼叫服务员
	- 查看做菜进度
	- 查看餐桌剩余情况
	- 评价厨师和服务员
- <span id="1.1.5">服务生界面</span>
	- 实时接收顾客请求
	- 实时接收厨师上菜请求
	- 实时统计服务次数
- <span id="1.1.6">厨师界面</span>
	- 实时接收顾客order
	- 确认做菜
	- 确认菜品已完成
	- 实时统计做菜数
	
			####本系统最主要的功能是实现了多用户系统，即在一次程序启动后，可以登录进入一名服务生，一名厨师，一名顾客，实现顾客，厨师，服务生实时信息沟通。

 <h2 id= "1.2">1.2功能流程描述</id>

登录主界面如图:

![a](/home/mty/DDDCPP/report/reportimages/login.png) 

**登录界面操作流程**

![a](/home/mty/DDDCPP/report/reportimages/liuc_login.png)
###模拟标准用餐过程
<br>
![a](/home/mty/DDDCPP/report/reportimages/liuc_order.png)

	**以上为一次标准的用餐过程,可以体现在本次用餐过程中的所有的实现的功能,当然,在实际使用中不一定会全部体现出.**

####服务员设计
<br>
**服务生可以实时接收所服务桌号的顾客发送过来的请求,和厨师已做好菜需要上菜的请求,并确认消息.**
####厨师设计    
<br>
**厨师界面实时刷新显示顾客的已点菜品,并勾选要做的菜品,点击*确认选菜*可认领已选菜品,做菜完毕后点击*做菜完毕*即可通知服务员端菜**
####餐厅经理设计
<br>
**餐厅经理登录后可选择*查询服务员评价*或*查询厨师评价*,点击后会弹出相应的员工列表,选择一个即可查看本人的工作质量折线图,工作效率折线图,以及历史评价,历史服务(做菜)总数**
####系统管理员设计
<br>
**系统管理员界面如图:**
![a](/home/mty/DDDCPP/report/reportimages/sys_ctrol.png)
<span id="a">
**可以对在菜单中直接进行菜品的添加修改,若删除则选中菜品点击删除菜品,但每次操作完都要提交菜品更改以保存,可点击查看账号信息以进行对用户账号的管理,其中顾客信息是不可修改的,员工信息可以直接进行修改或选择添加员工信息,但==每次操作后都要提交修改以保存==,此次不==设计删除员工信息的功能==,旨在保存历史员工信息,方面餐厅其他的事务管理。**</span>
<h2 id="1.3">1.3初始内置信息说明</h2>
<span id="b">

用户类型|用户账号|用户密码
---|---|---
系统管理员|000001|123456
经理|000002|123456
服务生|000003|123456
厨师|000004|123456
顾客|13037958306|123456
顾客|18801000859|123456

<br>

餐桌总数|初始状态
----|---
9|未使用

<br>
数据库结构

usrinfo.db|dishes.db
---|---

<br>
**usrinfo.db**
![a](/home/mty/DDDCPP/report/reportimages/usrinfo_tables.png)
**dishes.db**
![a](/home/mty/DDDCPP/report/reportimages/dish_table.png)
[点击查看数据库结构具体说明](#introsqlite)
<br>
<h1 id="2">2.系统结构设计</h1>
代码结构图如下:
![a](/home/mty/DDDCPP/report/reportimages/filetree.png)
<br>
**其中,每种用户界面需要的cpp,h,ui文件都存放在相应的文件夹之中,extrah头文件夹和extracpp文件夹存放了系统所需要的额外编写的头文件和cpp文件**
![a](/home/mty/DDDCPP/report/reportimages/treebegin.png)	
<br>
![a](/home/mty/DDDCPP/report/reportimages/sourcetree.png)
<br>
	
	在**extrah**和**extracpp**文件夹中,extern文件是我声明并定义的一些程序中使用到的全局变量,delegate文件中定义在使用model/view时的一些委托类,yrmssqliter文件中定义一些数据库操作的函数。在使用到的文件中都会引用相应的头文件,其他每一个界面文件都包含一个类,且继承了qdialog类,用作界面显示以及功能实现。
<h1 id="3">3.系统详细设计</h1>
<h2 id="3.1">3.1类结构设计</h2>
**除extrah外中的头文件外,每个头文件都是一个qdialog类,以实现相应的界面的显示,同时在相应的类的私有成员变量中,声明了要跳转的界面的类的指针,在cpp文件中会实现存储空间的分配。代码举例如下:**
~~~c
//login.h
namespace Ui {
class Login;
}

class Login : public QDialog
{
    Q_OBJECT

public:
    explicit Login(QWidget *parent = 0);
    ~Login();

private:
    Ui::Login *ui;
    Systemcontroler *syslogin;
    Chefwindow *cheflogin;
    Managerwindow *managerlogin;
    Serverwindow *serverlogin;
    Logup *logupwindow;
    Customers *customer;
    static int progress_value;
private slots:
    void logintomain();
    void on_logup_clicked();
    void on_exit_clicked();
};

~~~   
**在delegate.h文件中声明了model/view模式中需要的spinbox委托类,readonly委托类,combobox委托类,checkbox委托类,代码举例如下:**
~~~c
class SpinBoxDelegate : public QItemDelegate//设置spinbox代理
{
    Q_OBJECT

public:
    SpinBoxDelegate(QObject *parent = 0):QItemDelegate(parent){}
    //返回一个编辑控件，用来编辑指定项的数据
    QWidget *createEditor(QWidget *parent,const QStyleOptionViewItem &,const QModelIndex &)const
    {
        //返回该QSpinBox控件
        QSpinBox *editor= new QSpinBox(parent);
        editor->setMinimum(0);
        editor->setMaximum(50);
        return editor;
    }
    void setEditorData(QWidget *editor,const QModelIndex &index)const
    {

        //获得当前模式中索引对应的数值
        int value = index.model()->data(index , Qt::EditRole).toInt();
        //强制类型转换
        QSpinBox *spinbox = static_cast<QSpinBox*>(editor);
        //设置spinbox的数值
        spinbox->setValue(value);
    }
    void setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index)const
    {
        QSpinBox *spinbox = static_cast<QSpinBox*>(editor);
        //interpretText()用于解释spinbox中的文本。
        spinbox->interpretText();
        //获得编辑器中的数值
        int value = spinbox->value();
        model->setData(index,value,Qt::EditRole);
    }
    void updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index)const
    {
        //根据给定的样式编辑器更新索引对应项
        editor->setGeometry(option.rect);
    }
};
~~~
**其他三类设计类似,在此不再累赘**

<h2 id="3.2">3.2系统界面设计</h2>

**系统界面设计采用以ui界面设计为主,代码信号槽实现为辅,界面的跳转都会有相应的部件操作,同时在部分操作中有QMessagebox类窗口提醒。**

<h2 id="3.3">3.3关键设计思路</h2>

###本系统设计的亮点有如下：
<h4 id="3.3.1">1.extern全局变量的使用</h4>
~~~c
class Extern
{
public:
    static int choisen;
    static QString loginername;
    static QMap<QString,int> allloginer;
    static int progress_value;
    static int loginfocus;
    static int check_desk_choosen;
    static int customer_to_server;
    static QString chefname;
    static QString servername;
    static QString managername;
    static int cur_finished_dish;//本次厨师完成的菜品数
    static int cur_users;//所有用户数
    static QString man_chef_num;//经理选中的查看厨师
    static QString man_ser_num;//经理选中的查看服务生
    static int cur_server_to_desk;
    static int server_status;
    static int ctrl_menu_status;
};

~~~

~~~c++
int Extern::choisen=0;//临时
QString Extern::loginername="z";//临时用户名
QMap<QString,int> Extern::allloginer;
int Extern::progress_value=0;
int Extern::loginfocus=0;
int Extern::check_desk_choosen=0;
int Extern::customer_to_server=2;
QString Extern::chefname="z";
QString Extern::servername="z";
QString Extern::managername="z";
int Extern::cur_finished_dish=0;
int Extern::cur_users=0;
QString Extern::man_chef_num="z";
QString Extern::man_ser_num="z";
int Extern::cur_server_to_desk=0;
int Extern::server_status=0;//服务员在线状态
int Extern::ctrl_menu_status=0;

~~~
<span id="introsqlite">
**通过声明extern类来保持在==一次程序运行中==需要的状态信息,如本次用餐的顾客信息,经理查看的员工账号等,方便了在程序设计中的数据保持与交流。**</span>
<h4 id="3.3.2">2.sqlitle3数据库的使用</h4>
**所使用的数据库名称即与数据库中的table罗列如下**

usrinfo.db | dish.db
---- | ---

<br>
**usrinfo 中Users表存放用户信息,serverlist中存放所有服务生账号,cheflist中存放所有厨师账号,每一位厨师有一个以"自己账号"命名的表,存放历史做菜数,有一个以"自己账号+c"命名的table存放顾客的所有评价,每一位服务生也有一个以"自己名字命名的表,存放历史服务总数,另一个以"自己账号+c"的表存放顾客对本人的所有评价**

**dishes中Deshinfo存放餐桌编号以及餐桌状态,如下图,states=0表示未使用**
![a](/home/mty/DDDCPP/report/reportimages/deskinfo_tables.png)
**Dishinfo表存储所有菜品的名称和单价**
[返回查看表的结构](#b)

<h4 id="3.3.3">3.Timer库的使用</h4>
**使用Timer类库,可以实现对界面的实时刷新,实现顾客-服务生-初始实时通讯,代码举例如下**
~~~c
//chefwindow.cpp
    timer=new QTimer(this);
    timer->setInterval(100);
    timer->start();
    connect(timer,SIGNAL(timeout()),this,SLOT(fresh()));
~~~
**这段代码可以实现界面每隔0.1秒刷新一次.**

**通过以上方法,实现了实时的三角信息交流**

![a](/home/mty/DDDCPP/report/reportimages/triger.png)

<h1 id="4">4.项目总结</h1>


**自己感觉qt的上手还是需要一个比较长的过程,需要在实践中慢慢理解,比如窗口的类实现,不同窗口类之间的区别,不同model类的继承关系等,在熟悉后做做起来就会很快,同时熟练掌握几种库类的使用,在很多地方就可以多次利用了。本次大作业收获很多,很好地巩固了c++的基础知识,对面向对象设计有了更深的体会,对一个软件项目的实施也有了基本的认识,我认为这次作业最大的收获,就是极大的提高了自学的能力,大作业的完成很大一部分都是边自学边实践,在实践中熟悉,并一次次修改大作业中不满意的地方,直到做到自己认为比较完美。我希望这只是一个开始,以后会自学更多的东西,并多锻炼自己文字表达的能力,以更好的提高自己的技术。**

<h1 id="5">5.相关问题说明</h1>

**由于我是使用Ubuntu16.04的系统，在软件安装过程中比较方便，没有遇到很多在window中出现的问题，整个数据库操作也方便很多，节省了不少时间。**