# CMake 笔记

#### 1.CMake指令备注

```cmake
cmake_minimum_required(VERSION <min>[...<max>] [FATAL_ERROR])
```

用于设置CMake构建需要的最低版本（Releases），同时初始化的CMake策略（policy）设置。<min>和可选的<max>都是**major.minor[.patch[.tweak]]**的格式。

如果使用低于<min>版本的CMake构建项目，则或停止构建并且报错。...可以看做<min>和<max>版本中间版本的省略，在CMake 3.12中被添加，如果低于3.12，则...会被视为版本号分隔符，从而<max>被忽略。

可选的FATAL_ERROR，在CMake 2.6或者更高版本中被忽略，但是如果会使用CMake 2.4或者更低的版本构建项目，则应该指定它，避免在2.4或或者更低的版本仅仅显示一个警告而不是报错。

cmake_minimum_required()应该在顶层CMakeLists.txt中的第一行调用，因为初始化版本和策略设置是非常重要的，避免对其他指令(可能会改变策略行为)造成影响。

cmake_minimum_required()会隐式的调用**cmake_policy(VERSION)**来指定根据给定的CMake版本范围来编写项目构建代码(基于<min>或了<max>,如果指定了<max>)。所有指定版本或更低的CMake策略设置将被设置为NEW，所有高于版本范围的都未设置，从而更新版本中包含的新的策略，将会被警告。

```cmake
cmake_policy(VERSION <min>[...<max>]) # 根据CMake版本进行CMake策略设置
cmake_policy(SET CMP<NNNN> NEW) 			# 明确设置CMP<NNNN>编号的策略为NEW
cmake_policy(SET CMP<NNNN> OLD)				# 明确设置CMP<NNNN>编号的策略为OLD
cmake_policy(GET CMP<NNNN> <variable>)# 获取CMP<NNNN>的值，保存在<variable>中，可以检查策略设置

if(POLICY CMP<NNNN>)		# 用于判断当前CMake版本是否存在指定的policy
endif()
```

CMake策略机制用于保证现有的项目不因为随CMake发展而引入的新策略或者改进的策略而影响。有**NEW**和**OLD**两种提供选择，如果没有指定策略，则CMake会假定为OLD并且产生警告。

CMake策略的**OLD**行为是已决定弃用的行为，获取会被未来的CMake版本删除，因此应该尽量将所有CMake策略都设置为**NEW**，设置为**OLD**的唯一作用仅仅是忽略CMake产生的警告。

CMake策略设置保存在是**栈(stack)**上，因此cmake_policy只能影响栈顶，使用**include()**或者**find_package()**包含进来的CMake策略设置只在被包含的文件中生效，在包含者中是不生效的，除非在**include()**或者**find_package()**显式指明了**NO_POLICY_SCOPE**。

如果在**function()**或者**macro()**中设置了CMake策略，那么该策略设置将自动传播到调用者中。

CMake各个版本的策略代码和说明参见

[cmake_policy]: https://cmake.org/cmake/help/latest/manual/cmake-policies.7.html#manual:cmake-policies(7)

