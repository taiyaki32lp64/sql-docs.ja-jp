---
title: sqlsrv_errors |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08879880e93307a496969b79c3aa05144f7aef62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015062"
---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

最後に実行された **sqlsrv** 操作に関する拡張エラーや警告の情報を返します。  
  
後の「パラメーター」セクションで示されているパラメーター値のいずれかを指定して **Sqlsrv_errors** 関数を呼び出すことにより、エラーや警告の情報を取得できます。  
  
既定では、いずれかの **sqlsrv** 関数の呼び出しで生成される警告はエラーとして扱われます。 **sqlsrv** 関数の呼び出しで警告が発生した場合、関数は false を返します。 ただし、SQLSTATE 値 01000、01001、01003、および 01S02 に対応する警告はエラーとして扱われません。  
  
次のコード行は、上で説明した動作を無効にします。 **sqlsrv** 関数の呼び出しによって警告が生成されても、関数は false を返しません。  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
次のコード行は、既定の動作に戻します。(上で説明した場合を除き) 警告はエラーとして扱われます。  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
設定に関係なく、警告は、**SQLSRV_ERR_ALL** または **SQLSRV_ERR_WARNINGS** パラメーター値を指定して **sqlsrv_errors** を呼び出すことによってのみ取得できます (詳細については後の「パラメーター」セクションを参照)。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>パラメーター  
*$errorsAndOrWarnings* (省略可能): 定義済みの定数。 このパラメーターには、次の表に示すいずれかの値を指定できます。  
  
|[値]|[説明]|  
|---------|---------------|  
|SQLSRV_ERR_ALL|**sqlsrv** 関数の最後の呼び出しで生成されたエラーと警告が返されます。|  
|SQLSRV_ERR_ERRORS|**sqlsrv** 関数の最後の呼び出しで生成されたエラーが返されます。|  
|SQLSRV_ERR_WARNINGS|**sqlsrv** 関数の最後の呼び出しで生成された警告が返されます。|  
  
パラメーターの値を指定しないと、 **sqlsrv** 関数の最後の呼び出しで生成されたエラーと警告が返されます。  
  
## <a name="return-value"></a>戻り値  
配列の **array** 、または **null**。 返される **array** 内の各 **array** には、3 つのキーと値のペアが含まれます。 次の表では、各キーとその説明を示します。  
  
|Key|[説明]|  
|-------|---------------|  
|SQLSTATE|ODBC ドライバー由来のエラーの場合、ODBC が返す SQLSTATE。 ODBC の SQLSTATE 値については、「 [ODBC Error Codes (ODBC エラー コード)](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)」を参照してください。<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]由来のエラーの場合、IMSSP の SQLSTATE。<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]由来の警告の場合、01SSP の SQLSTATE。|  
|コード|SQL Server 由来のエラーの場合、SQL Server のネイティブ エラー コード。<br /><br />ODBC ドライバー由来のエラーの場合、ODBC が返すエラー コード。<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]由来のエラーの場合、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] のエラー コード。 詳細については、「 [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md)」を参照してください。|  
|message|エラーの説明です。|  
  
配列の値は、数値キー 0、1、および 2 でアクセスすることもできます。 エラーまたは警告が発生しなかった場合、 **null** が返されます。  
  
## <a name="example"></a>例  
次の例では、失敗したステートメント実行の間に発生したエラーを表示します (ステートメントは、**InvalidColumName** が指定されたテーブルの有効な列名ではないために失敗します)。この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
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
  
/* Set up a query to select an invalid column name. */  
$tsql = "SELECT InvalidColumnName FROM Sales.SalesOrderDetail";  
  
/* Attempt execution. */  
/* Execution will fail because of the invalid column name. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
      if( ($errors = sqlsrv_errors() ) != null)  
      {  
         foreach( $errors as $error)  
         {  
            echo "SQLSTATE: ".$error[ 'SQLSTATE']."\n";  
            echo "code: ".$error[ 'code']."\n";  
            echo "message: ".$error[ 'message']."\n";  
         }  
      }  
}  
  
/* Free connection resources */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
