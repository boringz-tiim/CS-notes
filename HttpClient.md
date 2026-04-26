# 介绍HttpClient
客户端编程工具包,并且支持HTTP协议最新的版本和建议
## 发送请求步骤：
1. 创建HttpClient对象
2. 创建Http请求对象
3. 调用HttpClient对象的execute()方法发送请求
## 简单案例
```java
//懒得整理了索性都贴过来了，反正注释都写的很明白了
@SpringBootTest
public class HttpClientTest {
    /**
     * 测试通过httpclienct发送GET方式的请求
     */
    @Test
    public void testGET() throws Exception {
        //创建Httpclient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();
        HttpGet httpGet =new HttpGet("http://localhost:8080/user/shop/status");
        CloseableHttpResponse response = httpClient.execute(httpGet);
        //获取服务端返回的状态码，解析返回的数据
        int statusCode = response.getStatusLine().getStatusCode();
        System.out.println("服务器返回的状态码为："+statusCode );

        HttpEntity entity = response.getEntity();
        String body = EntityUtils .toString(entity) ;
        System.out.println("服务器返回的数据"+body);

        //关闭资源
        response .close() ;
        httpClient .close();
    }
    @Test
    public void testPOST() throws Exception {
        //创建httpClint对象
        CloseableHttpClient httpClient = HttpClients.createDefault();
        //创建请求对象
        HttpPost httpPost=new HttpPost("http://localhost:8080/admin/employee/login");

        //初始化json格式的请求
        JSONObject jsonObject =new JSONObject() ;
        jsonObject.put("username","admin");
        jsonObject.put("password","123456");

        //StringEntity把json对象封装成http请求体
        StringEntity entity =new StringEntity(jsonObject .toString());
        //指定请求编码
        entity.setContentEncoding("utf-8");
        //数据格式
        entity.setContentType("application/json");
        httpPost.setEntity(entity);

        //发送请求
        CloseableHttpResponse response = httpClient.execute(httpPost);

        //解析返回结果
        int statuscode = response .getStatusLine() .getStatusCode() ;
        System.out.println("响应码为:"+statuscode );

        HttpEntity entity1 = response.getEntity();
        String body = EntityUtils.toString(entity1);
        System.out.println("响应数据为："+body);

        //关闭资源
        response .close() ;
        httpClient .close() ;

    }

}
```