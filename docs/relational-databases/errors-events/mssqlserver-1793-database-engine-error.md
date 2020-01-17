---
title: MSSQLSERVER_1793 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f1c1e83836ad9e6312d33e64c48810ec3f10c9d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137192"
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1793|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|FILESTREAM_BASEDATA_NEED_SAME_PARTITION|  
|メッセージ テキスト|パーティション構成が FILESTREAM データに指定されていないため、操作 (インデックス '%.*ls' の削除) を実行できません。|  
  
## <a name="explanation"></a>説明  
このメッセージは、FILESTREAM データを含むテーブルで、クラスター化インデックスの削除を実行する場合に、基本データに **MOVE TO** 句を指定したにもかかわらず、FILESTREAM データに **FILESTREAM_ON** 句が指定されていないときに表示されます。  
  
## <a name="user-action"></a>ユーザーの操作  
FILESTREAM データを含むテーブルで、クラスター化インデックスを削除する場合は、次のオプションのどちらかを使用します。  
  
-   基本データに **MOVE TO** 句、FILESTREAM データに **FILESTREAM_ON** 句の両方を指定します。  
  
-   基本データに **MOVE TO** 句、FILESTREAM データに **FILESTREAM_ON** 句の両方とも指定しません。  
  
次の例は、基本データにパーティション構成が指定されているにもかかわらず、FILESTREAM データには指定されているので、失敗します。  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
次の例は、基本データに **MOVE TO** 句、FILESTREAM データに **FILESTREAM_ON** 句の両方が指定されているので、成功します。  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
次の例は、基本データに **MOVE TO** 句、FILESTREAM データに **FILESTREAM_ON** 句の両方とも指定されていないので、成功します。  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  
