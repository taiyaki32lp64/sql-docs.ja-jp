---
title: IsNull (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: aaae21e3a47465011f6644901d0ac886da6846f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930222"
---
# <a name="isnull-geography-data-type"></a>IsNull (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** インスタンスが NULL かどうかを指定するプロパティです。 インスタンスが NULL の場合は "TRUE" を、NULL ではない場合は 0 を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型: **bit**  
  
 CLR の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull` では、**geography** インスタンスが NULL かどうかをテストできます。 このテストの結果は若干複雑であるため注意してください。インスタンスが NULL でなければ 0 を返し、インスタンスが NULL であれば NULL を返します。  
  
 このメソッドは、主に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インフラストラクチャによって使用されます。**geography** インスタンスが NULL かどうかをテストするために T-SQL 述語の IS NULL を使用することをお勧めします。 T-SQL 述語の IS NULL の詳細については、「[IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
