---
title: INDEXKEY_PROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INDEXKEY_PROPERTY_TSQL
- INDEXKEY_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- index keys [SQL Server]
- INDEXKEY_PROPERTY function
- viewing index keys
- displaying index keys
- keys [SQL Server], index
ms.assetid: 87c0c385-6b2d-4716-ac8c-a3ce6e8d89e9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: edaa3069bece2d6acf7f28ab32da5f5639f49be4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024269"
---
# <a name="indexkey_property-transact-sql"></a>INDEXKEY_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インデックス キーについての情報を返します。 XML インデックスに対して NULL を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
INDEXKEY_PROPERTY ( object_ID ,index_ID ,key_ID ,property )  
```  
  
## <a name="arguments"></a>引数  
 *object_ID*  
 テーブルまたはインデックス付きビューのオブジェクト ID 番号です。 *object_ID* は **int** です。  
  
 *index_ID*  
 インデックスの ID 番号です。 *index_ID* は **int**です。  
  
 *key_ID*  
 インデックス キー列の位置です。 *key_ID* is **int**.  
  
 *property*  
 情報が返されるプロパティの名前です。 *プロパティ* 、文字の文字列は、次の値のいずれかを指定することができます。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**ColumnId**|列の ID で、*key_ID*、インデックスの位置。|  
|**IsDescending**|インデックス列を格納する順序です。<br /><br /> 1 = 降順、0 = 昇順|  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="exceptions"></a>例外  
 エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。  
  
 ユーザーが所有しているか、または権限を与えられている、セキュリティ保護可能なリソースのメタデータのみを表示できます。 つまり、オブジェクトに対する権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (INDEXKEY_PROPERTY など) が NULL を返す可能性があります。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、両方のプロパティが `1` テーブルのインデックス ID `1`、キー列 `Production.Location` に対して返されます。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT   
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'ColumnId') AS [Column ID],  
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'IsDescending') AS [Asc or Desc order];  
```  
  
 以下に結果セットを示します。  
  
```  
Column ID   Asc or Desc order   
----------- -----------------   
1           0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [INDEX_COL &#40;Transact-SQL&#41;](../../t-sql/functions/index-col-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
