Utilization skills
========================================

P/Invoke
----------------------------------------
Platform Invoke (P/Invoke) provides C#'s ability to access data structures, callbacks, and functions in DLLs. The basic usage methods are shown in the official `Platform Invoke <https://docs.microsoft.com/en-us/dotnet/standard/native-interop/pinvoke>`_ documentation. Using the capabilities of P/Invoke, C# programs can easily call standard Windows APIs.

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

The disadvantage of P/Invoke is that the referenced API calls will eventually appear in the IAT of the executable file, making some sensitive behaviors easily noticed by the protection software. At the same time, some sensitive APIs may be monitored by the protection software, and API calls made in this way are also easily intercepted by the protection software.

D/Invoke
----------------------------------------
Based on P/Invoke, some researchers proposed D/Invoke based on the `Delegates <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/`_ mechanism, Call the required API in a more obscure way.
