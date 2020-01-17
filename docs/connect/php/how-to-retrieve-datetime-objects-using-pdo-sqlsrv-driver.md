---
title: '方法: PDO_SQLSRV ドライバーを使用して日付/時刻型を PHP DateTime オブジェクトとして取得する | Microsoft Docs'
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 165e91cee3b0b4592f9b746f8b35b46bc73bce50
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264573"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdosqlsrv-driver"></a>方法: PDO_SQLSRV ドライバーを使用して日付/時刻型を PHP DateTime オブジェクトとして取得する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

バージョン5.6.0 で追加されたこの機能は、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]の PDO_SQLSRV ドライバーを使用している場合にのみ有効です。

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>日付/時刻型を DateTime オブジェクトとして取得するには

PDO_SQLSRV を使用する場合、日付と時刻の型 (**smalldatetime**、 **datetime**、 **date**、 **time**、 **datetime2**、および**datetimeoffset**) は、既定で文字列として返されます。 PDO:: ATTR_STRINGIFY_FETCHES と PDO:: SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 属性のいずれにも影響はありません。 日付と時刻の型を[PHP DateTime](http://php.net/manual/en/class.datetime.php)オブジェクトとして取得するには、接続また`PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE`はステートメントの属性を**true** (既定では**false** ) に設定します。

> [!NOTE]
> この接続属性またはステートメント属性は、DateTime オブジェクトを出力パラメーターとして指定できないため、日付と時刻の型の通常のフェッチにのみ適用されます。

## <a name="example---use-the-connection-attribute"></a>例-接続属性を使用する
次の例では、わかりやすくするためにエラーチェックを省略しています。 これは、接続属性を設定する方法を示しています。

```php
<?php
$server = 'myserver';
$databaseName = 'mydatabase';
$username = 'myusername';
$passwd = 'mypasword';
$tableName = 'mytable';

$conn = new PDO("sqlsrv:Server = $server; Database = $databaseName", $username, $passwd);

// To set the connection attribute
$conn->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = $conn->prepare($query);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_ASSOC);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-attribute"></a>例-ステートメント属性を使用する
次の例では、ステートメントの属性を設定する方法を示します。

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");
$query = "SELECT DateTimeCol FROM myTable";
$stmt = $conn->prepare($query);
$stmt->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_NUM);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-option"></a>例-ステートメントオプションを使用する
または、ステートメントの属性をオプションとして設定することもできます。

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");

$dateObj = null;
$query = "SELECT DateTimeCol FROM aTable";
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => true);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateObj, PDO::PARAM_LOB);
$row = $stmt->fetch(PDO::FETCH_BOUND);
var_dump($dateObj);

unset($stmt);
unset($conn);
?>
```

## <a name="example---retrieve-datetime-types-as-strings"></a>例-datetime 型を文字列として取得する
次の例では、逆のを実現する方法を示しています (これは、既定では false であるため、実際には必要ありません)。

```php
<?php
$database = "MyData";
$conn = new PDO("sqlsrv:server = (local); Database = $database");

$dateStr = null;
$query = 'SELECT DateTimeCol FROM table1';
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateStr);
$row = $stmt->fetch(PDO::FETCH_BOUND);
echo $dateStr . PHP_EOL;

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>参照
[データの取得](../../connect/php/retrieving-data.md)

[SQLSRV ドライバーを使用して日付/時刻型を文字列として取得する](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)