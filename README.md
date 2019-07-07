#ezserver
一句话构建服务端与客户端

服务端

// 创建一个HTTP服务端
ezserver.HTTP_Server_Start((string rawURL, string postContent) => { return "Hello World"; },8085);

// 创建一个TCP Socket 服务端
ezserver.TCP_Server_Start((string clientID)=> { /* On Connect */ },(string clientID, string receivedStr) => { /* On Received */ return "got it"; }, 8084);

// 创建一个UDP Socket 服务端
ezserver.UDP_Server_Start((System.Net.EndPoint endPoint, string receivedStr) => { return "git it"; }, 8083);


客户端

// 创建一个HTTP客户端
ezserver.HTTP_Request_GET("http://127.0.0.1", (string data) => { } );

// 创建一个TCP客户端
ezserver.TCP_Client_Start("127.0.0.1", 8084, (string receivedStr) => { return "got it"; });

// 发送一条UDP消息（不需要创建客户端）
ezserver.UDP_Send(new System.Net.IPEndPoint(System.Net.IPAddress.Parse("127.0.0.1"), 8083), "hello");


小工具

// 获取本地IP
string[] myIp = Tools.NetWorkTools.GetLocalIP();

// 正则匹配 
// 示例：爬取页面内所有图片
ezserver.HTTP_Request_GET("http://example.com", (string html) => {
      foreach (var item in Tools.RegEx.FindAll(html, "<img src=\"", "\"", false)){
            Console.WriteLine(item);}});
