<h1>Thrift连接池实现</h1>

目标：<br/>
  1、支持池化管理thrift客户端连接<br/>
  2、支持thrift服务器的负载均衡<br/>
  3、支持thrift服务器列表的动态管理<br/>

<h1>示例</h1>

	ThriftConnectionPoolConfig config = new ThriftConnectionPoolConfig();
	config.setConnectTimeout(3000);
	config.setThriftProtocol(TProtocolType.BINARY);
	config.setClientClass(Example.Client.class);
	config.addThriftServer("127.0.0.1", 9119);
	config.setMaxConnectionPerServer(2);
	config.setMinConnectionPerServer(1);
	config.setIdleMaxAge(2, TimeUnit.SECONDS);
	config.setMaxConnectionAge(2);
	config.setLazyInit(false);
	try {
		ThriftConnectionPool<Example.Client> pool = new ThriftConnectionPool<Example.Client>(config);
		Example.Client client = pool.getConnection().getClient();
		client.ping();
		pool.close();
	} catch (ThriftConnectionPoolException e) {
		e.printStackTrace();
	} catch (TException e) {
		e.printStackTrace();
	} catch (IOException e) {
		e.printStackTrace();
	}

<h1>使用</h1>
	maven中央仓库发布审核中。。。

<h1>特性</h1>	
  1、支持服务器之间的负载均衡<br/>
  2、每个服务器拥有一个独立的连接分区 所有的连接分区合并一起为整个连接池<br/>
  3、连接池支持自动创建连接、管理超时连接、管理失效连接<br/>
  4、支持服务器列表动态增加或者移除

<h1>接下来需要完善内容：</h1>
 1、建议使用者添加ping方法检测连接<br/>
 2、代码格式整理<br/>
 3、补充文档<br/>
 4、补充性能测试<br/>


