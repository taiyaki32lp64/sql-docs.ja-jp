---
title: '@@CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b614ba90bddad592bedbf67e82d250ea8ba51e25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132079"
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

この関数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最後に開始された後に試行された接続数 (成功と失敗の両方) を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>戻り値の型
**整数 (integer)**
  
## <a name="remarks"></a>Remarks  
接続の数はユーザーの数とは異なります。 たとえば、アプリケーションでは、ユーザーがこれらの接続を監視することなく、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への複数の接続を開くことができます。
  
接続試行回数など、いくつかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計情報を含むレポートを表示するには、**sp_monitor** を実行します。
  
@@MAX_CONNECTIONS は、サーバーに対する同時接続の最大許容数です。 @@CONNECTIONS はログインが試行されるたびに増えるため、@@CONNECTIONS は @@MAX_CONNECTIONS を超える可能性があります。
  
## <a name="examples"></a>使用例  
この例では、現在の日付と時刻のログイン試行回数を返します。
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>参照
[システム統計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md):
  
  
