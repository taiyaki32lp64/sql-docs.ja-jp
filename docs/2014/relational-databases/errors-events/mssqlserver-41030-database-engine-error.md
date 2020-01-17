---
title: MSSQLSERVER_41030 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 015a01f849bb00dd0db4c2f060447d63a2f96bc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914074"
---
# <a name="mssqlserver41030"></a>MSSQLSERVER_41030
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41030|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|OPEN_CLUSTER_SUB_KEY|  
|メッセージ テキスト|Windows Server フェールオーバー クラスタリング レジストリ サブキー '%.*ls' を開くことができませんでした (エラー コード %d)。  親キーはクラスター ルート キーです。  WSFC サービスは実行されていないか、現在の状態でアクセスできない可能性があります。または、指定された引数が無効です。 対応する可用性グループが削除されている場合、このエラーが発生します。 このエラー コードの詳細については、Windows 開発ドキュメントの「システム エラー コード」を参照してください。|  
  
## <a name="explanation"></a>説明  
 WSFC クラスターが破棄されると、[!INCLUDE[ssHADR](../../includes/sshadr-md.md)] に関連するすべてのレジストリ キーが削除されます。  
  
## <a name="user-action"></a>ユーザーの操作  
 WSFC クラスターを再作成した後、AlwaysOn が有効になっている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの各クラスター ノードで AlwaysOn を無効にし、再度有効にします。 この作業には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用できます。  
  
## <a name="see-also"></a>関連項目  
 [有効にして、AlwaysOn 可用性グループを無効にする&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
