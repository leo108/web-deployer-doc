任务脚本
==========

Shell 脚本
-----------
Shell 脚本的代码会直接在目标服务器上执行，代码中被 ``{{ }}`` 包裹起来的会被自动替换为环境变量。

假设我们定义了一个名为 ``deploy_path`` 值为 ``/home/www/website`` 的环境变量，那么如下代码::

    cd {{ deploy_path }}

实际上执行的是::

	cd /home/www/website

PHP 脚本
---------
PHP 脚本的 PHP 代码是在 Web Deployer 的 docker 容器中执行的，通过 PHP 的 ``run`` 函数在目标服务器上执行 Shell 命令，如::

	run('cd {{deploy_path}}');

实际上执行的是::

	cd /home/www/website

Web Deployer 提供了一些 PHP 函数来方便部署：

1. run::
	
	run(string $command): string

run 函数用于在目标服务器上执行命令，传入的 ``$command`` 变量里的 ``{{ }}`` 会被自动替换为对应的环境变量。返回值是该命令的输出。


2. cd::

	cd(string $path)

cd 函数的作用是切换当前工作目录，等效于 ``run("cd $path")``

3. test::

	test(string $command): bool

test 函数可以在服务器上执行 test 命令并将结果以 PHP 布尔值的形式返回，如::

	if (!test('[ -d {{release_path}} ]')) {
		run('mkdir -p {{release_path}}');
	}

4. write::

	write(string $message)

write 函数将 ``$message`` 变量输出到标准输出，同时变量里的 ``{{ }}`` 会被自动替换为对应的环境变量。

5. writeln::

	writeln(string $message)

writeln 函数与 write 函数类似，但是会在末尾自动追加一个换行。

6. get::

	get(string $env, $default = null)

get 函数的作用是读取环境变量，第一个参数是环境变量名，第二个参数代表默认值。如果我们没有定义对应的环境变量并且没有传入第二个参数，则系统会认为该任务执行失败。

7. set::

	set(string $name, $value)

set 函数用于动态改变环境变量的值。

8. has::

	has(string $name): bool

has 函数用于判断指定的环境变量是否存在。

9. commandExist::

	commandExist(string $command): bool

commandExist 函数用于判断目标服务器上是否存在指定的命令。
