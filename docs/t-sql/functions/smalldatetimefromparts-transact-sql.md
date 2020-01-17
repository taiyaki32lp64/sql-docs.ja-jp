---
title: SMALLDATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f18ee84c1bbb2234672d198923e93af4d99374f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907105"
---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  返します、 **smalldatetime** 指定した日付と時刻の値です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
```  
  
## <a name="arguments"></a>引数  
 *year*  
 年を指定する整数式。  
  
 *month*  
 月を指定する整数式。  
  
 *day*  
 日を指定する整数式。  
  
 *hour*  
 時間を指定する整数式。  
  
 *minute*  
 分を指定する整数式。  
  
## <a name="return-types"></a>戻り値の型  
 **smalldatetime**  
  
## <a name="remarks"></a>Remarks  
 この関数は、完全に初期化された **smalldatetime** 値のコンストラクターと同様に動作します。 引数が有効でない場合は、エラーがスローされます。 必須の引数が null の場合は、null が返されます。  
  
 この関数は、リモート処理は実行することのできる [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバー上とします。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 下のバージョンのサーバーには、リモート処理されません。  
  
## <a name="examples"></a>使用例  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2010-12-31 23:59:00  
  
(1 row(s) affected)  
```  
  

