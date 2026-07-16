# Kingco proxy
將以下兩個設定檔放置於與kingco proxy執行檔相同目錄下

# 設定檔
* `ServiceConfig.json`: proxy服務相關參數配置
* `KingcoConfig.json`: 後台API相關參數配置
# 設定檔配置

### ServiceConfig.json
* kingco proxy只需啟用http service
* ReadTimeoutSecond 、 WriteTimeoutSecond以及IdleTimeoutSecond建議設為60秒
```
{
	"Version":"1.0",
	"Logger":{
		"FileName":"lottery",	//logger file name
		"Level":"info"	 		//default level:"debug", "info", "warning", "error", "panic"
	},
	"Mysql":{
		"Enable":false,  //true=enable, false=disable
		"MainDB":{
			"DriverName":"mysql",
			"DataSourceName":"root:xxxxx@tcp(localhost:3306)/db",  
			"User":"",							
			"Password":"",						
			"Net":"tcp",   						
			"Address":"localhost:3306",		  	
			"DBName":"",						
			"Timeout":"1m2s",
			"ReadTimeout":"2s",
			"WriteTimeout":"2s"
		},
		"ReadWriteSplitting":false,
		"WriteOnlyDB":{
			"DriverName":"mysql",
			"DataSourceName":"root:xxxxx@tcp(localhost:3306)/db",
			"User":"",
			"Password":"",
			"Net":"tcp",
			"Address":"",
			"DBName":"",
			"Timeout":"1m2s",
			"ReadTimeout":"2s",
			"WriteTimeout":"2s"
		}
	},
	"MQ":{
		"Enable":false,
		"Url":"amqp://account:password@localhost:5672/",  
		"ResponseTimeoutSecond":1,
		"QueueParam":{
			"Name":"name",
			"Durable":true,
			"AutoDelete":false,
			"Exclusive":false,
			"NoWaite":false,
			"Args":{}
		},
		"ConsumeParam":{
			"Queue":"queue",
			"Consumer":"consume",
			"AutoAck":false,
			"Exclusive":false,
			"NoLocal":false,
			"NoWaite":false,
			"Args":{}
		},
		"Qos":{
			"PrefetchCount":1,
			"PrefetchSize":0,
			"Global":false
		},
		"QueueDefinition":[
			{"Name":"queue1","Type":0},	// Name quene name, 
										// Type 0= consume command
										// Type 1=consuem response
										// Type 2= other service queue
			{"Name":"queue2","Type":1}
		]
	},
	"HTTP":{
		"Enable":true,                        //true=enable, false=disable
		"Address":"",                         //ip address
		"Port":"20000",                       //ip port
		"ReadTimeoutSecond":60,               //request timeout second
		"WriteTimeoutSecond":60,              //response timeout second
		"IdleTimeoutSecond":60,
		"MaxHeaderBytes":1048576,
		"IsTLS":false,                        //是否有TLS
		"CertificateFile":"lc8168.com.crt",   //TLS憑證
		"KeyFile":"lc8168.com.key"            //TLS私鑰
	},
	"Redis":{
		"Enable":false,                 
		"Network":"tcp",               
		"Address":"localhost:6379",   
		"Password":"",                 
		"DB":0,                        
		"DialTimeoutSecond":5,
		"ReadTimeoutSecond":3,
		"WriteTimeoutSecond":3,
		"PoolSize":10
	}
}
```

### KingcoConfig.json
```
{
	"Version":"1.0",
	"Domain":"test.cc",                                 //會員站點域名
	"ECRMAPIURL":"http://test.net:8888/test-api/",      //後台API URL
	"DefaultMD5Key":"XjvTLI6p0mOQK051",                 //預設MD5 key，用以獲取企業對應的MD5 key
	"DefaultAESKey":"i9Q30JYMf06NmBCJ",                 //預設AES key，用以獲取企業對應的AES key
	"TokenExpireSecond":1800                            //user token的時效
}

```
