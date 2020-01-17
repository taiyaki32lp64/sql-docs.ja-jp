---
title: LocalDB | のサポートMicrosoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6da7f1aed956c8b2f5c71496c9c121f6006eabb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935959"
---
# <a name="support-for-localdb"></a>LocalDB のサポート

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB は、以降[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]で使用可能なの軽量バージョンです。 ここでは、LocalDB インスタンス内のデータベースに接続する方法について説明します。

## <a name="remarks"></a>Remarks

Localdb のインストール方法、localdb インスタンスの構成方法など、localdb の詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB のオンラインブックの「」を参照してください。

LocalDB では、次のことを簡単に行うことができます。

-   **Sqllocaldb i**を使用して、既定のインスタンスの名前を検出します。

-   **AttachDBFilename** 接続文字列キーワードを使用して、サーバーをアタッチするデータベース ファイルを指定できます。 **AttachDBFilename** を使用するときに、**Database** 接続文字列キーワードを使用してデータベース名を指定しなかった場合、データベースはアプリケーションの終了時に LocalDB インスタンスから削除されます。

-   接続文字列では、次のように LocalDB インスタンスを指定します。 例として、SQLSRV 接続文字列の例を次に示します。

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    PDO_SQLSRV 接続文字列の例を次に示します。  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

必要に応じて、sqllocaldb.exe を使用して LocalDB インスタンスを作成できます。 また、sqlcmd.exe を使用して、LocalDB インスタンスのデータベースの追加と変更を実行できます。 たとえば、`sqlcmd -S (localdb)\v11.0` のようになります。 (IIS で実行している場合、コマンドラインでを実行する場合と同じ結果を得るには、正しいアカウントでを実行する必要があります。詳細については、「完全な IIS での[LocalDB の使用」、「パート 2: インスタンスの所有権](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx)」を参照してください)。

次に示すのは、myInstance という名前の LocalDB インスタンス内のデータベースに接続する SQLSRV ドライバーを使用した接続文字列の例です。

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

PDO_SQLSRV ドライバーを使用した接続文字列の例を次に示します。このドライバーは、myInstance という名前の LocalDB インスタンス内のデータベースに接続します。  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

LocalDB のインストール手順については、 [localdb のドキュメント](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)を参照してください。 LocalDB インスタンス内のデータを変更するために sqlcmd を使用する場合は、 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)が必要です。

## <a name="see-also"></a>参照

[サーバーへの接続](../../connect/php/connecting-to-the-server.md)
