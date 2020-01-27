Installating rabbitmq-server in Amazon linux 2
 
Step 1. Installing Erlang Version 20.1
Erlang is also a language which needs to be installed. Use the following commands to install Erlang.

cd /opt
wget https://github.com/rabbitmq/erlang-rpm/releases/download/v20.1.7/erlang-20.1.7-1.el6.x86_64.rpm
rpm -ivh erlang-20.1.7-1.el6.x86_64.rpm

Step 2. Installing Socat
This is the package which is needed to install RabbitMQ V 3.7, so install it beforehand with the following command:

yum install socat

Step 3. Installing RabbitMQ v3.7.0
So now the ground is ready to install the RabbitMQ server. Use the following commands to proceed:

wget https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.0/rabbitmq-server-3.7.0-1.el6.noarch.rpm
rpm -ivhrabbitmq-server-3.7.0-1.el6.noarch.rpm
service rabbitmq-server start
chkconfigrabbitmq-server on
cd /usr/lib/rabbitmq/bin/
rabbitmq-plugins enable rabbitmq_management
cd /etc/rabbitmq/
vim rabbitmq.config
[{rabbit, [{tcp_listeners, [{"", 5672}]},{loopback_users, []}]}].
Esc+:wq! (To save file and exit editor)

Now you can access RabbitMQ on the browser using:

http://<IP_Of_Your_AWS_Machine>:15672/

chown -R rabbitmq:rabbitmq /var/lib/rabbitmq/ 
rabbitmqctl add_user admin mqadmin 
rabbitmqctl set_user_tags admin administrator
rabbitmqctl set_permissions -p / admin " .*"  " .*"  " .*"
