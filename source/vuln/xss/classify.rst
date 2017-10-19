分类
--------------------------------
反射型XSS
    一次浏览，最常见，最广泛
    e.g ``http://www.baidu.com<script>alert("hack")</script>``
储存型XSS
    危害较大，把相应脚本传到服务器上
DOM XSS
    类似储存型