---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 751b3615e8c54ab5899f64a6604c5a228c859879
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868688"
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|33027|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SEC_CRYPTOPROV_CANTLOADDLL|  
|メッセージ テキスト|Authenticode 署名またはファイル パスが無効なため、暗号プロバイダー '%.*ls' を読み込めませんでした。 前のメッセージでその他のエラーを確認してください。|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、エラー メッセージに表示されている暗号化サービス プロバイダーを使用できませんでした。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が該当する DLL を読み込めなかったことが原因です。 名前が無効であるか、Authenticode 署名が無効です。  
  
## <a name="user-action"></a>ユーザーの操作  
 このファイルが存在し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がファイルの場所にアクセスするための権限を持っていることを確認します。 エラー ログで、その他の関連メッセージを確認します。 または、暗号化サービス プロバイダーに詳細を問い合わせてください。  
  
  
