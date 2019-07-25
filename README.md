# eigen3_cmake_module

This package adds a [CMake find module](https://cmake.org/cmake/help/v3.14/manual/cmake-developer.7.html#find-modulesjj) for [Eigen3](https://eigen.tuxfamily.org/dox/) that sets [standard cmake variables](https://cmake.org/cmake/help/v3.5/manual/cmake-developer.7.html#standard-variable-names).
This enables `ament_export_dependencies(Eigen3)` and `ament_target_dependencies(my_target Eigen3)`.

## Using this package

This section assume you're using [ament_cmake](https://github.com/ament/ament_cmake).

### Edit your CMakeLists.txt
In your `CMakeLists.txt`, call `find_package()` on this package using `REQUIRED`; then find `Eigen3`.

```CMake
find_package(eigen3_cmake_module REQUIRED)
find_package(Eigen3)
```

If your library or executable uses `Eigen3`, then call `ament_target_dependencies()` to give it access to the `Eigen3` headers.

```CMake
# add_library(my_thing ...)
# # OR
# add_executable(my_thing ...)
# ...
ament_target_dependencies(my_thing Eigen3)
```

If your package uses Eigen3 in public headers, then call `ament_export_dependencies()` on this package, and afterwards do the same for `Eigen3`.

```CMake
ament_export_dependencies(eigen3_cmake_module)
ament_export_dependencies(Eigen3)
```

### Edit your package.xml

Add build dependencies to both this package and Eigen3 to your `package.xml`.

```xml
<build_depend>eigen3_cmake_module</build_depend>
<build_depend>Eigen3</build_depend>
```

If your package uses Eigen3 in public headers, then **also add** `<build_export_depend>` so downstream packages depend on both this package and `Eigen3`.

```xml
<build_export_depend>eigen3_cmake_module</build_export_depend>
<build_export_depend>Eigen3</build_export_depend>
```

`<run_depend>` are not necessary because `Eigen3` is a header only library.
