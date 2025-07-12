- ui文件，设计模式
- .pro项目文件
- ### 指针
	- int  * p =new int;                           //声明一个指针变量p，分配一个int类型的内存
	- * p =99；                                      //将99赋值给p的地址
	- cout<<"打印指针p指向的地址："<<p<<endl;                          //  == 0x1f1100
	- cout<<"打印赋值为99后指针p存放的值："<<* p<<endl;        //  == 99
	- delete p;         //释放指针p的内存
	- p=NULL;        //指针指向0地址，即置空。==一定记得要在释放后加上
	- ==对指针进行判空：== if(NULL!=p)   //如果指针不为空的话则
- ### 引用
	- 在声明时就要初始化,初始化后不能指向其他对象：int hour;   //定义引用：int& s_hour = hour;  s_hour=xxx；cout<<hour<<endl; return 0;
	- 把引用作为形参，调用时实参可直接为变量本身
		- void calcHour(int& s_tick,int& s_hour){
			- s_hour = s_tick/3600;
		- }
		- int main()
			{
			- int tick=0;
			- int hour;
			- calcHour(tick,hour);    //直接将变量作为实参计算hour的值
			- cout<<hour<<endl;
			- return 0;
			}
- ### 类的继承
	- 公有public：父类的public和protected成员可以分别继承给子类。
	- 私有private：父类的public和protected可以写到子类的private中；父类的private成员只能用父类原有的方法访问
	- 保护protected：子类的protected中可以直接使用父类public和protected中的成员
	- 例子
		class Calctime
			`{
				`private://成员只能在下面的public中使用，不能离开父类
				`public:
			`}；
		//类CalcAllTime通过公有继承方式继承基类CalcTime
		`class CalcAllTime：public CalcTime`
		{
			`public：
			`//外部接口，输出转换的秒值
			`数据类型 函数（数据类型 变量）
			`{局部变量；父类成员=局部变量；return 局部变量}`
			
			//判断变量是否符合条件的标志位
			int calcFlg(int count)
			{
				int validFlag=0; //判断tick是否符合条件的标志位
				
				if(count>=0&&count<=366)
				{
					validFlag=1;  //符合则返回1，然后转换时间
				}
				return validFlag;
			}
			//获取转换的时间并打印显示
			void dispTime(int count)
			{
				int month;
				int day;
				const char* weekday;
				
				//当count的值在0~366之间时，获取转换的时间值
				if(calcFlg(count)==1)
				{
					month=getMonthVal(count);
					
					day=getDayVal(count);
					
					weekday=get_weekday(getWeekdayVal(count));
					
					//打印转换之后的时间结果
					cout <<"Current time:2022年"<<month<<"月"<<day<<"日"<<weekday<<endl;
				}
			}
		}；
		`//主函数
		int main()
		{
			CalcAllTime ct;
			int xxx
			`ct.dispTime(xxx)`
			return 0;
		}
- ### 多态
	- class CalcTime
	- {
		- private:
		- public:
			- ==virtual== **xxx()**  //加上virtual关键字来修饰他可以被继承的子类重写，称为虚方法，实现多态
	- }
	- class CalcMin:public CalcTime     //公有继承父类CalcTime
	- {
		- private:
		- public:
			- **xxx()
	- }
- ### 重载
		class CalcTime
		{
			public:
				int xxx;
				int zzz;
				void calcTimeVal(==bool== xxxFlg,int tick)
				{
					if(xxxFlg== 1&&tick>=0&&tick<=99){
					xxx=;
					cout<<xxx<<endl;
					}
				}
				void calcTimeVal(bool xxxFlg,bool zzzFlg,int tick)
				{
					if(xxxFlg== 1&&zzzFlg== 1 && tick>=0&&tick<=99){
					xxx=;
					zzz=;
					cout<<xxx<<zzz<<endl;
				}
		}
		int main()
		{
			CalcTime ct;
			int tick;
			ct.calcTimeVal(1,tick);
			ct.calcTimeVal(1,1,tick);
			return 0;
		}
- ### 抽象
	- //抽象类，不能创建对象，只能用于继承
	- class Time{public：==virtual void dispTime（）=0==；}；
	- class CalcTime：public Time{pubilc：void dispTime（）{}}；
- ### 接口
	- //接口特点：公有；纯虚；抽象；可继承
	- class Interface{**public**：**virtual** void CalcTime（int tick）**=0**；}
	- class CalcTime：public Interface{pubilc：void CalcTime（int tick）{}}；
- ### 异常处理
	- 使用if语句
	- class CalcTime{pubilc：void CalcTimeVal（int tick）{if（）{throw"";}else}}；//抛出异常信息
	- int main()
	- {
		- CalcTime ct;
		- try{ct.calcTimeVal(tick);}          //保护代码
		- catch(const char* e){cout<<e<<endl;}            //捕获异常信息并输出提示
		- return 0;}
### exec()
    exec() 函数是 Qt 框架中用于显示模态对话框的重要方法。它的主要作用是 显示模态对话框并阻塞当前线程的执行，直到对话框关闭。使用 exec() 可以让对话框在被打开时，阻止用户与其他窗口进行交互，直到对话框被关闭为止。
- exec() 函数的用法和意义：
	1.显示模态对话框：
		2.exec() 用于启动一个模态对话框，即一个在显示时会阻止用户与其他窗口交互的对话框。只有在对话框关闭之后，用户才能回到主界面继续操作。
		3.当 exec() 被调用时，它会显示对话框并进入一个事件循环，直到对话框被关闭（例如点击“OK”或“Cancel”按钮）才会返回。
	2.阻塞调用线程：
		5.exec() 是一个阻塞操作。调用 exec() 后，程序会暂停执行当前的代码，直到对话框关闭后，程序才会继续执行后续的代码。
		6.这意味着在调用 exec() 期间，程序不会响应用户的其他交互，直到对话框关闭。
	7.返回值：
		8.exec() 会返回一个整数值（通常是 QDialog::Accepted 或 QDialog::Rejected），表示用户在对话框中的选择。通常，Accepted 表示用户点击了“确定”或“OK”按钮，而 Rejected 表示用户点击了“取消”或关闭了对话框。
	9.典型应用：
		10.exec() 函数常用于模态对话框的使用场景中，如确认、设置、输入等对话框。它允许应用程序暂停执行，直到用户做出选择。
	示例：
		假设有一个简单的对话框，用户可以选择“OK”或“Cancel”。当你调用 exec() 时，程序会等待用户做出选择，之后返回执行代码。
			Dialog *dialog = new Dialog(this);
			dialog-&gt;setWindowTitle("Modal Dialog");
			
			// 显示模态对话框，直到用户关闭它
			int result = dialog-&gt;exec();
			
			if (result == QDialog::Accepted) {
			    // 用户点击了“OK”按钮
			    qDebug() &lt;&lt; "OK button clicked!";
			} else {
			    // 用户点击了“Cancel”按钮
			    qDebug() &lt;&lt; "Cancel button clicked!";
			}
	总结：
		11.exec() 使得对话框成为模态对话框，用户必须先与对话框交互并关闭对话框，才会继续执行后续代码。
		12.它的返回值帮助程序判断用户的选择（如点击 OK 或 Cancel）。
		13.用于需要强制用户完成某项操作或确认的场景，防止用户在未完成当前操作前与其他窗口交互。
### 字节和字符
-  **字节（Byte）**：一个字节是由 8 位（bit）组成的二进制数据单位，能够表示的数值范围是从 0 到 255
- **字符（Character）**：字符是计算机中表示文本的基本单位，可以表示字母、数字、符号等。 字符的大小（即占用多少字节）取决于所使用的编码方式。
- 在**ASCII 编码**中，一个字符通常占用 1 字节。ASCII 仅包含 128 个字符（包括字母、数字、标点符号和控制字符），因此一个字符正好对应一个字节
- **UTF-16** 通常使用 2 字节来表示一个字符，但对于某些字符（如表情符号），可能需要 4 字节来表示
- **UTF-8**是一种可变长度的字符编码方式，一个字符可以占用 1 到 4 个字节。英文字符（例如 'A'）只占用 1 字节，一些常见的非英文字符（例如汉字）通常占用 3 个字节。
### 槽
//头文件mainwindow.h
	private plots:  //`private slots:` 是 Qt 中特有的概念，用于定义**槽函数**的访问权限
		void MainWindow::on_bloodStart_clicked(bool checked)
// 连接信号与槽,cpp文件：MainWindow::MainWindow(QWidget * parent) : QMainWindow(parent), ui(new Ui: :MainWindow)
    {   connect (ui -> bloodStart, & QPushButton :: clicked, this, &MainWindow::on_bloodStart_clicked ）；}
//槽函数
	void MainWindow::on_bloodStart_clicked(bool checked)
	{
	    if (*mUARTOpenFlag* && **mSerialPort->isOpen()**) 
	    {
        // 启动测量命令包
        **QByteArray** startCommand = **QByteArray::fromHex**("14 81 80 80 80 80 80 80 80 95");
        mSerialPort->write(startCommand);
        qDebug() << "发送启动测量命令包: " << startCommand.toHex();
	    } 
	    else {
        QMessageBox::warning(this, "警告", "串口未打开或无法连接");
	    }	}
### 打包解包
//头文件：packunpack.h //直接添加文件对h和cpp
### 串口
//头文件
```c++
private:   //用于定义类中的私有成员（变量、函数等），这些成员是不能在类的外部直接访问的
QSerialPort  *mSerialPort; // 串口类
	bool mUARTOpenFlag; //串口状态
	QByteArray mRxData; //接收数据暂存
	QList<uchar>mPackAfterUnpack;  //解包后的数据
```
		 
//cpp文件
```c++
	MainWindow::MainWindow(QWidget *parent) :
	    QMainWindow(parent),
	    ui(new Ui::MainWindow)
	{
	    ui->setupUi(this);
		mUARTOpenFlag=false;
	}
	void MainWindow::on_openUARTButton_clicked(bool checked)
	{
		qDebug() << ui->uartNumComboBox（串口窗口）->currentText(); //获取当前串口号
		if(!mUARTOpenFlag)
		{
			mSerialPort = new QSerialPort;    //创建串口对象
	        mSerialPort->setPortName(ui->uartNumComboBox->currentText());//获取选中的串口号
	        if(mSerialPort->open(QIODevice::ReadWrite))
	        {
	        //设置界面中的参数
	        QObject::connect(mSerialPort, &QSerialPort::readyRead, this, &MainWindow::readSerial);  //连接信号与槽
	        }
	        else	        
	        {
            QMessageBox::about(NULL, "提示", "串口无法打开\r\n不存在或已被占用");
            mUARTOpenFlag=false;
            return;  	        
            }
            mUARTOpenFlag=true;
		}
	}
	
//串口数据读取
	void MainWindow::readSerial()
	{
	    mRxData = mSerialPort->readAll();
	    if(!mRxData.isEmpty())     //如果非空说明有数据接收
	    {
	        if(ui->unpackCheckBox->checkState())
	        {
	            procUARTData();    //PCT解包并显示
		    }
	        else if(ui->showHexCheckBox->checkState())  //是否解包显示，，Hex显示
	        {
	            QString str = mRxData.toHex().data();     //转换成16进制大写
	            str = str.toUpper();
	            QString buffer;
	            for(int i = 0; i < str.length(); i += 2)	            {
	                buffer += str.mid (i, 2);
	                buffer += " ";      //一个16进制占4位，8位为一字节，所以每两位16进制空一格
	            }
            ui->receiveTextBrowser->*append*(buffer);//显示
	        }
	        else	        
	        {
	            ui->receiveTextBrowser->append(mRxData);//显示 
	        }
	    }
	    mRxData.clear();//清空已显示的数据
	}
```

### 清除槽函数
	//清除发送区
	ui->(界面的区域，比如：发送区块的ui名称:)sendPlainTextEdit->clear()；
### 文件读取保存
1. QFileDialog类：使用getOpenFileName（）方法
	打开一个对话框，标题为Open Image，在对话框中显示“/home/jana"目录中的内容，仅显示后缀为.png * .jpg * .bmp的文件：
	```c++
	QString fileName = QFileDialog: : getOpenFileName(this,tr("Open Image"),"/home/jana",tr("Image Files(*.png *.jpg *.bmp)")); 
	``` 
2. QFile类
	- QFile: :QFile(const QString &name): 用于构造一个以name为文件名的QFile对象
	- bool QFile: :open(OpenMode mode)：打开文件，参数open指定打开模式
### 绘制曲线图
1. 坐标轴（QAbstractAxis类）
2. 系列（QAbstractSeries类）
3. 图表（QChart类）
	1. 初始化波形绘制区域
	void Widget::initWaveLineChart()
	{
	    mAxisX = new QValueAxis(); 	    mAxisY = new QValueAxis();	    mSeries = new QLineSeries();	    mWaveLineChart = new QChart();
	    **////添加曲线到chart中**
	    mWaveLineChart->addSeries(mSeries); 
	    **//设置Y轴范围 ，设置x轴范围**
		mAxisX->setRange(0, 2048);   mAxisY->setRange(0, 4096);  
		//不显示线框
		mAxisX->setGridLineVisible(false);  mAxisY->setGridLineVisible(false); 
		**//不显示坐标轴刻度**
		mAxisX->setLabelsVisible(false);   mAxisY->setLabelsVisible(false); 
		//把坐标轴添加到chart中，第二个参数是设置坐标轴的位置，
	    ***//只有四个选项，下方：Qt::AlignBottom，左边：Qt::AlignLeft，右边：Qt::AlignRight，上方：Qt::AlignTop***
	    mWaveLineChart->addAxis(mAxisX, Qt::AlignBottom);    mWaveLineChart->addAxis(mAxisY, Qt::AlignLeft);
	    **//把曲线关联到坐标轴**
	    mSeries->attachAxis(mAxisX); 	    mSeries->attachAxis(mAxisY);
	    **//设置标题**
	    mWaveLineChart->setTitle("波形显示区");
	    **//设置线的颜色**
	    mSeries->setColor(QColor(Qt::black));
	    //设置外边界全部为0
	    mWaveLineChart->layout()->setContentsMargins(0, 0, 0, 0); 
	    //设置内边界全部为0
	    mWaveLineChart->setMargins(QMargins(0, 0, 0, 0));         
	    //设置背景区域无圆角
	    mWaveLineChart->setBackgroundRoundness(0);         
	    //不显示注释       
	    mWaveLineChart->legend()->hide();                         
	    **//把设置好的QChart与QChartView进行绑定**
	    ui->waveGraphicsView->setChart(mWaveLineChart);           
	}
4. 视图（QChartView类）
### 进度条
	ui->procDataProgressBar->setRange(0, 链表.length() - 1);   //设置进度条范围
    ui->procDataProgressBar->setValue(0);  //设置当前进度值
    ui->procDataProgressBar->setVisible(true);  //设置进度条是否可见
### <<
1. 调试输出：`<<` 最常见的用途是在 `qDebug()`、`qInfo()`、`qWarning()`、`qCritical()` 等调试函数中，用来输出不同类型的数据到控制台。通过将数据传递给调试流，可以方便地打印调试信息。
2. 自定义输出：可以重载 `operator<<`，使得自定义类型也能像基本类型那样通过 `qDebug()` 等输出。假设你有一个自定义的类 `Person`，你可以重载 `<<` 操作符来输出 `Person` 对象的内容：QDebug **operator<<**(QDebug debug, const **Person** &person) { debug.nospace() << "Person(name: " << person.name << ", age: " << person.age << ")";     return debug; }
	1. 将 `Person` 类型的对象（`person`）与 `QDebug` 类型的对象（`debug`）结合起来，以便在使用 `qDebug()` 输出调试信息时能够正确显示 `Person` 对象的信息。
	2. `&` 表示 `person` 参数是一个 **常量引用**（`const Person&`）
		1.  **避免不必要的拷贝**
			- **效率**：如果不使用引用，函数将会接受 `person` 的一个副本，即对 `Person` 对象进行复制。对于大型对象（尤其是包含大量数据或动态分配内存的对象），这种复制会带来额外的开销。
			- **引用传递**：通过引用传递（`&`），函数直接操作传入的原始对象，而不会创建副本，从而节省了内存和性能开销。
		2.  **保护原对象不被修改**
			- **`const` 修饰**：`const` 表示 `person` 对象在该函数内部不可修改。你不能改变 `person` 的成员变量或调用其非 `const` 成员函数。这样可以确保你仅仅读取该对象的内容而不会意外地修改它，符合只读操作的预期。
		3.  **避免临时对象的创建**
			- *如果不使用引用，而是传值（即不加 `&`），那么在调用 `operator<<` 时，Qt 会生成一个临时 `Person` 对象，传递给重载的操作符。这不仅消耗性能，而且也会让代码变得不必要复杂。*
			- 使用引用（`const Person&`）可以直接使用原始对象，而避免了创建临时副本。
		4.  **提升代码的可维护性和可读性**
			- 使用引用和 `const` 能够明确表达你希望传递的是一个对象的引用，并且不打算修改它。这种方式让代码意图更清晰，也有助于维护者理解这段代码的使用方式。
	3. - `debug.nospace()` 通过点符号调用该函数，以控制 `QDebug` 对象输出时是否插入空格。
### 基类QMainWindow：提供一个主应用程序窗口
1. 菜单栏QMenuBar
	1. 菜单QMenu
		1. 向菜单栏中添加菜单addMenu()
		2. 向菜单中添加子菜单addMenu()
	2. 菜单项QAction
		1. 向菜单栏或菜单中添加菜单项addAction
		2. `ui->menuBar->addAction(tr("串口设置"), this, SLOT(menuSetUART()));
	3. 对应的槽函数
	```c
	//"串口设置"按钮，按下，的槽函数
	void MainWindow::menuSetUART()
	{
	    qDebug() << "click setUART";
	    FormSetUART *formSetUART = new FormSetUART();
	    connect(formSetUART, SIGNAL(uartSetData(QString, int, int, int, int, bool)), this, SLOT(initSerial(QString, int, int, int, int, bool)));
	    formSetUART->show();
	}
	```
2. 工具栏
3. 停靠窗口
4. 状态栏
	1. 设置
	```c
	mFirstStatusLabel = new QLabel();
    mFirstStatusLabel->setMinimumSize(200, 18);   //设置标签最小尺寸
    QFont font("Microsoft YaHei", 10, 50);                //字体和大小
    mFirstStatusLabel->setFont(font);                       //设置
    mFirstStatusLabel->setText(tr("串口未配置"));     //设置标题？
    ui->statusBar->addWidget(mFirstStatusLabel);  //应用到状态栏中
    ```
5. 中央窗口
- 添加图片资源文件
	1. 向MainwindowLayout文件夹中添加文件
	2. 右击项目名MainwindowLayout，选择Add New，选择Qt→Qt Resource File，设置名称为存放图片的文件夹名，单击下一步，完成
	3. 错误打开其他文件，右击文件选择Open in Editor，进入编辑模式
	4. 在编辑模式下单击“添加”下拉菜单，选择“添加前缀”，“添加”，“添加文件”，选中图片，打开
- 在标签或按钮上显示图片
	1. 右击标签或按钮，“改变样式表”，“添加资源”，border-image，“prefix1中的image，单击图片，OK，ok
- 基本组成
	1. MainWindow::MainWindow(QWidget * parent) :
    QMainWindow(parent),
    ui(new Ui: :MainWindow) {
	2. ui->setupUi(this);
	3. 设置标题：setWindowTitle(tr("xxxxx"));
	4. 设置边框：ui->exxxLabel->setStyleSheet("border:1px solid black;");  //有多少个框设置多少个
	5. 设置菜单栏（在顶部）：ui->menuBar->addAction(tr("状态栏的名字"), this, SLOT(menu相关函数())); 
	6. 设置状态栏（底部）：
	```c++
	mFirstStatusLabel = new QLabel();
	mFirstStatusLabel->setMinimumSize(200, 18); //设置标签最小尺寸
	QFont font("Microsoft YaHei", 10, 50);
	mFirstStatusLabel->setFont(font);
	mFirstStatusLabel->setText(tr("状态xxx"));
	ui->statusBar->addWidget(mFirstStatusLabel);
	```
	7. 如果有打包解包：mPackUnpack = new PackUnpack();
					mPackAfterUnpackArr = new uchar*[PACK_QUEUE_CNT];
				    for(int i = 0; i < PACK_QUEUE_CNT; i++)
				    {
				        mPackAfterUnpackArr[i] = new uchar[10]{0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
				    }
				    在常量定义处添加模块ID和二级ID
	8. 画布初始化：QPixmap pix画布名字(WAVE_X_SIZE, WAVE_Y_SIZE);
			    mPixmap画布名字 = pix画布名字;
			    mPixmap画布名字.fill(Qt: :white);
	9. 如果有定时器：mTimer = startTimer(20);  //打开定时器，前提要在头文件中加上#include < QTimer>
	10. 初始化参数：uiInit();  ui->名字InfoGroupBox->installEventFilter(this);
	11. 析构方法：MainWindow::~MainWindow()   {      delete ui;   }
### bool
1. `bool` 是一种数据类型，用于表示布尔值（真或假），只有两个可能值，true，false
2.  `bool` 在 Qt 中的作用
	**条件判断**：`bool` 用来控制程序的流程，例如在 `if` 语句中判断某个条件是否为真或假。
	**标志/状态**：`bool` 常用于表示状态或开关（如是否启用某个功能，是否完成某个操作）。
	 **返回值**：许多 Qt 函数返回 `bool` 类型值，用来指示操作是否成功。例如，`QFile::open()` 函数返回一个 `bool`，表示文件是否成功打开。
3. 使用
	1. 声明bool变量：`bool isConnected = true`;
	2. 在条件语句中使用bool：if (isConnected) { // 如果 isConnected 为 true，执行这里的代码 qDebug() << "Connection successful!"; } else { // 如果 isConnected 为 false，执行这里的代码 qDebug() << "Connection failed!"; }
	3. 使用bool类型的函数返回值
		1. **QDialog::exec() 函数**：`exec()` 函数返回一个 `int`，通常用于对话框的执行状态，但如果你想使用 `bool` 类型来判断对话框是否成功关闭，你可以做如下判断：QDialog dialog; if (dialog.exec() == QDialog::Accepted) { // 如果对话框返回 Accepted 状态，说明操作成功 qDebug() << "Dialog accepted!"; } else { // 否则，表示对话框取消或关闭 qDebug() << "Dialog rejected!"; }
		2. **QCheckBox**：`QCheckBox` 控件的 `isChecked()` 方法返回一个 `bool` 值，用于表示复选框是否被选中。
			QCheckBox* checkBox = new QCheckBox("Enable Feature");
			if (checkBox->isChecked()) {
			    qDebug() << "Feature enabled!";
			} else {
			    qDebug() << "Feature disabled!";
			}
	4. 与逻辑操作符结合使用
### int head = (mPackHead + 1) % PACK_QUEUE_CNT;
1. **`   mPackHead`** ：整数变量，它通常表示某种队列的**头部位置**，或者某个环形缓冲区的当前头部索引。
2. **`PACK_QUEUE_CNT`** 是一个常量，表示队列或缓冲区的最大容量（即**队列的大小**）。
3. **`(mPackHead + 1)`**：表示将 `mPackHead` 的值加 1。也就是说，计算下一个位置或下一个索引。
4. **`% PACK_QUEUE_CNT`**：这个操作符是取模运算（取余）。`%` 是模运算符，计算 `(mPackHead + 1)` 除以 `PACK_QUEUE_CNT` 的余数。这个操作确保了索引始终在 `0` 到 `PACK_QUEUE_CNT-1` 的范围内，防止超过队列的最大容量，从而实现环形缓冲区的效果。
5. **环形队列的用途：**
	 - 这种写法通常用于**环形队列**或**环形缓冲区**（Circular Buffer）。环形队列是一个在达到最大容量时会重新回到开始的位置的队列。也就是说，当队列的索引达到最大值时，下一次会从索引 0 开始，这样队列的头部和尾部可以循环使用内存空间。
6. **目的：** 确保 `head` 的值始终保持在队列索引的合法范围内，从 `0` 到 `PACK_QUEUE_CNT-1`，从而实现循环队列的效果。
### `tr()` 用于字符串的国际化
### 按位或运算
按位或运算（bitwise OR）是一种对二进制数进行操作的运算方式，它将两个数的每一位进行比较，按照以下规则进行计算：

1.如果两个对应的二进制位中至少有一个是1，结果就为1；
2.如果两个对应的二进制位都是0，结果就为0。

具体的规则可以总结如下：
| A (二进制) | B (二进制) | A | B (按位或运算) |
|------------|------------|-----------------|
| 0          | 0          | 0               |
| 0          | 1          | 1               |
| 1          | 0          | 1               |
| 1          | 1          | 1               |
例子
假设有两个数字 A 和 B，我们想要对它们进行按位或运算。
3.A = 0101 （二进制）
4.B = 1100 （二进制）

按位或运算过程如下：
   A = 0101
   B = 1100
  ------------
A | B = 1101
所以，0101 | 1100 = 1101（结果是1101，即13）。

在代码中的应用
在你给出的代码中，按位或运算是这样使用的：
hr = (ushort)(hr | hrHByte);

假设hr和hrHByte是二进制数，hr和hrHByte的按位或运算会将hr的每一位与hrHByte的相应位进行比较，得出新的hr值。这样做的目的是将hrHByte的高字节放入hr的高位。
### 菜单栏的退出按下槽函数
void MainWindow::menuQuit()
{
    QMessageBox meg(QMessageBox::Question, tr("退出"), tr("是否退出程序？"), NULL);
    QPushButton * okButton = meg.addButton(tr("确定"), QMessageBox::AcceptRole);
    QPushButton * cancelButton = meg.addButton(tr( "取消 "), QMessageBox: :RejectRole);
    meg.exec();
    if((QPushButton* )meg.clickedButton() == okButton)//点击确定
    {
        qDebug() << "Yes";
        QApplication* app;
        app->exit(0);
    }
    else if((QPushButton*)meg.clickedButton() == cancelButton)
    {
        qDebug() << "NO";
    }
}