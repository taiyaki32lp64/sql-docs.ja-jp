---
title: SQLSRV ドライバーを使用して日付/時刻型を文字列として取得する | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8c3fbd475d5f7038d36ba17a9578713c3ed1b53
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993530"
---
# <a name="how-to-retrieve-date-and-time-types-as-strings-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用して日付/時刻型を文字列として取得する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

の[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]SQLSRV ドライバーを使用する場合は、次のように指定することで、日付と時刻の型 (**smalldatetime**、 **datetime**、 **date**、 **time**、 **datetime2**、 **datetimeoffset**) を文字列として取得できます。接続文字列またはステートメントレベルのオプション:

```
'ReturnDatesAsStrings'=>true
```

既定値は **false** です。つまり、**smalldatetime**、**datetime**、**date**、**time**、**datetime2**、**datetimeoffset** 型は [PHP DateTime](http://php.net/manual/en/class.datetime.php) オブジェクトとして返されます。 このオプションがステートメントレベルで設定されている場合は、接続レベルの設定が上書きされます。

PDO_SQLSRV ドライバーは、既定では日付と時刻の型を文字列として返します。 PHP DateTime オブジェクトとして取得する方法については、「[方法: PDO_SQLSRV を使用して日付と時刻の型を Php Datetime オブジェクトとして取得](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)する」を参照してください。

## <a name="example"></a>例
次は、日付/時刻型を文字列として取得する構文の例です。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_close($conn);
?>
```

## <a name="example"></a>例
次の例では、文字列の取得時に UTF-8 を指定することで、接続が `"ReturnDatesAsStrings" => false` で行われていても、日付を文字列として取得できます。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;

sqlsrv_close($conn);
?>
```

## <a name="example"></a>例
次の例は、接続文字列に UTF-8 と `"ReturnDatesAsStrings" => true` を指定し、日付を文字列として取得する方法を示しています。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8');
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;
sqlsrv_close($conn);
?>
```

## <a name="example"></a>例
次のコード例では、日付を PHP 型として取得する方法を示します。 `'ReturnDatesAsStrings'=> false` は既定でオンです。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as a DateTime object, then convert to string using PHP's date_format function
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

$date_string = date_format($date, 'jS, F Y');
echo "Date = $date_string\n";

sqlsrv_close($conn);
?>
```

## <a name="example"></a>例
ステートメントレベルの Return? Asstrings オプションは、対応する接続オプションよりも優先されます。

```php
<?php
$serverName = 'MyServer';
$connectionInfo = array('Database' => 'MyDatabase', 'ReturnDatesAsStrings' => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tableName = 'MyTable';
$options = array('ReturnDatesAsStrings' => true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}
sqlsrv_execute($stmt);

// Expect the fetched value to be a string
$field = sqlsrv_get_field($stmt, 0);
echo $field . PHP_EOL;

sqlsrv_close($conn);
?>
```

## <a name="see-also"></a>参照
[データの取得](../../connect/php/retrieving-data.md)

[方法: PDO_SQLSRV を使用して日付/時刻型を PHP DateTime オブジェクトとして取得する](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)
