---
title: 一括読み込みのセキュリティに関する考慮事項 (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, XML Bulk Load
- bulk load [SQLXML], security
- security [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], security
ms.assetid: 192fc6d4-ecbc-4a4d-a5cb-55e1f64af318
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 817c8c4d0ff2a140033e99879c0720a63f81e5f4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252524"
---
# <a name="bulk-load-security-considerations-sqlxml-40"></a>一括読み込みのセキュリティに関する注意点 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  次に、XML 一括読み込みを使用する場合のセキュリティに関するガイドラインを示します。  
  
-   一括読み込み操作をトランザクションとして実行するように指定する場合は、 **Tempfilepath**プロパティを使用して、一時ファイルを作成するフォルダーを指定します。  
  
     一括読み込み処理では、次の権限付きの一時ファイルが作成されます。  
  
    -   読み取り、書き込み、削除アクセス。一括読み込み処理に許可されます。  
  
    -   読み取り権限。これらのファイルに Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がアクセスするときのアカウントは不明であるため、この権限はすべてのユーザーに許可されます。 一時ファイルを格納するフォルダーに適切な権限を設定することで、これらの一時ファイルへのアクセスを制限できます。  
  
-   XML 一括読み込み自体には権限の設定はありません。 ここでは、データベースが正しく設定され、ユーザー コンテキスト (一括読み込みを使用するよう設定されているログイン) に適切な権限が設定されていることが前提となります。  
  
-   トランザクション以外のモードで一括読み込みの処理中にエラーが発生した場合は、データが部分的に読み込まれたままになることがあります。 一括読み込み処理は、エラーが発生した時点で停止するだけです。 この問題を軽減するには、トランザクション モードを使用します。  
  
-   一括読み込みで発生するエラーには、データベースに関する情報が含まれる場合があります。 たとえば、テーブルまたは列の名前や、列の型情報が含まれることが考えられます。 一括読み込みを使用するときには、一括読み込み処理でエラーを検出して一般的なエラー メッセージを返すように設計し、ユーザーに直接エラーが表示されないようにしてください。  
  
-   一括読み込みで処理されるデータ量に制限は設定されていません。 一括読み込みでは、読み込むデータのサイズはチェックされません。 一括読み込みを実行するユーザーは、自身の責任で、指定したファイルの処理に必要なメモリを確保し、読み込むデータの格納に必要な空き領域がデータベースにあるかどうかを確認する必要があります。  
  
-   一括読み込みでは、コードとして提供されたデータは使用されず、 データ入力はどのような形式でも実行されません。 入力データ内のコードまたはコマンドは、通常のデータとして扱われ、実行されることはありません。  
  
-   一括読み込みでは、XML と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ モデルの違いに基づき、指定されたデータの形式が変更される場合があります。 たとえば、時間を指定する形式はこれら 2 つで異なるため、 一括読み込みではこの違いの解決が試みられます。 この結果、一部の精度情報が失われる場合があります。  
  
-   一括読み込みでは、データ処理は時間の制限なく、 処理が完了するかエラーが発生するまで続けられます。  
  
-   一括読み込みでは、データベース内の一時テーブルを作成および削除できます。したがって、このための権限が必要です。 これらのテーブルに対する権限は、一括読み込み処理のためデータベースに接続している同じユーザーに与えられます。  
  
-   一括読み込みでは、トランザクション モードでの処理中に使用される一時ファイルを作成および削除できます。したがって、このための権限が必要です。 これらのファイルには、作成時、一括読み込みが実行されているスレッドの現在のユーザーと同じ権限が与えられます。  
  
-   ユーザーが、エラーを書き込む SQLXML のエラー ログ ファイルを設定した場合は、一括読み込みが実行されるたびに、最新の一括読み込み処理のデータでファイルの内容が上書きされます。  
  
## <a name="see-also"></a>参照  
 [XML データの一括読み込みを実行する &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
