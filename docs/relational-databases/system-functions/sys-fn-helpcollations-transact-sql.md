---
title: sys.fn_helpcollations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_helpcollations
- fn_helpcollations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_helpcollations function
- collations [SQL Server], supported
- fn_helpcollations function
ms.assetid: b5082e81-1fee-4e2c-b567-5412eaee41c1
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016|| = azure-sqldw-latest ||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee626b9eef8cf2f2e80217b2a3709271a227f293
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906121"
---
# <a name="sysfnhelpcollations-transact-sql"></a>sys.fn_helpcollations (TRANSACT-SQL)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  サポートされているすべての照合順序の一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
fn_helpcollations ()  
```  
  
## <a name="tables-returned"></a>返されるテーブル

 **fn_helpcollations**次の情報を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|名前|**sysname**|標準の照合順序名。|  
|説明|**nvarchar(1000)**|照合順序の説明|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Windows 照合順序をサポートします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 限られた数もサポートしています (< 80) と呼ばれる照合順序の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する前に開発された照合順序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 照合順序をサポートします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序は、旧バージョンと互換性のためは引き続きサポートされますが、新しい開発作業のために使用しないでください。 Windows 照合順序について詳しくは、「[Windows 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)」をご覧ください。 照合順序の詳細については、「[Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」 (照合順序と Unicode のサポート) を参照してください。  
  
## <a name="examples"></a>使用例

 次の例は、文字で始まるすべての照合順序名を返します`L`バイナリ順の照合順序であるとします。

> [!Note]
> Fn_helpcollations() に対して azure SQL Data Warehouse のクエリは、master データベースで実行する必要があります。  
  
```sql  
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name like 'L%' AND Description LIKE '% binary sort';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Name                   Description  
 -------------------    ------------------------------------  
 Lao_100_BIN            Lao-100, binary sort  
 Latin1_General_BIN     Latin1-General, binary sort  
 Latin1_General_100_BIN Latin1-General-100, binary sort  
 Latvian_BIN            Latvian, binary sort  
 Latvian_100_BIN        Latvian-100, binary sort  
 Lithuanian_BIN         Lithuanian, binary sort  
 Lithuanian_100_BIN     Lithuanian-100, binary sort  
  
 (7 row(s) affected)  
 ```
  
## <a name="see-also"></a>関連項目

[COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
[COLLATIONPROPERTY &#40;TRANSACT-SQL&#41;](../../t-sql/functions/collation-functions-collationproperty-transact-sql.md)  
[Azure SQL Data Warehouse のデータベース照合順序のサポート](https://azure.microsoft.com/blog/database-collation-support-for-azure-sql-data-warehouse-2)  