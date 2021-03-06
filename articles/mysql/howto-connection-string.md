---
title: How to connect applications to Azure Database for MySQL | Microsoft Docs
description: This document lists the currently supported connection strings for applications to connect with Azure Database for MySQL, including ADO.Net (C#), JDBC, Node.JS, ODBC, PHP, Python, Ruby.
services: mysql
author: mswutao 
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.assetid: 
ms.service: mysql-database
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
---

# How to connect applications to Azure Database for MySQL
This document lists the connection string types supported by Azure Database for MySQL, together with templates and examples. You may have different parameters and different settings in your connection string.

- Refer to this document [How to configure SSL](./howto-configure-ssl.md) to obtain the certificate.
- {your_host} = <servername>.mysql.database.azure.com

## ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={your_username};Pwd={your_password};[SslMode=Required;]
```

In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, password is `mypassword!2`. Then, the connection string should be:

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {your_username}, {your_password}";
```

## Node.JS
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {your_username}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={your_username};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {your_username}, {your_password}, {your_database}, {your_port});
```

## Python
```python
cnx = mysql.connector.connect(user={your_username}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## Ruby
```ruby
client = Mysql2::Client.new(username: {your_username}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## Get the connection string details from the Azure portal
In [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL and click **Connection strings** to get your string list for your instance:
![connection strings on portal](./media/howto-connection-strings/connection-strings-on-portal.png)

The string provides details such as the driver, server, and other database connection parameters. Modify these examples using your own parameters, such as database name, password, and so on. You can then use this string to connect to the server from your code and applications.

## Next steps
- For more information regarding connection library, see [Concepts - Connection libraries](./concepts-connection-libraries.md)
