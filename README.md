# dotnet-etcd
A C# .NET (dotnet) GRPC client for etcd v3+

![Nuget Version Info](https://img.shields.io/nuget/v/dotnet-etcd.svg)
![Nuget Download Info](https://img.shields.io/nuget/dt/dotnet-etcd.svg)

## Installing Package
Nuget package is published on [nuget.org](https://www.nuget.org/packages/dotnet-etcd/) and can be installed in the following ways :
    
### Nuget Package Manager
    
    Install-Package dotnet-etcd -Version 1.0.0	

### .NET CLI
    
    dotnet add package dotnet-etcd --version 1.0.0	

### Paket CLI
    
    paket add dotnet-etcd --version 1.0.0	
` The NuGet Team does not provide support for this client. Please contact its maintainers for support.`

## Usage :

Add using statement at the top of your class file

    using dotnet_etcd;

### Client Initialization

#### No Basic auth or SSL
    
    EtcdClient client = new EtcdClient(<HOSTNAME_STRING>, <PORTNO_INT>);
    // E.g.
    EtcdClient client = new EtcdClient("127.0.0.1", 2379);

#### SSL but no basic auth
    
    EtcdClient client = new EtcdClient(<HOSTNAME_STRING>, <PORTNO_INT>,<CERTIFCATE_STRING>);
    // E.g.
    EtcdClient client = new EtcdClient("127.0.0.1", 2379,File.ReadAllText("/path/to/cert"));

#### Basic auth but no SSL

    EtcdClient client = new EtcdClient(<HOSTNAME_STRING>, <PORTNO_INT>,<USERNAME_STRING>,<PASSWORD_STRING>);
    // E.g.
    EtcdClient client = new EtcdClient("127.0.0.1", 2379,"sr","@hV:%f%xU+2m4~?K");

#### Basic auth and SSL
    
    EtcdClient client = new EtcdClient(<HOSTNAME_STRING>, <PORTNO_INT>,<USERNAME_STRING>,<PASSWORD_STRING>,<CERT_STRING>);
    // E.g.
    EtcdClient client = new EtcdClient("127.0.0.1", 2379,"sr","@hV:%f%xU+2m4~?K",File.ReadAllText("/path/to/cert"));

### Operations
#### Put a key

    client.Put(<KEY_STRING>,<VALUE_STRING>);
    // E.g Put key "foo/bar" with value "foobar"
    client.Put("foo/bar","barfoo");

    await client.PutAsync(<KEY_STRING>,<VALUE_STRING>);
    // E.g Put key "foo/bar" with value "foobar" in async
    await client.PutAsync("foo/bar","barfoo");

#### Get a key
    
    client.Get(<KEY_STRING>);
    // E.g Get key "foo/bar"
    client.Get("foo/bar");

    await client.GetAsync(<KEY_STRING>);
    // E.g. Get key "foo/bar" in async
    await client.GetAsync("foo/bar");

#### Get multiple keys with a common prefix

    client.GetRange(<PREFIX_STRING>);
    // E.g. Get all keys with pattern "foo/*"
    client.GetRange("foo/"); 

    await client.GetRangeAsync(<PREFIX_STRING>);
    // E.g. Get all keys with pattern "foo/*" in async
    await client.GetRangeAsync("foo/");

#### Delete a key

    client.Delete(<KEY_STRING>);
    // E.g. Delete key "foo/bar"
    client.Delete("foo/bar");

    await client.DeleteAsync(<KEY_STRING>);
    // E.g. Delete key "foo/bar" in async
    await client.DeleteAsync("foo/bar");

#### Delete multiple keys with a common prefix

    client.DeleteRange(<PREFIX_STRING>);
    // E.g. Delete all keys with pattern "foo/*"
    client.DeleteRange("foo/"); 

    await client.DeleteRangeAsync(<PREFIX_STRING>);
    // E.g. Delete all keys with pattern "foo/*" in async
    await client.DeleteRangeAsync("foo/");


## Coming Soon
* Watch support
* Auth Operations (Add users,roles etc.)