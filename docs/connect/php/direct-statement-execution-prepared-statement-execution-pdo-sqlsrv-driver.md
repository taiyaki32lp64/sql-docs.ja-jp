---
title: Direct ステートメント-準備されたステートメントの実行 PDO_SQLSRV Driver |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa9e544fb7b79009d86a5742946a722d5adc18f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993621"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver (PDO_SQLSRV ドライバーでの直接ステートメント実行と準備されたステートメントの実行)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、PDO::SQLSRV_ATTR_DIRECT_QUERY 属性を使用して、準備されたステートメントの実行である既定ではなく、直接のステートメントの実行を指定する方法について説明します。 パラメーターバインドを使用してステートメントを複数回実行した場合、準備されたステートメントを使用すると、パフォーマンスが向上する可能性があります。  
  
## <a name="remarks"></a>Remarks  
ドライバーによるステートメントの[!INCLUDE[tsql](../../includes/tsql-md.md)]準備を行わずにステートメントをサーバーに直接送信する場合は、pdo:: SQLSRV_ATTR_DIRECT_QUERY 属性を pdo:: [setAttribute](../../connect/php/pdo-setattribute.md) (または、 [pdo:: __ コンストラクトに渡されるドライバーオプションとして設定できます。](../../connect/php/pdo-construct.md))、または[PDO::p repare](../../connect/php/pdo-prepare.md)を呼び出す場合。 既定では、PDO:: SQLSRV_ATTR_DIRECT_QUERY の値は False です (準備されたステートメントの実行を使用します)。  
  
[PDO:: query](../../connect/php/pdo-query.md)を使用する場合は、直接実行することもできます。 [Pdo:: query](../../connect/php/pdo-query.md)を呼び出す前に、pdo:: [setAttribute](../../connect/php/pdo-setattribute.md)を呼び出し、pdo:: SQLSRV_ATTR_DIRECT_QUERY を True に設定します。  Pdo:: [query](../../connect/php/pdo-query.md)の各呼び出しは、pdo:: SQLSRV_ATTR_DIRECT_QUERY に対して異なる設定を使用して実行できます。  
  
[PDO::p repare](../../connect/php/pdo-prepare.md)と[PDOStatement:: execute](../../connect/php/pdostatement-execute.md)を使用して、バインドされたパラメーターを使用してクエリを複数回実行する場合、準備されたステートメントを実行すると、繰り返しクエリの実行が最適化されます。  この状況では、ドライバーオプションの配列パラメーターで pdo:: SQLSRV_ATTR_DIRECT_QUERY を False に設定して[pdo::p repare](../../connect/php/pdo-prepare.md)を呼び出します。 必要に応じて、PDO:: SQLSRV_ATTR_DIRECT_QUERY を False に設定して、準備されたステートメントを実行できます。  
  
[Pdo::p repare](../../connect/php/pdo-prepare.md)を呼び出した後、準備されたクエリの実行時に pdo:: SQLSRV_ATTR_DIRECT_QUERY の値を変更することはできません。  
  
クエリで、前のクエリで設定されたコンテキストが必要な場合は、PDO:: SQLSRV_ATTR_DIRECT_QUERY を True に設定してクエリを実行します。 たとえば、クエリで一時テーブルを使用する場合は、PDO:: SQLSRV_ATTR_DIRECT_QUERY を True に設定する必要があります。  
  
次の例では、前のステートメントのコンテキストが必要な場合に、PDO:: SQLSRV_ATTR_DIRECT_QUERY を True に設定する必要があることを示しています。 このサンプルは、クエリが直接実行されたときに、プログラム内の後続のステートメントでのみ使用できる一時テーブルを使用します。  
  
> [!NOTE]
> クエリでストアドプロシージャを呼び出し、このストアドプロシージャで一時テーブルを使用する場合は、代わりに[PDO:: exec](../../connect/php/pdo-exec.md)を使用します。

```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)
  
