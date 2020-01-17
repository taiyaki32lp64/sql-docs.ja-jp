---
title: SQL Server または Azure SQL Database への接続 | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aeb46551b33f40ba6c42de705559e20d8c7b0315
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264608"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>SQL Server または Azure SQL Database への接続

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
サーバーとデータベースで作業するには、まず、サーバーに接続する必要があります。 同時に複数のサーバーに接続することができます。

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) では、複数の種類の接続をサポートしています。 この記事では、SQL Server と Azure SQL Database への接続 (Azure SQL 単一データベースまたはエラスティック プールへの接続) の詳細について説明します。 他の接続オプションについては、このページの下部に示す[リンク](#see-also)を参照してください。
  
## <a name="connecting-to-a-server"></a>サーバーへの接続  

1. **オブジェクト エクスプローラー**で、 **[接続]、[データベース エンジン]** の順にクリックします。

   ![connect](../media/connect-to-server/connect-db-engine.png)

1. **[サーバーへの接続]** フォームに必要事項を入力し、 **[接続]** をクリックします。

   ![サーバーへの接続](../media/connect-to-server/connect.png)

1. Azure SQL Server に接続する場合は、サインインしてファイアウォール規則を作成するように求めるメッセージが表示される場合があります。 **[サインイン]** をクリックします (メッセージが表示されない場合は、下記の手順 6 に進みます)。

   ![ファイアウォール](../media/connect-to-server/firewall-rule-sign-in.png)

1. サインインが正常に終了すると、フォームには特定の IP アドレスが既に設定された状態となります。 IP アドレスが頻繁に変更になる場合は、特定の範囲へのアクセス権を付与するのが簡単です。環境に応じて最適なオプションを選択してください。 

   ![ファイアウォール](../media/connect-to-server/new-firewall-rule.png)

1. ファイアウォール規則を作成して、サーバーに接続するには、 **[OK]** をクリックします。

1. 接続が正常に行われると、**オブジェクト エクスプローラー**にサーバー表示されます。

   ![接続済み](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>Next Steps

[テーブルの設計、作成、更新](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>参照

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[SQL Server Management Studio (SSMS) のダウンロード](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Azure Storage](../f1-help/connect-to-microsoft-azure-storage.md)  
