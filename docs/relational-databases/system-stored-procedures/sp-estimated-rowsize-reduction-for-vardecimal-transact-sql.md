---
title: sp_estimated_rowsize_reduction_for_vardecimal (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- sp_estimated_rowsize_reduction_for_vardecimal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- decimal data type, compressing
- numeric data type, compressing
- estimate decimal compression
- table compression [SQL Server]
ms.assetid: 0fe45983-f9f2-4c7f-938a-0fd96e1cbe8d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 90de7b95febdf2f1a25a5e584b2ca77bb67f93d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124507"
---
# <a name="spestimatedrowsizereductionforvardecimal-transact-sql"></a>sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  テーブルで vardecimal ストレージ形式を有効にした場合は、行の平均サイズ削減量を見積もります。 この数値を使用して、テーブル サイズ全体の削減量を見積もることができます。 統計のサンプリングを使用する、行サイズの平均削減量を計算すると、以降は、見積もりとして見なします。 vardecimal ストレージ形式を有効にした後、まれに行サイズが増加する場合があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代わりに、行の圧縮とページの圧縮を使用してください。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。 テーブルとパーティション インデックスのサイズに圧縮効果を参照してください。 [sp_estimate_data_compression_savings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_estimated_rowsize_reduction_for_vardecimal [ [ @table_name = ] 'table'] [;]  
```  
  
## <a name="arguments"></a>引数  
`[ @table = ] 'table'` ストレージ形式を変更するテーブルの 3 部構成の名前です。 *テーブル*は**nvarchar (776)** します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 現在と見積もりテーブル サイズの情報を提供する次の結果セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**avg_rowlen_fixed_format**|**decimal (12, 2)**|固定の decimal ストレージ形式の行の長さを表します。|  
|**avg_rowlen_vardecimal_format**|**decimal (12, 2)**|Vardecimal ストレージ形式を使用すると行サイズの平均を表します。|  
|**row_count**|**int**|テーブル内の行の数。|  
  
## <a name="remarks"></a>コメント  
 使用**sp_estimated_rowsize_reduction_for_vardecimal**を vardecimal ストレージ形式のテーブルを有効にした場合の節約を推定します。 インスタンスを 40%、テーブルのサイズを小さく場合は、行の平均サイズを 40% 削減することができます、可能性のあることができます。 ただし FILL FACTOR と行サイズによっては、テーブル領域を削減できない場合もあります。 たとえば、長さ 8,000 バイトの行があり、そのサイズを 40% を削減したとしても、データ ページに収まるのは 1 行のみであることに変わりはないので、領域は削減されません。  
  
 場合の結果**sp_estimated_rowsize_reduction_for_vardecimal**テーブルが増大、つまりほぼ全体有効桁数の decimal データ型と、小規模の追加に使用する多くの行で、テーブルのことを示しますvardecimal ストレージ形式に必要なオーバーヘッドは、vardecimal ストレージ形式による削減量を超えています。 このまれな場合、vardecimal ストレージ形式有効にしないでください。  
  
 テーブルが vardecimal ストレージ形式の有効な場合を使用して、 **sp_estimated_rowsize_reduction_for_vardecimal**を vardecimal ストレージ形式が無効になっている場合、行の平均サイズを推定します。  
  
## <a name="permissions"></a>アクセス許可  
 テーブルに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
 場合、次の例では、推定行サイズの削減、`Production.WorkOrderRouting`テーブルに、`AdventureWorks2012`データベースを圧縮します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimated_rowsize_reduction_for_vardecimal 'Production.WorkOrderRouting' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_db_vardecimal_storage_format &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
