---
title: sqlsrv_free_stmt |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_free_stmt
apitype: NA
helpviewer_keywords:
- sqlsrv_free_stmt
- API Reference, sqlsrv_free_stmt
ms.assetid: 3c71f432-36ad-41e1-8ac7-587c82539448
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6f062d1237cfc92c5697fa005b3f78268aa48f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992718"
---
# <a name="sqlsrvfreestmt"></a>sqlsrv_free_stmt
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

指定したステートメントに関連付けられているすべてのリソースを解放します。 この関数が呼び出された後はステートメントは再利用できません。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_free_stmt( resource $stmt)  
```  
  
#### <a name="parameters"></a>パラメーター  
*$stmt*: 閉じるステートメントです。  
  
## <a name="return-value"></a>戻り値  
関数が無効なパラメーターを使用して呼び出されている場合を除き、ブール値は **true** です。 関数が無効なパラメーターで呼び出された場合、 **false** を返します。  
  
> [!NOTE]  
> この関数のパラメーターとして、**Null** は有効です。 これにより、スクリプトで複数回関数を呼び出すことが可能になります。 たとえば、エラー状態でステートメントを解放して、スクリプトの最後にもう 1 回解放する場合、**sqlsrv_free_stmt** への 2 回目の呼び出しによって **true** が返されます。これは、(エラー状態での) **sqlsrv_free_stmt** への最初の呼び出しでステートメント リソースが **null** に設定されるためです。  
  
## <a name="example"></a>例  
次の例では、ステートメントのリソースを作成し、単純なクエリを実行し、このステートメントに関連付けられているすべてのリソースを解放する **sqlsrv_free_stmt** を呼び出します。 この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM Person.Contact");  
if( $stmt )  
{  
     echo "Statement executed.\n";  
}  
else  
{  
     echo "Query could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*-------------------------------  
     Process query results here.  
-------------------------------*/  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  

[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)  
  
