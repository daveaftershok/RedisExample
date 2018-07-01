# RedisExample

This is an example of using Redis in Azure via .net core Web API.

It can be deployed directly to an app service via the publish option in Visual Studio. Once deployed to an app service you will need to create a redis instance in Azure.

Once redis is setup in Azure, get connection details (from the redis instance) and create a App setting. 'CacheConnection' within your app service with value which looks something like this: 

```dave.redis.cache.windows.net,abortConnect=false,ssl=true,password=[Password]```
  
The app uses the connection string in HomeController.cs:

```var lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
{
  string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
  return ConnectionMultiplexer.Connect(cacheConnection);
});
```
