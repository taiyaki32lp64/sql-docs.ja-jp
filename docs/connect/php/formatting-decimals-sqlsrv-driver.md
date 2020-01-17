---
title: 10 進数文字列と金額の書式設定 (SQLSRV ドライバー) | Microsoft Docs
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
ms.openlocfilehash: 4a5ac641a98077c09bb38a5fc8fbd3fb1a4bf73d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265144"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>10 進数文字列と金額の書式設定 (SQLSRV ドライバー)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

精度を維持するために、 [decimal 型または numeric 型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)は常に正確な有効桁数とスケールを使用して文字列としてフェッチされます。 値が1未満の場合は、先頭のゼロがありません。 Money フィールドと smallmoney フィールドは、固定小数点以下桁数が4に設定された10進数フィールドであるため、これと同じです。

## <a name="add-leading-zeroes-if-missing"></a>先頭に0がない場合は追加します
バージョン5.6.0 以降では、オプション`FormatDecimals`が sqlsrv connection およびステートメントレベルに追加されます。これにより、ユーザーは10進数の文字列を書式設定できます。 このオプションでは、ブール値 (true または false) が想定され、フェッチされた結果の10進数値または数値の書式設定にのみ影響します。 つまり、 `FormatDecimals`このオプションは、挿入や更新などの他の操作には影響しません。

既定では、`FormatDecimals` は **false** です。 True に設定すると、1未満の10進値に対して先頭のゼロが追加されます。

## <a name="configure-number-of-decimal-places"></a>小数点以下桁数の構成
を`FormatDecimals`有効にすると、別`DecimalPlaces`のオプションとして、money と smallmoney のデータを表示するときにユーザーが小数点以下桁数を構成できるようになります。 [0, 4] の範囲で整数値を許容し、表示されると丸めが発生する場合があります。 ただし、基になる money データは変わりません。

どちらのオプションも接続レベルまたはステートメントレベルに設定できます。また、ステートメントの設定は、常に対応する接続設定よりも優先されます。 このオプションは`DecimalPlaces` money データに**のみ**影響するため`FormatDecimals` `DecimalPlaces` 、を有効にするには true に設定する必要があることに注意してください。 それ以外の`DecimalPlaces`場合は、設定に関係なく、書式設定は無効になります。

> [!NOTE]
> Money または smallmoney のフィールドには小数点`DecimalPlaces`以下桁数が4であるため、負の数値または4より大きい値に設定すると無視されます。 書式設定された money データを任意の計算の入力として使用することはお勧めしません。

## <a name="example---a-simple-fetch"></a>例-単純なフェッチ
次の例は、単純なフェッチで新しいオプションを使用する方法を示しています。

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>例-出力パラメーターの書式を設定する
Decimal または numeric フィールドが[output パラメーター](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)として返される場合、戻り値は通常の varchar 文字列と見なされます。 ただし、SQLSRV_SQLTYPE_DECIMAL または SQLSRV_SQLTYPE_NUMERIC のいずれかが指定され`FormatDecimals`ている場合は、を true に設定して、数値文字列値に先行ゼロがないことを確認できます。 詳細については、「[方法: SQLSRV ドライバーを使用して出力パラメーターを取得する](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)」をご覧ください。

次の例では、10進数 (8, 4) の値を返すストアドプロシージャの出力パラメーターを書式設定する方法を示します。

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>参照
[10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[データの取得](../../connect/php/retrieving-data.md)
