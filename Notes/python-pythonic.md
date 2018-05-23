## **Python 的Pythonic 规范**

***

1. 包和模块儿的命名采用小写、单数形式，而且短小。
2. 避免只用大小写区分不用的对象。
3. 避免使用容易引起混淆的名称。
4. 即使变量名过长也要保证可读性
5. 符合pep8代码规范
    * pip install -U pep8
    * pep8 --show-source --show-pep8 x.py
    * 自动化pep8格式化工具
        * pip install -U autopep8
        * autopep8 -v --in-place --aggressive --aggressive x.py
            * --in-place: 用修改的文件替换原文件
            * --aggressive: 修复的登记，可以叠加增加等级
            * --select: 选择性的修复，如--select=E40修复E40类型排版错误
