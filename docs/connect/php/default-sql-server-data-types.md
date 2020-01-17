---
title: 既定の SQL Server データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69c138e7eb5d2c4f6dbace0db59ce235e1c0a5f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993660"
---
# <a name="default-sql-server-data-types"></a>既定の SQL Server のデータ型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

サーバーにデータを送信する際に、ユーザーが SQL Server のデータ型を指定していない場合、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] はその PHP データ型を SQL Server のデータ型に変換します。 次の表は、PHP のデータ型 (サーバーに送信されるデータ型) と SQL Server の既定のデータ型 (データが変換されるデータ型) を示しています。 サーバーにデータを送信する際にデータ型を指定する方法の詳細については、「 [方法: SQLSRV ドライバーを使用する場合に SQL Server データ型を指定する](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md)」を参照してください。  
  
|PHP のデータ型|SQLSRV ドライバーの SQL Server の既定の型|PDO_SQLSRV ドライバーの SQL Server の既定の型|  
|-----------------|------------------------------------------------|-----------------------------------------------------|  
|NULL|varchar (1)|サポートされていません|  
|Boolean|bit|bit|  
|Integer|INT|INT|  
|float|float(24)|サポートされていません|  
|文字列 (長さ 8000 バイト未満)|varchar(<string length>)|varchar(<string length>)|  
|文字列 (8000 バイトを超える長さ)|varchar(max)|varchar(max)|  
|リソース|サポートされていません。|サポートされていません。|  
|ストリーム (エンコード: バイナリではない)|varchar(max)|varchar(max)|  
|ストリーム (エンコード: バイナリ)|varbinary|varbinary|  
|Array|サポートされていません。|サポートされていません。|  
|Object|サポートされていません。|サポートされていません。|  
|DateTime (1)|DATETIME|サポートされていません。|  
  
## <a name="see-also"></a>参照  
[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[データ型の変換](../../connect/php/converting-data-types.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)

[PHP の型](https://php.net/manual/language.types.php)

[データ型 (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)  
  
