---
title: PDO::prepare | Microsoft Docs
ms.custom: ''
ms.date: 04/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bb02fefe4e4845a1ab1e7b7a7117845fdaebf13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993202"
---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

実行するステートメントを準備します。

## <a name="syntax"></a>構文

```
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )
```

#### <a name="parameters"></a>パラメーター
$*statement*: SQL ステートメントを含む文字列。

*key_pair*: 属性の名前と値を含む配列。 詳細については、「解説」を参照してください。

## <a name="return-value"></a>戻り値
成功した場合は、PDOStatement オブジェクトを返します。 失敗した場合は、PDOException オブジェクトを、または `PDO::ATTR_ERRMODE` の値によっては false を返します。

## <a name="remarks"></a>Remarks
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] では、実行されるまで準備されたステートメントを検証しません。

次の表は、使用可能な *key_pair* の値を一覧しています。

|Key|[説明]|
|-------|---------------|
|PDO::ATTR_CURSOR|カーソル動作を定義します。 スクロール不可の順方向カーソル `PDO::CURSOR_FWDONLY` が既定値です。 `PDO::CURSOR_SCROLL` はスクロール可能なカーソルです。<br /><br />たとえば、`array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )` のようになります。<br /><br />`PDO::CURSOR_SCROLL` に設定すると、以下で説明するように、`PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` を使用してスクロール可能なカーソルの種類を設定することができます。<br /><br />PDO_SQLSRV ドライバーの結果セットとカーソルに関する詳細については、「[カーソルの種類 &#40;PDO_SQLSRV ドライバー&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)」を参照してください。|
|PDO::ATTR_EMULATE_PREPARES|既定ではこの属性は false です。この `PDO::ATTR_EMULATE_PREPARES => true` により変更することができます。 詳細と例については、[エミュレートの準備](#emulate-prepare)に関するセクションを参照してください。|
|PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE|スクロール可能なカーソルの種類を指定します。 `PDO::ATTR_CURSOR` が `PDO::CURSOR_SCROLL` に設定されている場合にのみ有効です。 この属性に指定可能な値については、以下を参照してください。|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|フェッチされた通貨値の書式設定時に、小数点以下の桁数を指定します。 このオプションは `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` が true の場合のみ機能します。 詳細については、「[10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)」を参照してください。|
|PDO::SQLSRV_ATTR_DIRECT_QUERY|True の場合、直接クエリの実行を指定します。 False は、準備されたステートメントの実行です。 `PDO::SQLSRV_ATTR_DIRECT_QUERY` に関する詳細については、「[Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)」 (PDO_SQLSRV ドライバーでの直接ステートメント実行と準備されたステートメントの実行) を参照してください。|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (既定値)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|日付型と時刻型を [PHP DateTime](http://php.net/manual/en/class.datetime.php) オブジェクトを使用して取得するかどうかを指定します。 詳細については、「[方法: PDO_SQLSRV ドライバーを使用して日付/時刻型を PHP DateTime オブジェクトとして取得する](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)」を参照してください。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|数値の SQL 型の列からの数値フェッチを処理します。 詳細については、「 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)」を参照してください。|
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|該当する場合に 10 進文字列の前にゼロを追加するかどうかを指定します。 このオプションを設定すると、`PDO::SQLSRV_ATTR_DECIMAL_PLACES` オプションが money 型の書式設定用に有効となります。 詳細については、「[10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)」を参照してください。| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|詳細については、「 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)」を参照してください。|

`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` を使用する場合、`PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` を使用してカーソルの種類を指定できます。 たとえば、動的カーソルを設定するには次の配列を PDO::prepare に渡します。
```
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));
```
`PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` に指定可能な値を次の表に示します。 スクロール可能なカーソルの詳細については、「[カーソルの種類 &#40;PDO_SQLSRV ドライバー&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)」を参照してください。

|[値]|[説明]|
|---------|---------------|
|PDO::SQLSRV_CURSOR_BUFFERED|クライアント側の (バッファー処理された) 静的カーソルを作成します。これは、クライアント マシンのメモリ内に結果セットをバッファー処理します。|
|PDO::SQLSRV_CURSOR_DYNAMIC|サーバー側 (バッファーなし) の動的カーソルを作成します。これは、任意の順序で行にアクセスすることができ、変更内容がデータベースに反映されます。|
|PDO::SQLSRV_CURSOR_KEYSET|サーバー側のキーセット カーソルを作成します。 行がテーブルから削除される場合 (削除された行は、値なしで返されます)、キーセット カーソルは行の数を更新しません。|
|PDO::SQLSRV_CURSOR_STATIC|サーバー側の静的カーソルを作成します。これは、任意の順序で行にアクセスできますが、変更内容はデータベースに反映されません。<br /><br />`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` は `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC` を意味します。|

PDOStatement オブジェクトを閉じるには、`unset` を呼び出します。
```
unset($stmt);
```

## <a name="example"></a>例
この例では、パラメーター マーカーと順方向専用カーソルで PDO::prepare を使用する方法を示します。

```
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$col1 = 'a';
$col2 = 'b';

$query = "insert into Table1(col1, col2) values(?, ?)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( $col1, $col2 ) );
print $stmt->rowCount();
echo "\n";

$query = "insert into Table1(col1, col2) values(:col1, :col2)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );
print $stmt->rowCount();

unset($stmt);
?>
```

## <a name="example"></a>例
この例では、サーバー側の静的カーソルで PDO::prepare を使用する方法を示します。 クライアント側カーソルの例については、「[カーソルの種類 &#40;PDO_SQLSRV ドライバー&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)」を参照してください。

```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
$stmt->execute();

echo "\n";

while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){
   print "$row[Name]\n";
}
echo "\n..\n";

$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );
print "$row[Name]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );
print "$row[1]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );
print "$row[1]..\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );
print_r($row);
?>
```

<a name="emulate-prepare" />

## <a name="example"></a>例

この例では、`PDO::ATTR_EMULATE_PREPARES` を true に設定して PDO::prepare を使用する方法を示します。

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$database = "tempdb";
$conn = new PDO("sqlsrv:server = $serverName; Database = $database", $username, $password);

$pdo_options = array();
$pdo_options[PDO::ATTR_EMULATE_PREPARES] = true;
$pdo_options[PDO::SQLSRV_ATTR_ENCODING] = PDO::SQLSRV_ENCODING_UTF8;

$stmt = $conn->prepare("CREATE TABLE TEST([id] [int] IDENTITY(1,1) NOT NULL,
                                          [name] nvarchar(max))",
                                          $pdo_options);
$stmt->execute();

$prefix = '가각';
$name = '가각ácasa';
$name2 = '가각sample2';

$stmt = $conn->prepare("INSERT INTO TEST(name) VALUES(:p0)", $pdo_options);
$stmt->execute(['p0' => $name]);
unset($stmt);

$stmt = $conn->prepare("SELECT * FROM TEST WHERE NAME LIKE :p0", $pdo_options);
$stmt->execute(['p0' => "$prefix%"]);
foreach ($stmt as $row) {
    echo "\n" . 'FOUND: ' . $row['name'];
}

unset($stmt);
unset($conn);
?>
```

PDO_SQLSRV ドライバーの内部で、すべてのプレースホルダーが [PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md) でバインドされたパラメーターで置き換えられます。 そのため、プレースホルダーのない SQL クエリ文字列がサーバーに送信されます。 次の例について考えてみます。

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

`PDO::ATTR_EMULATE_PREPARES` が false に設定されている場合 (既定のケース)、データベースに送信されるデータは次のとおりです。

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

サーバーでは、パラメーターのバインド用のパラメーター化クエリ機能を使用してクエリが実行されます。 一方で、`PDO::ATTR_EMULATE_PREPARES` が true に設定されている場合、サーバーに送信されるクエリは基本的に次のとおりです。

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

`PDO::ATTR_EMULATE_PREPARES` を true に設定すると、SQL Server のいくつかの制限事項をバイパスすることができます。 たとえば、SQL Server では名前付きまたは位置パラメーターは一部の Transact-SQL 句でサポートされていません。 さらに、SQL Server には、2100 個のパラメーターのバインドの制限があります。

> [!NOTE]
> emulate prepare が true に設定されている場合、パラメーター化クエリのセキュリティは有効ではありません。 そのため、アプリケーションでは、パラメーターにバインドされたデータに、悪意のある Transact-SQL コードが含まれていないことを確認する必要があります。

### <a name="encoding"></a>[エンコード]

別のエンコーディング (UTF-8 やバイナリなど) でパラメーターをバインドしたい場合、PHP スクリプトにエンコーディングを明確に指定する必要があります。

PDO_SQLSRV ドライバーでは最初に `PDO::bindParam()` に指定されたエンコーディングがチェックされます (たとえば、`$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`)。

見つからない場合、`PDO::prepare()` または `PDOStatement::setAttribute()` にエンコーディングが設定されているかどうかドライバーによりチェックされます。 それ以外の場合、ドライバーでは `PDO::__construct()` または `PDO::setAttribute()` に指定されたエンコーディングが使用されます。

### <a name="limitations"></a>制限事項

ご覧のように、バインディングはドライバーによって内部的に行われます。 有効なクエリが実行のためにパラメーターなしでサーバーに送信されます。 通常のケースと比較すると、パラメーター化クエリ機能が使用されていない場合にいくつかの制限事項が発生します。

- `PDO::PARAM_INPUT_OUTPUT` としてバインドされたパラメーターの場合は機能しません。
    - ユーザーが `PDO::bindParam()` で `PDO::PARAM_INPUT_OUTPUT` を指定すると、PDO 例外がスローされます。
- 出力パラメーターとしてバインドされたパラメーターの場合は機能しません。
    - ユーザーが準備されたステートメントを出力パラメーター用のプレースホルダーを使用して作成した場合 (つまり、`SELECT ? = COUNT(*) FROM Table1` のようにプレースホルダーのすぐ後に等号が指定されている場合)、PDO 例外がスローされます。
    - 準備されたステートメントにより、出力パラメーター用の引数としてプレースホルダーを使用してストアド プロシージャが呼び出された場合、ドライバーでは出力パラメーターを検出できないため、例外はスローされません。 一方で、ユーザーが出力パラメーター用に指定した変数は変更されません。
- バイナリでエンコードされたパラメーター用にプレースホルダーが重複して指定されている場合、機能しません。

## <a name="see-also"></a>参照
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)

