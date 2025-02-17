## Проблемы

### Boost Filesystem

[Boost Filesystem](https://repo.okbtsp.com/projects/TSPNAVPL/repos/boost-filesystem/browse) после компиляции под новый темплейт не компилируется [TSP-NavigationPlatform-Components](https://repo.okbtsp.com/projects/TSPNAVPL/repos/tsp-navigationplatform-components/browse "TSP-NavigationPlatform-Components"):

```
|   |   |
|---|---|
|14-Feb-2025 13:03:53|In file included from /usr/include/boost/filesystem/path_traits.hpp:22,|
|14-Feb-2025 13:03:53|from /root/.conan/data/Boost-FileSystem/2.0.1/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include/Boost-FileSystem/boost/filesystem/path.hpp:25,|
|14-Feb-2025 13:03:53|from /home/bamboo/bamboo-agent-home/xml-data/build-dir/GLOBALNAVIGATIONPROJECTS-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892A2-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892ABUILDQT512/TSP-NavigationPlatform-Components/SimpleFileCommander/FileSystemOperations/CopyFunctor.cpp:8:|
|14-Feb-2025 13:03:53|/usr/include/boost/system/error_code.hpp:45:26: error: redefinition of ‘struct boost::system::is_error_code_enum<T>’|
|14-Feb-2025 13:03:53|45 \| template<class T> struct is_error_code_enum|
|14-Feb-2025 13:03:53|\|                          ^~~~~~~~~~~~~~~~~~|
|14-Feb-2025 13:03:53|In file included from /home/bamboo/bamboo-agent-home/xml-data/build-dir/GLOBALNAVIGATIONPROJECTS-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892A2-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892ABUILDQT512/TSP-NavigationPlatform-Components/SimpleFileCommander/FileSystemOperations/CopyFunctor.cpp:7:|
|14-Feb-2025 13:03:53|/root/.conan/data/Boost-FileSystem/2.0.1/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include/Boost-FileSystem/boost/system/error_code.hpp:54:12: note: previous definition of ‘struct boost::system::is_error_code_enum<T>’|
|14-Feb-2025 13:03:53|54 \|     struct is_error_code_enum { static const bool value = false; };|
|14-Feb-2025 13:03:53|\|            ^~~~~~~~~~~~~~~~~~|
|14-Feb-2025 13:03:53|In file included from /usr/include/boost/filesystem/path_traits.hpp:22,|
|14-Feb-2025 13:03:53|from /root/.conan/data/Boost-FileSystem/2.0.1/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include/Boost-FileSystem/boost/filesystem/path.hpp:25,|
|14-Feb-2025 13:03:53|from /home/bamboo/bamboo-agent-home/xml-data/build-dir/GLOBALNAVIGATIONPROJECTS-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892A2-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892ABUILDQT512/TSP-NavigationPlatform-Components/SimpleFileCommander/FileSystemOperations/CopyFunctor.cpp:8:|
|14-Feb-2025 13:03:53|/usr/include/boost/system/error_code.hpp:50:26: error: redefinition of ‘struct boost::system::is_error_condition_enum<T>’|
|14-Feb-2025 13:03:53|50 \| template<class T> struct is_error_condition_enum|
|14-Feb-2025 13:03:53|\|                          ^~~~~~~~~~~~~~~~~~~~~~~|
|14-Feb-2025 13:03:53|In file included from /home/bamboo/bamboo-agent-home/xml-data/build-dir/GLOBALNAVIGATIONPROJECTS-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892A2-TSPNAVPLTSPCMPNTE66694FFAAAD332C354D197E2EBF892ABUILDQT512/TSP-NavigationPlatform-Components/SimpleFileCommander/FileSystemOperations/CopyFunctor.cpp:7:|
|14-Feb-2025 13:03:53|/root/.conan/data/Boost-FileSystem/2.0.1/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include/Boost-FileSystem/boost/system/error_code.hpp:57:12: note: previous definition of ‘struct boost::system::is_error_condition_enum<T>’|
|14-Feb-2025 13:03:53|57 \|     struct is_error_condition_enum { static const bool value = false; };|
|14-Feb-2025 13:03:53|\|            ^~~~~~~~~~~~~~~~~~~~~~~|
```

Для подробного вывода команды компиляции выполняем:

```bash
cmake -DCMAKE_VERBOSE_MAKEFILE=ON ..
```

При вербозном выполнениии `make`:

```
cd
/work/Projects/tsp-navigationplatform-components/build/TSP-NavigationPlatform-Components
&&
/usr/bin/c++

-DPROD_NAME=\"TSP-NavigationPlatform-Components\"
-DPROD_VERSION=\"3.0.0\"
-DQT_CORE_LIB
-DQT_GUI_LIB
-DQT_NETWORK_LIB
-DQT_NO_DEBUG
-DQT_WIDGETS_LIB
-DQT_XML_LIB
-DTSPNAVIGATIONPLATFORMCOMPONENTS_LIBRARY
-DTSP_NavigationPlatform_Components_EXPORTS
-I/work/Projects/tsp-navigationplatform-components/build/TSP-NavigationPlatform-Components
-I/work/Projects/tsp-navigationplatform-components/TSP-NavigationPlatform-Components
-I/work/Projects/tsp-navigationplatform-components/build/TSP-NavigationPlatform-Components/TSP-NavigationPlatform-Components_autogen/include
-I/home/vladislav/.conan/data/TSP-GIS-RoutesSearch/9.0.1/_/_/package/68ab4dd3fbe8fad1280d71730a4bc2874673d999/include


-I/home/vladislav/.conan/data/Boost-FileSystem/2.0.1/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include


-I/home/vladislav/.conan/data/TSP-Navigation-Base/1.0.0/_/_/package/1aa5df37877e9ce026aa8f273743b5480ff0e412/include
-I/home/vladislav/.conan/data/TSP-MapWidget-StandardUi-Components/9.0.1/_/_/package/7d599f03f796345b7f613bbc32669c8e3710f8c0/include
-I/home/vladislav/.conan/data/TSP-GIS-Library/9.0.2/_/_/package/838cccccbf46b600b00a1a8bbf70e51f4173c5f5/include
-I/home/vladislav/.conan/data/TSP-DP-GrabberWidgets/10.0.2/_/_/package/ffb32b0733b9e38df5e42c8bbb2e78253e33ca56/include
-I/home/vladislav/.conan/data/TSP-MapWidget-Components-Types/5.0.1/_/_/package/1550ecc7aaf324726c50871f25c32838707f9ffd/include
-I/home/vladislav/.conan/data/TSP-DP-FS-Utils/2.0.0/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include
-I/home/vladislav/.conan/data/TSP-GIS-DriverInterfaces/5.0.1/_/_/package/42d8f5dda62da2155723ec180c520f9e683ca219/include
-I/home/vladislav/.conan/data/TSP-DP-Widgets/10.0.3/_/_/package/afbac51d9ccc075c33d7ee4230ebf7979373dc9d/include
-I/home/vladislav/.conan/data/TSP-MapMarkers-Base/2.0.2/_/_/package/3579aa88ce32ca2f7f5a0d40e1a815eb1ad6dfd1/include
-I/home/vladislav/.conan/data/TSP-MapWidget-CAPI-Base/4.0.1/_/_/package/7203e993359e5064b18fca753883ef8b62ed1b9a/include
-I/home/vladislav/.conan/data/TSP-MapWidget-GIS-Base/6.0.1/_/_/package/87271366dc1bfd3f9c07efa97b7532459aa695e9/include
-I/home/vladislav/.conan/data/TSP-MapWidget-Base/2.0.0/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include
-I/home/vladislav/.conan/data/TSP-MapWidget-Scenery-Types/5.0.1/_/_/package/ced31de303c09acab7e5ef748c762c03802ea66e/include
-I/home/vladislav/.conan/data/TSP-DP-Types/3.0.4/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include
-I/home/vladislav/.conan/data/TSP-GIS-Classes/4.0.1/_/_/package/2463307f19e721f738c49afcff75d6faaa22eca2/include
-I/home/vladislav/.conan/data/TSP-DPI-Helper/2.0.2/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include
-I/home/vladislav/.conan/data/TSP-DP-Utils/6.0.0/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include
-I/home/vladislav/.conan/data/TSP-MapMarkers-Types/2.0.1/_/_/package/87271366dc1bfd3f9c07efa97b7532459aa695e9/include
-I/home/vladislav/.conan/data/TSP-GIS-Math/4.0.2/_/_/package/87271366dc1bfd3f9c07efa97b7532459aa695e9/include
-I/home/vladislav/.conan/data/TSP-GIS-Types/4.0.1/_/_/package/b876cfd9ea60d197bac76ec0e5d753055319bb8d/include
-I/home/vladislav/.conan/data/TSP-DP-MetricsStrings/2.0.1/_/_/package/08bdb3b18ee11ecca36bc3c027e055b81a6e5e0f/include
-I/home/vladislav/.conan/data/TSP-DP-Localization/3.0.1/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include
-I/work/Projects/tsp-navigationplatform-components/TSP-NavigationPlatform-Components/TSP-NavigationPlatform-Components
-I/work/Projects/tsp-navigationplatform-components/TSP-NavigationPlatform-Components/GUI
-I/work/Projects/tsp-navigationplatform-components/TSP-NavigationPlatform-Components/GUI/Calendar
-I/work/Projects/tsp-navigationplatform-components/Utils
-I/work/Projects/tsp-navigationplatform-components/TSP-NavigationPlatform-Components/SimpleFileCommander
-I/work/Projects/tsp-navigationplatform-components


-I/work/Projects/tsp-navigationplatform-components/build/include/Boost-FileSystem
-isystem


/usr/include/x86_64-linux-gnu/qt5
-isystem
/usr/include/x86_64-linux-gnu/qt5/QtCore
-isystem
/usr/lib/x86_64-linux-gnu/qt5/mkspecs/linux-g++
-isystem
/usr/include/x86_64-linux-gnu/qt5/QtGui
-isystem
/usr/include/x86_64-linux-gnu/qt5/QtWidgets
-isystem
/usr/include/x86_64-linux-gnu/qt5/QtXml
-isystem
/usr/include/x86_64-linux-gnu/qt5/QtNetwork

-O3
-DNDEBUG

-fPIC
-fvisibility=hidden
-fvisibility-inlines-hidden


-fPIC
-std=gnu++17
-o
CMakeFiles/TSP-NavigationPlatform-Components.dir/SimpleFileCommander/FileSystemOperations/CopyFunctor.cpp.o
-c
/work/Projects/tsp-navigationplatform-components/TSP-NavigationPlatform-Components/SimpleFileCommander/FileSystemOperations/CopyFunctor.cpp
```

Для `Boost-Filesystem` добавляются 2 инклудпаса:
- `-I/home/vladislav/.conan/data/Boost-FileSystem/2.0.1/_/_/package/0eb1462ccfa2af6c7935218e2255cf2163c2d34b/include`
- `-I/work/Projects/tsp-navigationplatform-components/build/include/Boost-FileSystem-isystem`

Происходит из-за строки `target_include_directories(${CONAN_PACKAGE_NAME} PUBLIC ${CMAKE_BINARY_DIR}/include/Boost-FileSystem)` в `./TSP-NavigationPlatform-Components/CMakeLists.txt`. Удаление этой строки проблему **НЕ РЕШИЛО**, хотя двойной инклудпас пропал
