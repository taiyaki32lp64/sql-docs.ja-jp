---
title: PDOStatement::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6dab577ea12544d6dd40081283b46378dd07d5e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992936"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

定義済み PDO 属性またはカスタム ドライバー属性のいずれかの属性値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>パラメーター  
$*attribute*: PDO::ATTR_* または PDO::SQLSRV_ATTR_\* 定数のいずれかの整数。 使用可能な属性の一覧については、「解説」セクションを参照してください。  
  
$*value*: 指定された $*attribute* に設定される (複合) 値。  
  
## <a name="return-value"></a>戻り値  
成功した場合は TRUE、それ以外の場合は FALSE です。  
  
## <a name="remarks"></a>Remarks  
次の表に、使用可能な属性の一覧を示します。  
  
|attribute|値|[説明]|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|PHP メモリの制限に 1。|クライアント側カーソルの結果セットを保持するバッファーのサイズを設定します。<br /><br />既定値は 10,240 KB (10 MB) です。<br /><br />クライアント側カーソルの詳細については、「[カーソルの種類 &#40;PDO_SQLSRV ドライバー&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)」を参照してください。|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|0 から 4 までの整数|フェッチされた通貨値の書式設定時に、小数点以下の桁数を指定します。<br /><br />負の整数値または 4 を超える値は無視されます。<br /><br />このオプションは、PDO::SQLSRV_ATTR_FORMAT_DECIMALS が true の場合にのみ機能します。<br /><br />このオプションは、接続レベルでも設定されている場合があります。 その場合、このオプションにより接続レベルのオプションがオーバーライドされます。<br /><br />詳細については、「[10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)」を参照してください。|
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (既定)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|ドライバーがサーバーとの通信に使用する文字セット エンコーディングを設定します。|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true または false|日付型と時刻型を [PHP DateTime](http://php.net/manual/en/class.datetime.php) オブジェクトを使用して取得するかどうかを指定します。 false のままにすると、文字列として返すことが既定の動作となります。<br /><br />このオプションは、接続レベルでも設定されている場合があります。 その場合、このオプションにより接続レベルのオプションがオーバーライドされます。<br /><br />詳細については、「[方法: PDO_SQLSRV ドライバーを使用して日付/時刻型を PHP DateTime オブジェクトとして取得する](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)」を参照してください。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true または false|数値の SQL 型 (bit、integer、smallint、tinyint、float、または real) の列からの数値フェッチを処理します。<br /><br />接続オプション フラグ ATTR_STRINGIFY_FETCHES がオンの場合、SQLSRV_ATTR_FETCHES_NUMERIC_TYPE がオンであっても戻り値は文字列となります。<br /><br />バインド列の戻された PDO 型が PDO_PARAM_INT の場合、整数列からの戻り値は、SQLSRV_ATTR_FETCHES_NUMERIC_TYPE がオフであっても int となります。|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true または false|該当する場合に 10 進文字列の前にゼロを追加するかどうかを指定します。 このオプションを設定すると、PDO::SQLSRV_ATTR_DECIMAL_PLACES オプションが money 型の書式設定用に有効となります。 false のままにすると、正確な有効桁数を戻し、1 未満の値の前にあるゼロを省略するという既定の動作が使用されます。<br /><br />このオプションは、接続レベルでも設定されている場合があります。 その場合、このオプションにより接続レベルのオプションがオーバーライドされます。<br /><br />詳細については、「[10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)」を参照してください。| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|クエリのタイムアウト (秒単位) を設定します。<br /><br />既定で、ドライバーは、結果を無制限に待機します。 負の数値は許可できません。<br /><br />0 は、タイムアウトがないことを示します。|  
  
## <a name="example"></a>例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
