---
title: アップグレード後のクエリ ストアの使用
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cdb24eff5efa62058aa2c20ecec0a85d43c83ae0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251546"
---
# <a name="change-the-database-compatibility-level-and-use-the-query-store"></a>データベース互換性レベルの変更とクエリ ストアの使用

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、一部の変更は、[データベースの互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)が変更された後に有効になります。 これは、次の理由のためです。  
  
- アップグレードは一方向の操作である (ファイル形式をダウン グレードできない) ため、データベース内で新機能を有効にする操作を別の操作に分離することが重要です。 以前のデータベース互換性レベルに設定を戻すことができます。  新しいモデルでは、停止期間中に発生する処理の数が減ります。  
  
- クエリ プロセッサに対する変更は、複雑な影響をもたらす可能性があります。 システムに対する "良い" 変更は、ほとんどのワークロードには有益であっても、その他のワークロードにとって重要なクエリで許容できない回帰を引き起こす可能性があります。 アップグレード プロセスからこのロジックを分離すると、クエリ ストアなどの機能は、プラン選択の回帰を迅速に緩和し、さらには実稼働サーバーで完全に回避できます。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] では、データベースを装着したか復元したとき、また、インプレース アップグレード後、以下の動作が予想されます。
> - アップグレード前のユーザー データベースの互換性レベルが 100 以上の場合は、アップグレード後も互換性レベルは変わりません。    
> - アップグレード前のユーザー データベースの互換性レベルが 90 の場合、アップグレードされたデータベースの互換性レベルは 100 に設定されます。これは、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] でサポートされている下限の互換性レベルです。    
> - tempdb、model、msdb、および Resource データベースの互換性レベルは、アップグレード後に現在の互換性レベルに設定されます。   
> - master システム データベースは、アップグレード前の互換性レベルを保持します。    
  
新しいクエリ プロセッサの機能を有効にするためのアップグレード プロセスは、製品のリリース後のサービス モデルに関連付けられます。  それらの修正プログラムの一部は、[トレース フラグ 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199) でリリースされます。  修正プログラムを必要とするユーザーは、他のユーザーにとって予期しない回帰を引き起こすことなくそれらの修正プログラムを適用できます。 クエリ プロセッサの修正プログラムのリリース後のサービス モデルは、 [ここ](https://support.microsoft.com/kb/974006)に記載されています。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、新しい互換性レベルに移行した場合、トレース フラグ 4199 は不要になります。これは、それらの修正プログラムは最新の互換レベルで既定で有効になっているためです。 そのため、アップグレード プロセスの一環として、アップグレード プロセスが完了したら、4199 が無効になっていることを検証することが重要です。  

> [!NOTE]
> ただし、RTM の後にリリースされた新しいクエリ プロセッサの修正プログラムを有効にするためには (該当する場合)、トレース フラグ 4199 が必要です。
  
以下のような、クエリ プロセッサを最新バージョンのコードにアップグレード場合に推奨されるワークフローについては、「[新しい SQL Server にアップグレードするときにパフォーマンスの安定性を維持する](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)」を参照してください。  
  
![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "|::ref1::|") 

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18 以降では、ユーザーはクエリ調整アシスタントを使用して、推奨されるワークフローのガイドを得ることができます。 詳細については、「[クエリ調整アシスタントを使用したデータベースのアップグレード](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)」を参照してください。
 
## <a name="see-also"></a>参照  
[データベースの互換性レベルの表示または変更](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)     
[クエリ ストアの使用シナリオ](../../relational-databases/performance/query-store-usage-scenarios.md)     
[ALTER DATABASE &#40;Transact-SQL&#41; 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)     
[クエリ調整アシスタントを使用したデータベースのアップグレード](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)        
  
