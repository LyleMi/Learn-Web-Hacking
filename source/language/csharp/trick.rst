利用技巧
========================================

P/Invoke
----------------------------------------
Platform Invoke (P/Invoke) 提供了C#访问DLL中数据结构、回调、函数的能力。基本的使用方式如官方 `Platform Invoke <https://docs.microsoft.com/en-us/dotnet/standard/native-interop/pinvoke>`_ 文档中所示。利用P/Invoke的能力，C#程序可以较为容易的调用标准的Windows API。

.. code:: csharp

    using System;
    using System.Runtime.InteropServices;

    public class Program
    {
        // Import user32.dll (containing the function we need) and define
        // the method corresponding to the native function.
        [DllImport("user32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
        private static extern int MessageBox(IntPtr hWnd, string lpText, string lpCaption, uint uType);

        public static void Main(string[] args)
        {
            // Invoke the function as a regular managed method.
            MessageBox(IntPtr.Zero, "Command-line message box", "Attention!", 0);
        }
    }

P/Invoke的缺点在于引用了的API调用会最后出现在可执行文件的IAT中，使得一些敏感的行为容易被防护软件所注意。同时一些敏感的API可能是被防护软件所监控的，通过这种方式进行的API调用也容易被防护软件拦截。

D/Invoke
----------------------------------------
在P/Invoke的基础上，有研究人员提出了基于 `Delegates <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/>`_ 机制的D/Invoke，通过更隐蔽的方式来调用所需的API。
