快速开始（管理员）
========================================

创建团队
---------
注册成功之后，点击 ``创建团队`` Tab，填入自己团队的名称之后点击 ``创建团队`` 按钮。

.. image:: /_static/quickstart-leader/create-team.png

创建项目
---------
点击顶部菜单 ``项目``，点击 ``创建项目``。

Git仓库并不是必填，可以先略过，将 ``使用 Git 仓库`` 前的勾去掉。

选择一个足够强壮的字符串作为口令。

.. image:: /_static/quickstart-leader/create-project.png

.. note:: 项目在创建的时候会生成两对 RSA 密钥对，其中一对的 passphrase 就是创建项目时输入的口令，这对密钥对称为 ``加密密钥对``，另外一对密钥对用于 SSH 登录用户的服务器，称为 ``SSH 密钥对``，用户需要将 SSH 密钥对的公钥部署到服务器上以供 Web Deployer 执行部署任务。``SSH 密钥对`` 的私钥在存入数据库之前会被 ``加密密钥对`` 加密，只有用户提供了正确的口令才能将密文还原为正确的 RSA 私钥，也就说即使黑客获取到用户在 Web Deployer 的账号密码或者获得 Web Deployer 数据库权限，在没有口令的情况下也无法还原出 RSA 私钥。

添加服务器
----------
点击顶部菜单 ``服务器``。

点击第一个面板的右上角的 ``添加`` 按钮。

选择一个直观的服务器名称，比如 ``web-server-01``；IP/Hostname 必须是一个可以被外网访问到的 ip 或者域名；SSH 端口通常是22保持默认即可；登录用户填写 SSH 登录用户，不推荐使用 ``root``；中转服务器可不填；标签可以根据该服务器的属性填写，可以多个，如 ``web``、``db``。

点击保存。

.. image:: /_static/quickstart-leader/create-server.png

服务器配置 ssh 信任密钥
------------------------
点击顶部菜单 ``项目``，点击刚刚创建的项目。

点击右上角的 ``查看部署公钥`` 按钮，复制弹框中的文本，追加到服务器的 ``/{用户家目录}/.ssh/authorized_keys`` 文件末尾，注意这里的用户必须和添加服务器时填入的用户一致。

具体配置细节可以搜索 ``SSH 信任`` 查找相关技术文章。

.. image:: /_static/quickstart-leader/show-pubkey.png

Hello World
-------------
进入项目页面，点击 ``脚本`` Tab，点击右边的 ``添加`` 按钮。

名称和描述都填 ``Hello World Task``，类型选择 ``shell脚本``，脚本里填入一行 ``echo 'Hello World'``，点击保存。

.. image:: /_static/quickstart-leader/create-task.png

点击 ``工作流`` Tab，点击 ``添加`` 按钮。

填入名称 ``Hello World Flow`` 并保存。

在工作流列表里可以看到刚刚添加的 ``Hello World Flow`` 工作流，点击 ``编辑流程``。

.. image:: /_static/quickstart-leader/flow-created.png

在弹出的新窗口中，点击 ``添加子流程``。

在下方的表单中，基本信息面板的名称填入 ``echo``，类型保持 ``执行任务`` 不变；在 ``任务`` 面板中选中 ``Hello World Task``，点击 ``选择`` 按钮；在 ``执行服务器`` 面板的 ``服务器`` 选择之前添加好的服务器。点击保存。

.. image:: /_static/quickstart-leader/create-subflow.png

回到项目页面，点击 ``工作流`` Tab，此时可以看到 ``Hello World Flow`` 工作流的流程数为1，并且 ``发起部署`` 按钮为可点击状态，点击 ``发起部署`` 按钮。

.. image:: /_static/quickstart-leader/create-deployment.png

在弹出的新页面中可以看到部署的具体输入和输出。

.. image:: /_static/quickstart-leader/show-deployment.png
