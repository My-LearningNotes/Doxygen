`Calling Doxygen from cmake <https://p5r.uk/blog/2014/cmake-doxygen.html>`_
============================================================================

基本思路
--------

在\ ``doc/CMakeLists.txt`` \(也可以是其它路径下的\ ``CMakeLists.txt``\ , 但将文档放在\ ``doc``\ 路径下是一种较好的选择)中或\ ``cmake_modules/UseDoxygen.cmake``\ 中(也可以是其他命名的cmake脚本), 
checks for Doxygen and if found, adds a doc target to the build system
(在项目根路径下的\ ``CMakeLists.txt``\ 文件中包\含\ ``doc/CMakeLists.txt``\ 或\ ``cmake_modules/UseDoxygen.cmake``\ ; 
在构建目录中, 在生成\ ``Makefile``\ 之后, 就可以执行\ ``make doc``\ 来生成API文档).

在项目中需要包含一个\ ``Doxyfile.in``\ 文件, 做为生成\ ``Doxygen``\ 的配置文件\ ``Doxyfile``\ 的模板；
在\ ``Doxyfile.in``\ 文件中, 可以使用cmake中定义的变量, 并在cmake以\ ``Doxyfile.in``\ 为模板生成\ ``Doxyfile``\ 时, 将其中的变量替换为变量的值.

实现
-----
The following ``doc/CMakeLists.txt`` file checks for Doxygen and if found, adds a doc target to the build system.

It also generates a ``doc/Doxygen`` in the build folder, which allows cmake to substitute some variables such as version number, source and destination folder etc.

.. code-block:: cmake

    # add a target to generate API documentation with Doxygen
    find_package(Doxygen)
    option(BUILD_DOCUMENTATION "Create and install the HTML based API documentation(requires Doxygen)" ${DOXYGEN_FOUND})

    if(BUILD_DOCUMENTATION)
        if (NOT DOXYGEN_FOUND)
            message(FATAL_ERROR "Doxygen is needed to build the documentation.")
        endif()

        set(doxyfile_in ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)
        set(doxyfile ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)

        configuration_file(${doxyfile_in} ${doxyfile} @ONLY)

        add_custom_target(doc
            COMMAND ${DOXYGEN_EXECUTABLE} ${doxyfile}
            WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
            COMMENT "Generating API documentation with Doxygen"
            VERBATIM
        )

        install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/html DESTINATION share/doc)
      endif()


This ``doc/Doxyfile.in`` extract shows some example cmake variables used. Other values can be used too.

Since cmake uses the full path names in ``@PROJECT_SOURCE_DIR@``, we have to strip some parts of the path using the ``STRIP_FROM_PATH`` option.

.. code-block:: text

    PROJECT_NAME                            = "@CMAKE_PROJECT_NAME@"
    PROJECT_NUMBER                          = @VERSION_MAJOR@.@VERSION.MINOR@.@VERSION_PATCH@
    STRIP_FROM_PATH                         = @PROJECT_SOURCE_DIR@ \
                                              @PROJECT_BINARY_DIR@
    INPUT                                   = @doxygen main page@ \
                                              @PROJECT_SOURCE_DIR@ \
                                              @PROJECT_BINARY_DIR@
    FILE_PATTERNS                          = *.h \
                                             *.cc
    RECURSIVE                              = YES
    USE_MDFILE_ASMAINPAGE                  = @doxy_main_page@

To change the version number put this in one of your ``CMakeLists.txt`` files:

.. code-block:: cmake
    
    # The project version number.
    set(VERSION_MAJOR 0 CACHE STRING "Project major version number.")
    set(VERSION_MINOR 0 CACHE STRING "Project minor version number.")
    set(VERSION_PATCH 1 CACHE STRING "Project patch verison number.")
    mark_as_advanced(VERSION_MAJOR VERSION_MINOR VERSION_PATCH)

It is easy to extend this to "C/C++" as well. 
Just have a file pre-processed by cmake using the ``configure_file()`` command to generate a ``config.h`` file from a template.

