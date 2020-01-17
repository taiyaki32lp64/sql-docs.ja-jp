---
title: FILEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEPROPERTYEX_TSQL
- FILEPROPERTYEX
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTYEX function
- file names [SQL Server], FILEPROPERTYEX
author: stevestein
ms.author: sstein
ms.openlocfilehash: 955cfe87f93bedc41c6aeb29951ee1c81d0a4d6e
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425934"
---
# <a name="filepropertyex-transact-sql"></a>FILEPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  現在のデータベース内のファイル名とプロパティ名を指定すると、指定された拡張ファイル プロパティ値が返されます。 現在のデータベースに存在しないファイル、または存在しない拡張ファイル プロパティの場合は NULL が返されます。 現在のところ、拡張ファイル プロパティは Azure Blob ストレージ内のデータベースにのみ適用されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
FILEPROPERTYEX ( name , property )  
```  
  
## <a name="arguments"></a>引数  
 *name*  
 プロパティ情報を返す基になる、現在のデータベースに関連付けられたファイルの名前を含む式を指定します。 *file_name* は **nchar (128)** です。  
  
 *property*  
 返されるファイル プロパティの名前を含む式を指定します。 *プロパティ* は **varchar (128)** , 、値は次のいずれかを指定することができます。  


  
|[値]|[説明]|
|-----------|-----------------|  
|**BlobTier**|ターゲット Azure ページ BLOB の層。 Azure ページ BLOB ストレージを使用する Standard および GeneralPurpose データベースのみに適用されます。|
|**[AccountType]**|BLOB ストレージとファイル ストレージのどちらであるか、また Premium ストレージと Standard ストレージのどちらであるかを示すストレージ アカウントの種類。|
|**IsInferredTier**|層が、データ サイズに合わせて拡張できる暗黙的な (推定される) 層であるか、明示的 (固定) レベルであるかを示します。|
|**IsPageBlob**|ターゲット BLOB がページ BLOB かどうかを示します。|
  
## <a name="return-types"></a>戻り値の型  
 **sql_variant**  
  
## <a name="remarks"></a>Remarks  
 *file_name* に対応する、 **名前** 内の列、 **sys.master_files** または **sys.database_files** カタログ ビューです。  
  
## <a name="examples"></a>使用例  
 次の例では、データベース ファイルの設定が返されます。
```sql
SELECT s.file_id,
       s.type_desc,
       s.name,
       FILEPROPERTYEX(s.name, 'BlobTier') AS BlobTier,
       FILEPROPERTYEX(s.name, 'AccountType') AS AccountType,
       FILEPROPERTYEX(s.name, 'IsInferredTier') AS IsInferredTier,
       FILEPROPERTYEX(s.name, 'IsPageBlob') AS IsPageBlob
FROM sys.database_files AS s
WHERE s.type_desc IN ('ROWS', 'LOG');
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
file_id  type_desc  name  BlobTier  AccountType  IsInferredTier  IsPageBlob
--------------------------------------------------------------------------------------
1     ROWS      data_0  P30  PremiumBlobStorage  0   1
2     LOG       log     P30  PremiumBlobStorage  0   1

(2 rows affected)
```  
  
## <a name="see-also"></a>参照  
 [FILEGROUPPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
