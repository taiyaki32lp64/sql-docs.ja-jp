---
title: カーソルの種類 (PDO_SQLSRV ドライバー) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c62c2a35123e77f5366dd5348fd51b3c50c85605
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993688"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>カーソルの種類 (PDO_SQLSRV ドライバー)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV ドライバーを使用すると、複数のカーソルの 1 つでスクロール可能な結果セットを作成できます。

PDO_SQLSRV ドライバーを使用してカーソルを指定する方法と、コードのサンプルについては、「[pdo::prepare](../../connect/php/pdo-prepare.md)」を参照してください。

## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV とサーバー側のカーソル
バージョン 3.0 より前の [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] では、PDO_SQLSRV ドライバーを使用して、サーバー側の順方向専用または静的カーソルで結果セットを作成することができました。 バージョン 3.0 の [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] からは、キーセットと動的カーソルも利用できます。

サーバー側のカーソルの種類は、[PDO::prepare](../../connect/php/pdo-prepare.md) を使用して次のいずれかのカーソルの種類を選択することで指定できます。

-   `PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY`

-   `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`

`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` を指定し、その後適切な値を `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` に渡すことで、動的、静的、またはキーセット カーソルを要求できます。 サーバー側のカーソル用に `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` に渡すことができる値は、次のとおりです。

-   `PDO::SQLSRV_CURSOR_DYNAMIC`

-   `PDO::SQLSRV_CURSOR_STATIC`

-   `PDO::SQLSRV_CURSOR_KEYSET`

## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV とクライアント側のカーソル
クライアント側のカーソルはバージョン 3.0 の [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] で追加されました。これを使用すると、結果セット全体をメモリにキャッシュすることができます。 利点の 1 つは、クエリの実行後に行数を使用できることです。

クライアント側のカーソルは、小規模から中規模の結果セットに対して使用する必要があります。 大規模な結果セットの場合は、サーバー側のカーソルを使用する必要があります。

クライアント側のカーソルを使用しているときにバッファーが結果セット全体を保持するために十分な大きさではない場合、クエリから false が返されます。 バッファーのサイズは PHP メモリの上限まで増やすことができます。

[PDO::setAttribute](../../connect/php/pdo-setattribute.md) または [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) の `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE` の属性を使用すると、結果セットを保持するバッファーのサイズを構成することができます。 php.ini ファイルで pdo_sqlsrv.client_buffer_max_kb_size を使用して最大バッファー サイズを設定することもできます (たとえば、pdo_sqlsrv.client_buffer_max_kb_size = 1024)。

[PDO::prepare](../../connect/php/pdo-prepare.md) を使用し、`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` カーソルの種類を指定し、その後 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED` を指定することで、クライアント側のカーソルを要求できます。

## <a name="example"></a>例
次の例は、バッファー処理されたカーソルを指定する方法を示しています。
```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));
$stmt->execute();
print $stmt->rowCount();

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

## <a name="see-also"></a>参照
[カーソルの種類を指定し、行を選択する](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)

