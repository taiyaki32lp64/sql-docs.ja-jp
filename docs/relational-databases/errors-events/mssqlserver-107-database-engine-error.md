---
title: MSSQLSERVER_107 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 107 (Database Engine error)
ms.assetid: f33f514c-56aa-42e2-841b-e91244da90e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 473d752109ce90476602a0a60d7f6f5263caac09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060593"
---
# <a name="mssqlserver_107"></a>MSSQLSERVER_107
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|107|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|P_NOCORRMATCH|  
|メッセージ テキスト|列プレフィックス '%.*ls' とクエリで使用されているテーブル名または別名が一致しません。|  
  
## <a name="explanation"></a>説明  
クエリの選択リストに、不適切な列プレフィックスで修飾されたアスタリスク (*) が含まれています。 このエラーは、次のような状況で返される可能性があります。  
  
-   列プレフィックス '%.*ls' とクエリで使用されているテーブル名または別名が一致しない。 たとえば、次のステートメントでは、FROM 句で定義していない別名 (`T1`) を列プレフィックスとして使用しています。  
  
    ```  
    SELECT T1.* FROM dbo.ErrorLog;  
    ```  
  
-   FROM 句でテーブルの別名を指定しているときに、テーブル名を列プレフィックスとして指定している。 たとえば、次のステートメントでは、FROM 句でテーブルの別名 (`ErrorLog`) を定義しているにもかかわらず、テーブル名 `T1` を列プレフィックスとして使用しています。  
  
    ```  
    SELECT ErrorLog.* FROM dbo.ErrorLog AS T1;  
    ```  
  
    FROM 句でテーブルの別名を指定した場合、テーブルの列のプレフィックスとして使用できるのはその別名だけです。  
  
## <a name="user-action"></a>ユーザーの操作  
列プレフィックスとクエリの FROM 句で指定したテーブル名または別名を一致させます。 たとえば、上記のステートメントは次のように修正できます。  
  
```  
SELECT T1.* FROM dbo.ErrorLog AS T1;  
```  
  
内の複数の  
  
```  
SELECT ErrorLog.* FROM dbo.ErrorLog;  
```  
  
## <a name="see-also"></a>参照  
[MSSQLSERVER_4104](~/relational-databases/errors-events/mssqlserver-4104-database-engine-error.md)  
  
