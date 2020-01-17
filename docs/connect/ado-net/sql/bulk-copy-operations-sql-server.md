---
title: SQL Server での一括コピー操作
description: .NET Data Provider for SQL Server のバルク コピー機能について説明します。
ms.date: 09/30/2019
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70eed483eb7cb857e23b110b7149badff14ab46f
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452294"
---
# <a name="bulk-copy-operations-in-sql-server"></a>SQL Server での一括コピー操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server には、SQL Server データベースのテーブルまたはビューに大きなファイルを高速で一括コピーするための、**bcp** という一般的なコマンド ライン ユーティリティが用意されています。 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> クラスを使用すると、同様の機能を提供するマネージコードソリューションを作成できます。 SQL Server テーブルにデータを読み込む方法は他にもありますが (INSERT ステートメントなど)、<xref:Microsoft.Data.SqlClient.SqlBulkCopy> を使用する方が大幅にパフォーマンスが向上します。  
  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> クラスを使用すると、次の操作を実行できます。  
  
- 単一の一括コピー操作  
  
- 複数の一括コピー操作  
  
- トランザクション内での一括コピー操作  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient.SqlBulkCopy> クラスがサポートされていない、バージョン 1.1 以前の .NET Framework では、<xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを使用して、SQL Server Transact-SQL **BULK INSERT** ステートメントを実行できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
[一括コピーのセットアップ例](bulk-copy-example-setup.md)  
一括コピーの例で使用されるテーブルについて説明し、AdventureWorks データベースにテーブルを作成するための SQL スクリプトを示します。  
  
[単一の一括コピー操作](single-bulk-copy-operations.md)  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> クラスを使用して SQL Server のインスタンスにデータの単一の一括コピーを実行する方法と、Transact-sql ステートメントと <xref:Microsoft.Data.SqlClient.SqlCommand> クラスを使用して一括コピー操作を実行する方法について説明します。  
  
[複数の一括コピー操作](multiple-bulk-copy-operations.md)  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> クラスを使用して SQL Server のインスタンスにデータの複数の一括コピー操作を実行する方法について説明します。  
  
[トランザクションと一括コピー操作](transaction-bulk-copy-operations.md)  
トランザクションをコミットまたはロールバックする方法など、トランザクション内で一括コピー操作を実行する方法について説明します。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
