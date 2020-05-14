Doxygen常用指令
================

在源代码的文档注释块中, 可以使用doxygen定义的special commands, 控制doxygen的工作, 比如在文档中生成指定的段落.

* All commands in the documentation starts with a backslash( ``\`` ) or an at-sign( ``@`` );
* Some commands have one or more arguments:

    * argument is a single word(参数是一个单词);
    * argument extends until end of the line on which the command was found(参数是一行);
    * argument extends until the next paragraph(参数是一段).

* Paragraphs are delimited by a blank line or a section indicator;
* 命令都是小写的


常用commands
-------------

控制输出字体
^^^^^^^^^^^^

* ``\a <word>``
    Displays the argument in italics. 
    Use this command to emphasize words. 
    Use this command to refer member arguments in the running text.

* ``\b <word>``
    Display the argument using a bold font.
    To put multiwords in bold use ``<b>multiple words</b>``.

* ``\c <word>``
    Displays the argument using a typewriter font. 
    Use this to refer to a word of code.

生成特定段落
^^^^^^^^^^^^

* ``\author {list of authors}``
    Starts a paragraph where one or more author names may be entered.
    
* ``\brief {brief description}``
    Starts a paragraph that serves as a brief description.

* ``\bug {bug description}``
    Starts a paragraph where one or more bugs may be reported.

* ``\code ['{'<word>'}']``
    * Starts a block of code.
    * 默认情况下, 根据当前所在源文件来推断代码类型; 作为一个可选项, 可以在 ``\code`` 后显式注明代码的文件名后缀, 以此来判断代码的类型(代码类型决定了高亮语法).

    Example::
        
        \code{.py}
        class Python:
            pass
        \endcode

        \code{.cpp}
        class Cpp {};
        \endcode

* ``\copyright {copyright description}``
    Starts a paragraph where the copyright of an entity can be described.

* ``\date {date description}``
    Starts a paragraph where one or more dates may be entered.

* ``\details {detailed descpriton}``
    Just like ``\brief`` starts a brief description, ``details`` starts the detailed description.

* ``\param <param-name> {param description}``
    * Starts a parameter description for a function parameter withe the name, followed by a description of the parameter. 
    * This command has an optional attribute specifying the direction of paramter: ``[in]``, ``[out]``, or ``[in, out]``.

* ``\return {description of the return value}``
    Starts a return value description for a function.

* ``\see {reference}`` or ``\sa {reference}``
    Starts a paragraph where one or more cross-references to classes, funtions, methods, variables, files or URL may be specified.

* ``\todo {paragraph describing what is to be done}``
    Starts a paragraph where a TODO item is described.

* ``\version {version number}``
    Starts a pragraph where one or more version string may be entered.

* ``\waringing {warning message}``
    Starts a paragraph where one or more warning messages may be entered.

