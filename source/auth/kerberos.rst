Kerberos
========================================

简介
----------------------------------------
简单地说，Kerberos提供了一种单点登录(SSO)的方法。考虑这样一个场景，在一个网络中有不同的服务器，比如，打印服务器、邮件服务器和文件服务器。这些服务器都有认证的需求。很自然的，不可能让每个服务器自己实现一套认证系统，而是提供一个中心认证服务器（AS-Authentication Server）供这些服务器使用。这样任何客户端就只需维护一个密码就能登录所有服务器。

因此，在Kerberos系统中至少有三个角色：认证服务器（AS），客户端（Client）和普通服务器（Server）。客户端和服务器将在AS的帮助下完成相互认证。
在Kerberos系统中，客户端和服务器都有一个唯一的名字，叫做Principal。同时，客户端和服务器都有自己的密码，并且它们的密码只有自己和认证服务器AS知道。

简化的认证过程
----------------------------------------
1. 客户端向服务器发起请求，请求内容是：客户端的principal，服务器的principal
2. AS收到请求之后，随机生成一个密码Kc, s(session key), 并生成以下两个票据返回给客户端
    1. 给客户端的票据，用客户端的密码加密，内容为随机密码，session，server_principal
    2. 给服务器端的票据，用服务器的密码加密，内容为随机密码，session，client_principal
3. 客户端拿到了第二步中的两个票据后，首先用自己的密码解开票据，得到Kc、s，然后生成一个Authenticator，其中主要包括当前时间和Ts,c的校验码，并且用SessionKey Kc,s加密。之后客户端将Authenticator和给server的票据同时发给服务器
4. 服务器首先用自己的密码解开票据，拿到SessionKey Kc,s，然后用Kc,s解开Authenticator，并做如下检查
    1. 检查Authenticator中的时间戳是不是在当前时间上下5分钟以内，并且检查该时间戳是否首次出现。如果该时间戳不是第一次出现，那说明有人截获了之前客户端发送的内容，进行Replay攻击。
    2. 检查checksum是否正确
    3. 如果都正确，客户端就通过了认证
5. 服务器段可选择性地给客户端回复一条消息来完成双向认证，内容为用session key加密的时间戳
6. 客户端通过解开消息，比较发回的时间戳和自己发送的时间戳是否一致，来验证服务器

完整的认证过程
----------------------------------------
上方介绍的流程已经能够完成客户端和服务器的相互认证。但是，比较不方便的是每次认证都需要客户端输入自己的密码。

因此在Kerberos系统中，引入了一个新的角色叫做：票据授权服务(TGS - Ticket Granting Service)，它的地位类似于一个普通的服务器，只是它提供的服务是为客户端发放用于和其他服务器认证的票据。

这样，Kerberos系统中就有四个角色：认证服务器（AS），客户端（Client），普通服务器（Server）和票据授权服务（TGS）。这样客户端初次和服务器通信的认证流程分成了以下6个步骤：

1. 客户端向AS发起请求，请求内容是：客户端的principal，票据授权服务器的rincipal
2. AS收到请求之后，随机生成一个密码Kc, s(session key), 并生成以下两个票据返回给客户端：
    1. 给客户端的票据，用客户端的密码加密，内容为随机密码，session，tgs_principal
    2. 给tgs的票据，用tgs的密码加密，内容为随机密码，session，client_principal
3. 客户端拿到了第二步中的两个票据后，首先用自己的密码解开票据，得到Kc、s，然后生成一个Authenticator，其中主要包括当前时间和Ts,c的校验码，并且用SessionKey Kc,s加密。之后客户端向tgs发起请求，内容包括:
    1. Authenticator
    2. 给tgs的票据同时发给服务器
    3. server_principal
4. TGS首先用自己的密码解开票据，拿到SessionKey Kc,s，然后用Kc,s解开Authenticator，并做如下检查
    1. 检查Authenticator中的时间戳是不是在当前时间上下5分钟以内，并且检查该时间戳是否首次出现。如果该时间戳不是第一次出现，那说明有人截获了之前客户端发送的内容，进行Replay攻击。
    2. 检查checksum是否正确
    3. 如果都正确，客户端就通过了认证
5. tgs生成一个session key组装两个票据给客户端
    1. 用客户端和tgs的session key加密的票据，包含新生成的session key和server_principal
    2. 用服务器的密码加密的票据，包括新生成的session key和client principal
6. 客户端收到两个票据后，解开自己的，然后生成一个Authenticator，发请求给服务器，内容包括
    1. Authenticator
    2. 给服务器的票据
7. 服务器收到请求后，用自己的密码解开票据，得到session key，然后用session key解开authenticator对可无端进行验证
8. 服务器可以选择返回一个用session key加密的之前的是时间戳来完成双向验证
9. 客户端通过解开消息，比较发回的时间戳和自己发送的时间戳是否一致，来验证服务器

参考链接
----------------------------------------
- `Kerberos认证流程详解 <https://blog.csdn.net/jewes/article/details/20792021>`_
- `Delegate to the Top: Abusing Kerberos for arbitrary impersonations and RCE <https://www.blackhat.com/docs/asia-17/materials/asia-17-Hart-Delegate-To-The-Top-Abusing-Kerberos-For-Arbitrary-Impersonations-And-RCE-wp.pdf>`_
- `Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol <https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-sfu/3bff5864-8135-400e-bdd9-33b552051d94?redirectedfrom=MSDN>`_
