---
title: sys.bandwidth_usage (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ea963c07a15cd5c2db3cca113680026d3100936b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942573"
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

> [!NOTE]
> これにのみ適用されます[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.* *  
  
 内の各データベースで使用されるネットワーク帯域幅に関する情報を返します、  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11 データベース サーバー**、します。 指定のデータベースに対して返される各行は、1 時間にわたる 1 つの方向とクラスの使用状況をまとめたものです。  
  
 **これは非推奨で、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]します。**  
  
 **Sys.bandwidth_usage**ビューには、次の列が含まれています。  
  
|Column Name|説明|  
|-----------------|-----------------|  
|**time**|帯域幅が使用されていた時間。 このビューの行は、1 時間単位です。 たとえば、2009-09-19 02:00: 00.000 は、帯域幅が 2009 年 9 月 19 日午前 2:00 から午前 3:00 までの間に使用された ことを示します。|  
|**database_name**|帯域幅を使用したデータベースの名前。|  
|**direction**|帯域幅使用されたのいずれかの種類:<br /><br /> 受信:移行するデータ、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]します。<br /><br /> 送信:データの移動が、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]します。|  
|**class**|使用された帯域幅のクラス。次のどちらかです。<br />内部。Azure プラットフォーム内で移行するデータ。<br />外部:Azure platform から移行するデータ。<br /><br /> このクラスは、データベースで、地域 ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]) 間の連続コピー リレーションシップが進行中である場合に返されます。 連続コピー リレーションシップで、特定のデータベースが参加していない場合は、「インター リンク」行は返されません。 詳細については、このトピックの後半の「解説」セクションを参照してください。|  
|**time_period**|ピーク時または OffPeak のいずれかの期間の使用状況が発生したときに。 ピーク時間は、サーバーが作成されたリージョンに基づきます。 たとえば、 サーバーが "US_Northwest" リージョンで作成された場合、Peak 時間帯は太平洋標準時の午前 10:00 から 午後 6 時まで (PST)。|  
|**数量**|サポートされているキロバイト (Kb) 単位での帯域幅の量。|  
  
## <a name="permissions"></a>アクセス許可

 このビューはのみ利用可能、**マスター**データベース、サーバー レベル プリンシパル ログインをします。  
  
## <a name="remarks"></a>コメント  
  
### <a name="external-and-internal-classes"></a>外部および内部クラス

 特定の時点で使用される各データベースに対して、 **sys.bandwidth_usage**ビューには、クラスと帯域幅の使用の方向を示す行が返されます。 次の例は、指定されたデータベースに対して公開される可能性があるデータを示しています。 この例では、時刻は 2012-04-21 17:00:00 になっています。これは、ピーク タイムの時間帯における発生時刻です。 データベース名は、Db1 です。 この例で**sys.bandwidth_usage**受信と送信方向の外部および内部クラスでは、4 つの組み合わせをすべての行が次のように戻りました。  
  
|time|database_name|direction|class|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|外部リンク|Peak|741|  
|2012-04-21 17:00:00|Db1|Ingress|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|Internal|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>[!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]でのデータ方向の解釈

 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]の場合、帯域幅の使用状況データは連続コピー リレーションシップの両側にある論理マスター データベースで確認できます。 ように、イングレスを解釈して、クエリを実行するデータベースの観点から方向インジケーターを出力します。 たとえば、ソース サーバーからターゲット サーバーへ、1 MB のデータを転送するレプリケーション ストリームについて考えてみます。 この場合、移行元サーバーで 1 MB 数までカウントする、送信した合計データと対象サーバーで 1 MB が受信したデータとして記録されます。  
  
> [!NOTE]  
> 転送されたデータの大部分は、移行元サーバーからユーザーのデータ フローの方向で、対象サーバーです。 ただし、一部のデータ転送では他の方向が必要になる場合があります。  
