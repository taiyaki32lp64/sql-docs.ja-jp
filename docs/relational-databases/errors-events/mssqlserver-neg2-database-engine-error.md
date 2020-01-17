---
title: MSSQLSERVER_-2 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "-2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 09a5cbc03debdb4fc87986111fb0ac69138715bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903762"
---
# <a name="mssqlserver-2"></a>MSSQLSERVER_-2
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|-2|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|タイムアウトが発生しました。  処理が完了する前にタイムアウト期間が経過したか、サーバーが応答していません。 (Microsoft SQL Server、エラー: -2)。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントがサーバーに接続できません。 このエラーは、サーバー上のファイアウォールで接続が拒否されたために発生する場合があります。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサーバー インスタンスで、接続を許可するようにファイアウォールを構成していることを確認します。  
  
## <a name="see-also"></a>参照  
[SQL Server のアクセスを許可するための Windows ファイアウォールの構成](~/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
[データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[クライアント プロトコルの構成](~/database-engine/configure-windows/configure-client-protocols.md)  
[ネットワーク プロトコルとネットワーク ライブラリ](~/sql-server/install/network-protocols-and-network-libraries.md)  
[クライアント ネットワーク構成](~/database-engine/configure-windows/client-network-configuration.md)  
[クライアント プロトコルの構成](~/database-engine/configure-windows/configure-client-protocols.md)  
[サーバー ネットワーク プロトコルの有効化または無効化](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
