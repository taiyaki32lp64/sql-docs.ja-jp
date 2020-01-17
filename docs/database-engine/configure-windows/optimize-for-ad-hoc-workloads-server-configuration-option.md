---
title: optimize for ad hoc workloads サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c66a4d3826493d10974ab4ce8363e3adde1bd0fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998417"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>optimize for ad hoc workloads サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **optimize for ad hoc workloads** オプションを使用すると、1 回のみ使用するアドホック バッチが多数含まれているワークロードのプラン キャッシュの効率を高めることができます。 このオプションを 1 に設定すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、バッチが初めてコンパイルされるときに、完全なコンパイル済みプランではなく、コンパイル済みプランの小さいスタブをプラン キャッシュに格納します。 これにより、再利用されないコンパイル済みプランでプラン キャッシュがいっぱいにならないようにして、メモリの負荷を下げることができます。 
  
  コンパイル済みプランのスタブを使用すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、このアドホック バッチが既にコンパイルされているが、コンパイル済みプランのスタブしか格納していないと認識します。そのため、このバッチが再度呼び出される (コンパイルまたは実行される) と、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、バッチがコンパイルされ、コンパイル済みプランのスタブがプラン キャッシュから削除され、完全なコンパイル済みプランがプラン キャッシュに追加されます。 
  
 コンパイル済みプランのスタブは、sys.dm_exec_cached_plans カタログ ビューによって表示される cacheobjtype の 1 つです。 これには、一意の SQL ハンドルとプラン ハンドルが含まれています。 コンパイル済みプランのスタブには、関連付けられた実行プランがないため、プラン ハンドルに対してクエリを実行しても、XML プラン表示は返されません。  
  
 [トレース フラグ 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) は、キャッシュ制限パラメーターを [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM の設定に戻します。これにより、一般に、より大きいキャッシュに対応できるようになります。 この設定は、頻繁に再利用されるキャッシュ エントリがキャッシュに収まらない場合や、サーバー構成オプション [アドホック ワークロードの最適化] でプラン キャッシュの問題を解決できない場合に使用します。  
  
> [!WARNING]  
>  トレース フラグ 8032 を使用した場合、キャッシュが大きいために他のメモリ コンシューマー (バッファー プールなど) で利用できるメモリが少なくなると、パフォーマンスが低下することがあります。  

## <a name="recommendations"></a>推奨事項
プラン キャッシュに 1 回のみ使われるプランを多数格納することは避けてください。 この問題の一般的な原因は、クエリ パラメーターのデータ型が一貫して定義されていないことです。 これは文字列の長さに特に適用されますが、最大長、有効桁数、小数点以下桁数が含まれるすべてのデータ型に適用できます。 たとえば、@Greeting という名前のパラメーターが 1 回の呼び出しで nvarchar(10) として渡され、次の呼び出しで nvarchar(20) として渡される場合、パラメーター サイズごとに別のプランが作成されます。 クエリに複数のパラメーターが含まれ、これらが呼び出し時に一貫して定義されていないと、クエリごとに大量のクエリ プランが存在している場合があります。 プランは使用されているクエリ パラメーターのデータ型と長さの組み合わせごとに存在する可能性があります。

多数の 1 回のみ使われるプランにより、OLTP サーバーの [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のメモリの多くの部分が占有されていて、これらのプランがアドホック プランである場合は、このサーバー オプションを使って、これらのオブジェクトのメモリ使用量を削減します。
1 回のみ使われてキャッシュされるプランの数を調べるには、次のクエリを実行します。

```sql
SELECT objtype, cacheobjtype, 
  AVG(usecounts) AS Avg_UseCount, 
  SUM(refcounts) AS AllRefObjects, 
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> **optimize for ad hoc workloads** を 1 に設定すると、新しいプランのみに影響します。プラン キャッシュ内の既存のプランには影響しません。
> 既にキャッシュされているクエリ プランにすぐに適用するには、[ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) を使ってプラン キャッシュをクリアするか、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要があります。

## <a name="see-also"></a>参照  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
