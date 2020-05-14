`Doxygen <http://www.doxygen.nl/>`_ 简介
=========================================

* ``Doxygen``\ 是一个文档自动生成工具, 它能够提取源代码中特定格式的注释，根据配置文件的设置，自动生成API文档;
* The executable ``doxygen`` is the main program that parses the sources and generates the documentation;
* Optionally, the executable ``doxywizard`` can be used, 
  which is a graphical front-end for editing the configuration file that is used by doxygen and for running doxygen in a graphical environment.


安装
----

.. code-block:: sh
    :emphasize-lines: 2, 5

    # 安装doxygen
    sudo apt-get install doxygen

    # 安装doxywizard
    sudo apt-get install doxygen-gui


Doxygen的配置文件
------------------

Doxygen uses a configuration file to determine all of its settings.
Each project should get its own configuration file.

Creating a configuration file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``doxygen -g <config_file>`` 
    Create a template configuration file.
    Where ``<config_file>`` is the name of the configuration file.
    If you omit the file name, a file named **Doxyfile** will be created.

配置文件简介
^^^^^^^^^^^^
doxygen的配置文件的格式是一组 ``tag`` 和 ``value`` 形式的赋值对::

    TAGNAME = VALUE
    TAGNAME = VAULE1 VALUE2 ...

You can probably leave the values of most tags in a generated template configuration file to their default value.  
If you do not wish to edit the configuration file with a text editor, 
you can use ``doxywizard`` to create, read and wirte doxygen configuration files, 
and allows setting configuration options by entering them via dialogs.


Running doxygen
----------------

执行\ ``doxygen``\ 命令, 根据配置文件, 生成文档.

``doxygen``\ 命令的几种用法:
    - ``doxygen <config_file>``
        显式指定配置文件.
    - ``doxygen``
        在当前路径下寻找配置文件.

Depending on your settings doxygen will create ``html``, ``rtf``, ``latex``, ``xml``, ``man``, and/or ``docbook`` directories inside the output directory.


Documenting the sources
-----------------------

If the ``EXTRACT_ALL`` option is set to ``ON`` in the configuration file(the default), the doxygen will only generate documentation for documented entities.
So how do you document these? For members, classes, and namspaces there are basically two options:

    - Place a special documentation block in front of the declaration or defintion of the member, class or namespace. 
      For file, class and namespace members it is also allowed to place the documentation directly after the member.
    - Place s special documentation block somewhere else (another file or another location) and put a structural command in the documentation block. - **Not Recommended**

Files can only be documented using the second option, since there is no way to put a documentation block before a file.
Of course, file members(functions, variables, typedefs, defines) do not need an explicit structural command; 
just putting a special documentation block in front or behind them will work fine.

