### LNK2019: 无法解析的外部符号 main，函数 WinMain 中引用了该符号
- ==原因==：问题出在CMakeLists文件
	- `add_executable(${PROJECT_NAME} WIN32 ${srcs}` # <--- 问题在这里 )
		- 这行 `aux_source_directory(./src srcs)` 的意思是：**CMake会去查找名为 `src` 的子目录，并将该 `src` 子目录下的所有源文件（`.cpp` 文件）的列表存放到变量 `srcs` 中。**`add_executable` 使用 `${srcs}` 这个变量来获取要编译的源文件列表。
- ==解决==：创建src文件夹，并将main、cpp、h文件移入文件夹
### AutoUic subprocess error；  uic: Error in line 1, column 0 : Premature end of document.
- ==原因==：`MainWindow.ui` 文件损坏或格式无效
- ==解决==：不使用ui文件，完全使用代码进行编译
	- 从 `MainWindow.h` 中移除了 `namespace Ui { class MainWindow; }` 和 `Ui::MainWindow *ui;`。
	- 从 `MainWindow.cpp` 中移除了 `#include "ui_MainWindow.h"`
### .cpp(行,列): error C2352: 'vtkNamedColors::GetColor3d': 调用非静态成员函数需要一个对象
- ==**原因==：** `vtkNamedColors::GetColor3d()` 不是一个静态成员函数。不能直接用类名 `vtkNamedColors::` 来调用它。你需要先创建一个 `vtkNamedColors` 类的实例（对象），然后通过这个对象来调用 `GetColor3d()`。
- ==解决==：
	- 创建实例：vtkNew< vtkNamedColors> colors;
	- 将renderer->SetBackground(vtkNamedColors: :GetColor3d("SlateGray").GetData());改为 renderer->SetBackground(colors->GetColor3d("SlateGray").GetData());
### mocs_compilation_Debug.obj : error LNK2019: 无法解析的外部符号 "private: void __ cdecl MainWindow::onUpdateIsovalue(int)" (?onUpdateIsovalue@MainWindow@@AEAAXH@Z)，函数 "private: static void __ cdecl MainWindow::qt_static_metacall(...)" 中引用了该符号
- ==错误分析==：这个 LNK2019 错误意味着链接器找不到 `MainWindow::onUpdateIsovalue(int)` 这个函数的具体实现代码。
- ==原因==：在h文件声明了槽函数void onUpdateIsovalue(int value);，但是cpp文件中没有提供函数体void MainWindow::onUpdateIsovalue(int value) { ... }。。。。Qt的MOC（元对象编译器）会根据这个声明生成一些代码，这些生成的代码需要链接到 `onUpdateIsovalue` 函数的实际定义。
- ==解决==：为 `onUpdateIsovalue` 添加实现
	- void MainWindow::onUpdateIsovalue(int value) {
		updateMarchingCubes(static_cast< double>(value));
		}
### The program '[21568] MedicalSurfaceRendering.exe' has exited with code -1073741515 (0xc0000135). 在Windows上明确表示为STATUS_DLL_NOT_FOUND：“动态链接库（DLL）未找到”
- ==原因==：运行的环境中缺少Qt和VTK的DLL路径
- ==解决==：修改 `.vscode/launch.json` 文件
	"environment": [
		{
			name": "PATH", "value": "D:/Qt5.15.2/5.15.2/msvc2019_64/bin;D:/VTK9.1/bin;${env:PATH}" 
		}
### ERROR: In xx\ExecutionModel\vtkDemandDrivenPipeline.cxx, line 668 vtkCompositeDataPipeline (0000015D5E118B30): Input port 0 of algorithm vtkMarchingCubes(0000015D5BD44B10) has 0 connections but is not optional.
- ==原因==：VTK在尝试运行Marching Cubes算法时，发现没有给它提供输入数据
### 输出信息出现乱码
==解决==：搜索“区域”→管理→更改系统区域设置→勾选beta版：使用Unicode UTF-8 提供全球语言支持