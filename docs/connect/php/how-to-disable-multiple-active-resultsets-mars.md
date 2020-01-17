---
title: '方法: 複数のアクティブな結果セット (MARS) を無効にする | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c5edf63a654b21d080e48f93c71553b8909ce8fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993563"
---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>方法: 複数のアクティブな結果セット (MARS) を無効にする
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

複数のアクティブな結果セット (MARS) を有効にしていない SQL Server データ ソースに接続する必要がある場合、MultipleActiveResultSets 接続オプションを使用して、MARS を無効または有効にすることができます。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-disable-mars-support"></a>MARS のサポートを無効にするには  
  
-   次の接続オプションを使用します。  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    アプリケーションが、開いているアクティブな結果セットのある接続でクエリを実行しようとする場合、2 番目のクエリ試行で、次のエラー情報が返されます。  
  
    接続は、結果が保留中のステートメントがあるために、この操作を処理できません。  他のクエリが接続を使用できるようにするには、すべての結果をフェッチするか、ステートメントをキャンセルまたは解放します。 MultipleActiveResultSets 接続オプションの詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。  
  
## <a name="example"></a>例  
次の例は [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]の SQLSRV ドライバーを使用して、MARS サポートを無効にする方法を示しています。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>例  
次の例は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の PDO_SQLSRV ドライバーを使用して、MARS サポートを無効にする方法を示しています。  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>参照  
[サーバーへの接続](../../connect/php/connecting-to-the-server.md)  
  
