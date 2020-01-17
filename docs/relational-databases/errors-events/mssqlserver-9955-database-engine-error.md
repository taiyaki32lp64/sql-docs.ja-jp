---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5b286b790370abcb049daee16cb417bdb9299c80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903802"
---
# <a name="mssqlserver9955"></a>MSSQLSERVER_9955
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|9955|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|FTXT2_MSSEARCHACCESSDENY|  
|メッセージ テキスト|SQL Server は、名前付きパイプ '%ls' を作成して、フルテキスト フィルター デーモンと通信することができませんでした (Windows エラー: %d)。 フィルター デーモン ホスト プロセス用の名前付きパイプが既に存在するか、システムのリソースが不足しているか、またはフィルター デーモン アカウント グループのセキュリティ ID 番号 (SID) の検索に失敗したかのいずれかです。 このエラーを解決するには、実行中のフルテキスト フィルター デーモン プロセスをすべて終了し、必要に応じて、フルテキスト デーモン ランチャー サービス アカウントを再構成してください。|  
  
## <a name="explanation"></a>説明  
このメッセージは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がフルテキスト フィルター デーモンと通信するための名前付きパイプを作成できなかったことが原因で表示されます。 フィルター デーモン ホスト プロセス用の名前付きパイプが既に存在するか、システムのリソースが不足しているか、またはフィルター デーモン アカウント グループのセキュリティ ID 番号 (SID) の検索に失敗したかのいずれかです。  
  
## <a name="user-action"></a>ユーザーの操作  
このエラーを解決するには、実行中のフルテキスト フィルター デーモン プロセスをすべて終了し、必要に応じて SQL Server 構成マネージャーを使用してフルテキスト デーモン ホスト アカウントを再構成します。  
  
## <a name="see-also"></a>参照  
[SQL Server 構成マネージャー](~/relational-databases/sql-server-configuration-manager.md)  
[フルテキスト フィルター デーモン ランチャーのサービス アカウントの設定](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[フルテキスト検索](~/relational-databases/search/full-text-search.md)  
  
