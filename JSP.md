sun公司制定的一种服务器端动态页面技术规范。
jsp其实是一个以".jsp"的后缀的文件，该文件的内容主要是html和少量的java代码，容器会将jsp文件自动转换成一个Servlet然后执行。

# 如何写一个jsp文件
### step1，创建一个以".jsp"为后缀的文件。
### step2，在文件里面，添加如下的内容：
##### (1)html（css,js）：直接写。
##### (2)java代码：
1)java代码片段

     <% java语句;%>
2)jsp表达式

     <%= java表达式%>
     
# 隐含对象
    1）什么是隐含对象？
    在jsp文件里面，可以直接使用的对象，比如
    out.request,reponse.
    2)为什么可以直接使用这些隐含对象？
    容器会自动生成获得这些对象的代码。
 ### JSP页面中的隐含对象
 
                隐含对象          类型                  说明
                request       HttpServletRequest       请求信息
                response      HttpServletResponse      响应信息
                out           JSPWriter（PrinterWriter）输出的数据流
                session       HttpSession              会话
                application   ServletContext           全局的上下文对象
                pageContext   PageContext              JSP页面上下文
                page          Object                   JSP页面本身
                config        ServletConfig            Servlet配置对象
                exception     Throwable                捕获页面异常

 # 指令
    1）什么是指令？
    通知容器，在将jsp文件展缓成servlet类时，做一些额外的处理，比如包
    2）指令的语法
    <%@指令名称 属性=属性值%>
    3）page指令
      a,import属性：导包
      比如<%@page import="java.utl.*"%>
      b,contentType属性：设置
      response.setContentType的内容。
      c，pageEncoding属性：告诉容器jsp文件的编码。
      （有些容器在读取jsp文件时，默认为按照ISO8859-1解码，如果jsp文件里面包含了中文，会出现乱码）。
   
     <%@page %>
     <%@page contentType="text/html;charset=utf-8"%>
     <%@page
     pageEncoding="utf-8" 
     %>
    
 # jsp是如何执行的？
 ### step1，容器将jsp文件转换成一个servlet类
 
     html(css,js)------------->service方法里，使用out.write输出。
     <%java语句;>-------------->service方法里，照搬。
     <%=java表达式%>------------>service方法里，使用out.print()输出。

 ### step2，容器调用servlet

##### <!DOCYPE>文件头用于验证网页的合法与标准性
#### IE浏览器 如果没有DOCTYPE 会自动降级例如IE6——>IE5

     1>HttpServlet
     service()
     {

     }
     2>HttpJspBase extends HttpServlet
     service()
     {
      _jspService()
     {
       };
     }
     3>自定义类 extends HttpJspBase
     {
       @override
       _jspService()
       {
       }
     }
