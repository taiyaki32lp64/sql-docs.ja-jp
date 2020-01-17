---
title: トランザクションと一括コピー操作
description: トランザクションをコミットまたはロールバックする方法など、トランザクション内で一括コピー操作を実行する方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: c2e855407edd6b2af51ae5710cd6601e9aa25654
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451911"
---
# <a name="transaction-and-bulk-copy-operations"></a>トランザクションと一括コピー操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

一括コピー操作は、単独の操作として、または、複数の手順からなるトランザクションの一部として実行されます。 複数の手順からなるトランザクションの一部として実行する場合、挿入、更新、削除など、他のデータベース操作に加えて、同じトランザクション内で一括コピー操作を複数回実行でき、トランザクション全体をコミットまたはロールバックすることもできます。  
  
既定では、一括コピー操作は単独の操作として実行されます。 この一括コピー操作は非トランザクション方式で処理され、ロールバックできません。 エラーが発生した際に、バルク コピー処理の全部または一部をロールバックする必要がある場合は、<xref:Microsoft.Data.SqlClient.SqlBulkCopy> が管理するトランザクションを使用するか、既存のトランザクション内でバルク コピー操作を実行するか、または **System.Transactions**<xref:System.Transactions.Transaction> に参加させることもできます。  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>非トランザクション処理の一括コピー操作の実行  
次のコンソール アプリケーションでは、非トランザクション処理の一括コピー操作で操作途中にエラーが発生した場合の処理を示しています。  
  
例では、コピー元のテーブルとコピー先のテーブルにはそれぞれ、**ProductID** という名前の `Identity` 列があります。 このコードでは、最初にコピー先のテーブルの行をすべて削除してコピー先を用意し、コピー元のテーブルに存在する **ProductID** 行を 1 行挿入しています。 既定では、行が追加されるたびに、コピー先のテーブル内の `Identity` 列に新しい値が生成されます。 この例では、一括読み込み処理でコピー元のテーブルの `Identity` 値を強制的に使用する接続が開かれるときに、オプションが設定されます。  
  
この一括コピー操作は、<xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A> プロパティを 10 に設定して実行されます。 操作中に無効な行が検出されると、例外がスローされます。 次に示す最初の例の一括コピー操作はトランザクション処理ではありません。 エラー発生ポイントまでにコピーされたバッチはすべてコミットされ、重複キーが含まれるバッチはロールバックされます。また、一括コピー操作は、他のバッチを処理する前に中止されます。  
  
> [!NOTE]
>  このサンプルは、「[一括コピーのセットアップ例](bulk-copy-example-setup.md)」で説明しているように作業テーブルを作成して取得してからでないと動作しません。 このコードでは、**SqlBulkCopy** だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server インスタンス内に存在する場合、Transact-SQL`INSERT … SELECT` ステートメントを使用すれば簡単かつ高速にデータをコピーすることができます。  
  
[!code-csharp[DataWorks SqlBulkCopyOpeions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>トランザクションでの専用の一括コピー操作の実行  
既定では、一括コピー操作は専用のトランザクションで実行されます。 専用の一括コピー操作を実行する場合は、接続文字列を使用して <xref:Microsoft.Data.SqlClient.SqlBulkCopy> の新しいインスタンスを作成するか、アクティブなトランザクションを使用せずに既存の <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトを使用します。 各シナリオでは、一括コピー操作でトランザクションを作成し、その後、トランザクションをコミットするかロールバックします。  
  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> クラス コンストラクターで <xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> オプションを明示的に指定することにより、一括コピー操作を専用のトランザクションで明示的に実行できます。一括コピー操作の各バッチを別々のトランザクション内で実行できます。  
  
> [!NOTE]
>  異なるバッチは別々のトランザクション内で実行されます。このため、一括コピー操作中にエラーが発生した場合、現在処理中のバッチの行はすべてロールバックされますが、エラー発生より前のバッチでコピーされた行はデータベースに残ります。  
  
次のコンソール アプリケーションは、前の例と似ていますが、一括コピー操作で専用のトランザクションを管理している点が異なります。 エラー発生ポイントまでにコピーされたバッチはすべてコミットされ、重複キーが含まれるバッチはロールバックされます。また、一括コピー操作は、他のバッチを処理する前に中止されます。  
  
> [!IMPORTANT]
>  このサンプルは、「[一括コピーのセットアップ例](bulk-copy-example-setup.md)」で説明しているように作業テーブルを作成して取得してからでないと動作しません。 このコードでは、**SqlBulkCopy** だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server インスタンス内に存在する場合、Transact-SQL`INSERT … SELECT` ステートメントを使用すれば簡単かつ高速にデータをコピーすることができます。  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>既存のトランザクションの使用  
既存の <xref:Microsoft.Data.SqlClient.SqlTransaction> オブジェクトは、<xref:Microsoft.Data.SqlClient.SqlBulkCopy> コンストラクターのパラメーターとして指定できます。 この場合、一括コピー操作は既存のトランザクションで実行され、このトランザクションの状態は変更されません (つまり、コミットも中止もされません)。 これにより、アプリケーションは他のデータベース操作を行うトランザクションで一括コピー操作を実行できます。 ただし、<xref:Microsoft.Data.SqlClient.SqlTransaction> オブジェクトを指定せず、null 参照を渡し、接続にアクティブなトランザクションがある場合は、例外がスローされます。  
  
エラーが発生したために一括コピー操作全体をロールバックする必要がある場合、または、ロールバックできる大きなプロセスの一部として一括コピーを実行する必要がある場合は、<xref:Microsoft.Data.SqlClient.SqlBulkCopy> コンストラクターに <xref:Microsoft.Data.SqlClient.SqlTransaction> オブジェクトを指定できます。  
  
次のコンソール アプリケーションは、最初の (トランザクションのない) 例とほぼ同じですが、一括コピー操作がより大きな外部トランザクションに含まれている点が異なります。 主キー違反エラーが発生した場合、トランザクション全体がロールバックされ、コピー先のテーブルに行は追加されません。  
  
> [!IMPORTANT]
>  このサンプルは、「[一括コピーのセットアップ例](bulk-copy-example-setup.md)」で説明しているように作業テーブルを作成して取得してからでないと動作しません。 このコードでは、**SqlBulkCopy** だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server インスタンス内に存在する場合、Transact-SQL`INSERT … SELECT` ステートメントを使用すれば簡単かつ高速にデータをコピーすることができます。  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>次の手順
- [SQL Server での一括コピー操作](bulk-copy-operations-sql-server.md)
