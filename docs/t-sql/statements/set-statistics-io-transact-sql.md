---
title: SET STATISTICS IO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_IO_TSQL
- IO
- IO_TSQL
- SET STATISTICS IO
dev_langs:
- TSQL
helpviewer_keywords:
- disk I/O statistics [SQL Server]
- I/O [SQL Server], disk activity information
- disks [SQL Server], statement statistics
- STATISTICS IO option
- statements [SQL Server], statistical information
- SET STATISTICS IO statement
- statistical information [SQL Server], disk activity
ms.assetid: 7033aac9-a944-4156-9ff4-6ef65717a28b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3cf335242bd0f0e33939c0a72c19390d90252103
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941842"
---
# <a name="set-statistics-io-transact-sql"></a>SET STATISTICS IO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントによって生成されるディスク利用状況に関する情報を表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET STATISTICS IO { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 STATISTICS IO が ON のときは統計情報が表示され、OFF のときは表示されません。   
  
 このオプションを ON に設定した後は、オプションを OFF に設定するまで、すべての [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで統計情報が返されます。  
  
 次の表は、出力アイテムの一覧とその説明です。  
  
|出力アイテム|意味|  
|-----------------|-------------|  
|**Table**|テーブルの名前。|  
|**Scan count**|出力の最終的なデータセットを構築するすべての値を取得するため、リーフ レベルに達した後で任意の方向に開始されたシークまたはスキャンの数。<br /><br /> 使用されているインデックスが主キーの一意なインデックスまたはクラスター化インデックスで、1 つの値のみをシークしている場合、Scan count は 0 になります。 たとえば、`WHERE Primary_Key_Column = <value>` のようになります。<br /><br /> 主キーではない列で定義されている一意ではないクラスター化インデックスを使用して 1 つの値を検索する場合、Scan count は 1 になります。 この処理は、検索対象のキー値の重複値を確認するために行われます。 たとえば、`WHERE Clustered_Index_Key_Column = <value>` のようになります。<br /><br /> インデックス キーを使用してキー値を特定した後、リーフ レベルで左側または右側に向かって開始された異なるシークまたはスキャンの数が N である場合、Scan count は N になります。|  
|**logical reads**|データ キャッシュから読み取られたページ数。|  
|**physical reads**|ディスクから読み取られたページ数。|  
|**read-ahead reads**|クエリ用のキャッシュに読み取られたページ数。|  
|**lob logical reads**|データ キャッシュから読み取られたページ数。 **text**、**ntext**、**image**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、または列ストア インデックスのページが含まれます。|  
|**lob physical reads**|ディスクから読み取られたページ数。 **text**、**ntext**、**image**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、または列ストア インデックスのページが含まれます。|  
|**lob read-ahead reads**|クエリ用のキャッシュに読み取られたページ数。 **text**、**ntext**、**image**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、または列ストア インデックスのページが含まれます。|

 SET STATISTICS IO は、解析時ではなく実行時に設定されます。

> [!NOTE]  
> Transact-SQL ステートメントで LOB 列を取得するとき、LOB 取得操作で LOB ツリーを複数回移動することが必要になる場合があります。 その結果、SET STATISTICS IO では、予想より多くの論理読み取り数が報告されることがあります。

## <a name="permissions"></a>アクセス許可  
 SET STATISTICS IO を使用するには、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限が必要です。 SHOWPLAN 権限は必要ありません。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でステートメントの処理に使用された論理読み取りと物理読み取りの数を示します。  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS IO ON;  
GO  
SELECT *   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS IO OFF;  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
Table 'ProductCostHistory'. Scan count 1, logical reads 5, physical   
reads 0, read-ahead reads 0, lob logical reads 0, lob physical reads 0,   
lob read-ahead reads 0.  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)  
  
  
