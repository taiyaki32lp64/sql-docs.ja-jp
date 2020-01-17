---
title: データの取得 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2dd99b2195cb4f44725ff813bc79c70ec5ffc44b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935890"
---
# <a name="retrieving-data"></a>データの取得
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックと、このセクションのトピックでは、データを取得する方法について説明します。  
  
## <a name="sqlsrv-driver"></a>SQLSRV ドライバー  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の SQLSRV ドライバーは、結果セットからデータを取得するための次のオプションを提供しています。  
  
-   [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
  
-   [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)  
  
-   [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)/[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
  
> [!NOTE]  
> 上記のいずれかの関数を使用する場合は、ループの終了の条件として null 比較を避けてください。 **sqlsrv** 関数はエラーの発生時に false を返すため、次のコードは [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)でエラー発生時に無限ループになる可能性があります。  
>   
> `/*``This code could result in an infinite loop. It is recommended that`  
>   
> `you do NOT use null comparisons as the criterion for exiting loops,`  
>   
> `as is done here. */`  
>   
> `do{`  
>   
> `$result = sqlsrv_fetch_array($stmt);`  
>   
> `} while( !is_null($result));`  
  
クエリで、複数の結果セットを取得する場合、 [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)によって次の結果セットに移動できます。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] のバージョン 1.1 以降では、[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) を使用して、結果セットに行が含まれているかどうかを確認できます。  
  
## <a name="pdosqlsrv-driver"></a>PDO_SQLSRV ドライバー  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の PDO_SQLSRV ドライバーは、結果セットからデータを取得するための次のオプションを提供します。  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
クエリで、複数の結果セットを取得する場合、 [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md)によって次の結果セットに移動できます。  
  
スクロール可能なカーソルを指定し、 [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md)を呼び出すと、結果セットに含まれる行数を確認できます。  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) により、カーソルの種類を指定できます。 次に、 [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) によって、行を選択できます。 例および詳細については、 [PDO::prepare](../../connect/php/pdo-prepare.md) を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|---------|---------------|  
|[文字列としてデータを取得する](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|サーバーからデータをストリーミングする方法の概要を説明し、特定のユース ケースへのリンクを示します。|  
|[方向パラメーターを使用する](../../connect/php/using-directional-parameters.md)|ストアド プロシージャを呼び出す際に、方向パラメーターを使用する方法について説明します。|  
|[カーソルの種類を指定し、行を選択する](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|任意の順序でアクセスできる行を含む結果セットを作成する方法を示します。|  
|[方法: SQLSRV ドライバーを使用して日付/時刻型を文字列として取得する](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|SQLSRV ドライバーを使用して日付/時刻型を文字列として取得する方法について説明します。|  
|[方法: PDO_SQLSRV ドライバーを使用して日付/時刻型を PHP DateTime オブジェクトとして取得する](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)|PDO_SQLSRV ドライバーを使用して日付/時刻型をオブジェクトとして取得する方法について説明します。|  
|[SQLSRV ドライバーを使用した10進文字列の書式設定](../../connect/php/formatting-decimals-sqlsrv-driver.md)|SQLSRV ドライバーを使用して、decimal または money の値の書式を設定する方法を示します。|  
|[PDO_SQLSRV Driver を使用した10進文字列の書式設定](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)|PDO_SQLSRV ドライバーを使用して、10進数または money の値を書式設定する方法を示します。|  
  
## <a name="related-sections"></a>関連項目  
[方法: PHP データ型を指定する](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>参照  
[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[データの取得](../../connect/php/retrieving-data.md)  
  
