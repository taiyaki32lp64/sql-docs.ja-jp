---
title: FILEGROUPPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEGROUPPROPERTY_TSQL
- FILEGROUPPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], property values
- FILEGROUPPROPERTY function
- viewing filegroup properties
- displaying filegroup properties
ms.assetid: b3a930e6-df05-4034-929c-f681f5f6fc6e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5563c65352713f3557e4c412607d1944f28f3a3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071434"
---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

この関数は、指定した名前とファイル グループの値に対する、ファイル グループのプロパティ値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
FILEGROUPPROPERTY ( filegroup_name, property )  
```  
  
## <a name="arguments"></a>引数  
 *filegroup_name*  
`FILEGROUPPROPERTY` によって名前付けされたプロパティ情報が返されるファイル グループの名前を表す、**sysname** 型の式を指定します。  
  
 *property*  
ファイル グループのプロパティの名前を返す **varchar(128)** 型の式を指定します。 *property* によって返される値は次のいずれかです。  
  
|[値]|[説明]|返される値|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|ファイル グループが読み取り専用であるかどうかを示します。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 無効な入力です。|  
|**IsUserDefinedFG**|ファイル グループはユーザー定義のファイル グループです。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 無効な入力です。|  
|**IsDefault**|ファイルは既定のファイル グループです。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 無効な入力です。|  
  
## <a name="return-types"></a>戻り値の型  
**int**  
  
## <a name="remarks"></a>Remarks  
*filegroup_name* は、**sys.filegroups** カタログ ビューの **name** 列に対応します。  
  
## <a name="examples"></a>使用例  
この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内のプライマリ ファイル グループに対する `IsDefault` プロパティの設定値が返されます。  
  
```  
SELECT FILEGROUPPROPERTY('PRIMARY', 'IsDefault') AS 'Default Filegroup';  
GO  
```  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Default Filegroup   
---------------------   
1  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [FILEGROUP_ID &#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [FILEGROUP_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
