---
title: 10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 76c314159faf15e63bf77b17a8a45abf217b205c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265149"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

精度を維持するために、 [decimal 型または numeric 型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)は常に正確な有効桁数とスケールを使用して文字列としてフェッチされます。 値が1未満の場合は、先頭のゼロがありません。 Money フィールドと smallmoney フィールドは、固定小数点以下桁数が4に設定された10進数フィールドであるため、これと同じです。

## <a name="add-leading-zeroes-if-missing"></a>先頭に0がない場合は追加します
バージョン5.6.0 以降では、ユーザーは接続属性`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`またはステートメント属性を使用して、10進数の文字列を書式設定できます。 この属性は、ブール値 (true または false) を想定しており、フェッチされた結果の10進数値または数値の書式設定にのみ影響します。 言い換えると、この属性は、挿入や更新などの他の操作には影響しません。

既定では、`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` は **false** です。 True に設定すると、1未満の10進値に対して先頭のゼロが追加されます。

## <a name="configure-number-of-decimal-places"></a>小数点以下桁数の構成
で`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`は、別の接続`PDO::SQLSRV_ATTR_DECIMAL_PLACES`属性またはステートメント属性であるが有効になっているため、ユーザーは money および smallmoney データを表示するときに小数点以下の桁数を構成できます。 [0, 4] の範囲で整数値を許容し、表示されると丸めが発生する場合があります。 ただし、基になる money データは変わりません。

ステートメント属性は、常に対応する接続設定より優先されます。 このオプションは`PDO::SQLSRV_ATTR_DECIMAL_PLACES` money データに**のみ**影響し`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 、true に設定する必要があることに注意してください。 それ以外の`PDO::SQLSRV_ATTR_DECIMAL_PLACES`場合は、設定に関係なく、書式設定は無効になります。

> [!NOTE]
> Money または smallmoney のフィールドには小数点`PDO::SQLSRV_ATTR_DECIMAL_PLACES`以下桁数が4であるため、負の数値または4より大きい値に設定しても無視されます。 書式設定された money データを任意の計算の入力として使用することはお勧めしません。

### <a name="to-set-the-connection-attributes"></a>接続属性を設定するには

-   接続ポイントで属性を設定します。

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   接続後の属性の設定:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>例-money データの書式を設定する
次の例は、 [PDOStatement:: bindColumn](../../connect/php/pdostatement-bindcolumn.md)を使用して money データをフェッチする方法を示しています。

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>例-接続属性をオーバーライドする
次の例は、接続属性をオーバーライドする方法を示しています。

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>参照
[10 進数文字列と金額の書式設定 (SQLSRV ドライバー)](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[データの取得](../../connect/php/retrieving-data.md)
