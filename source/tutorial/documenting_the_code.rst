Documenting the code
====================

``doxygen``\ 提取源代码中的*comment block*, 根据这些*comment block*生成文档, 
所以我们需要知道应该如何正确的为源代码添加符合doxygen要求的注释.


Specail comment blocks
-----------------------

A special comment is a C or C++ style comment block with some addtional marking, 
so doxygen knows it is a piece of structural text that need to end up in the generated documentation.


Comment blocks for C-like languages
-------------------------------------------------------------------

几种不同风格的文档注释块
^^^^^^^^^^^^^^^^^^^^^^^^
在源代码中, 可以使用几种不同风格的注释: JavaDoc style, Qt style, 单行注释风格.

* JavaDoc style

::

    /**
     *  ... text ...
     */


* Qt style

::

    /*!
     *  ... text ...
     */

* 单行注释风格
  单行注释风格的文档注释块，至少要两行.

::

    ///
    /// ... text ...
    ///

or

::

    //!
    //! ... text ...
    //!

Unlike most other documentation systems, doxygen also allow you to put the documentation of members(including global functions) in front of the definiton. 
This way the documentation can be placed in the source file instead of the header file. 
This keeps the header file compact, and allows the implementer of the members more direct access to the documentaiton. 
As a compromise the brief description could be placed before the declaration and the detailed description before the member definiton.

Putting documentation after members
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you want to document the members of a file, struct, union, class or enum, 
it is sometimes desired to place the documentation block after the member instead of before. 
For this purpose you have to put an addtional ``<`` marker in the comment block.

::
    
    对于变量, 枚举成员, 结构体成员, 类成员和函数参数, 还可以将文档注释放在紧接其后的位置.
    将文档注释块放在紧接其后的位置,通常只做描述性的注释, brief descripiton or detailed description.
    brief description - 使用一行单行注释
    detailed description - 至少两行单行注释或块注释

Here are some examples::

    int var1; /*!< Detailed description after the member */

    int var2; /**< Detailed description after the member */

    # 单行注释风格的文档注释块, detailed description至少要有两行
    int var3; //!< Detailed description after the member
              //!<

    int var4; ///< Detailed description after the member
              ///<

Most after one only wants to put a brief description after a member. 
This is done as follows::

    int var1; ///< Brief description after the member

    int var2; //!< Brief description after the member

Documentation at other places
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
通常, 我们将文档注释块放在被注释的对象的前面后紧接其后, 但doxygen允许我们将文档注释块放在任意位置.
虽然doxygen允许我们这么做, 但除非确实需要, 还是最好将其放在靠近被注释的对象的位置.


Comment blocks in Python
-------------------------

Python有自己的文档注释标准, 对于Python代码:
    * 使用 ``'''`` 注释
        **Note that in this case none of doxygen's special commands are supported.**
    * 使用 ``#`` 注释
        * 文档注释块的开头使用 ``##``;
        * Support doxygen's special commands.

