---
title: SQL Server フェールオーバー クラスターでのレポート サーバー データベースのホスト | Microsoft Docs
ms.date: 03/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: edef2cd21dacb5911a37a6a1f46afd17e76e57be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62513614"
---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>SQL Server フェールオーバー クラスターでのレポート サーバー データベースのホスト
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して複数のディスクを使用できるように、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、フェールオーバー クラスタリングをサポートしています。 フェールオーバー クラスタリングは、レポート サーバー データベースでのみサポートされています。つまり、フェールオーバー クラスターの一部としてレポート サーバー サービスを実行することはできません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターでレポート サーバー データベースをホストするには、クラスターを事前にインストールして構成しておく必要があります。 その後、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールの [データベースのセットアップ] ページでレポート サーバー データベースを作成するときに、そのフェールオーバー クラスターをサーバー名として選択できます。  
  
 レポート サーバー サービスはフェールオーバー クラスターに参加できませんが、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] フェールオーバー クラスターをインストールしたコンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールできます。 レポート サーバーは、フェールオーバー クラスターとは別に実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー インスタンスの一部であるコンピューターにレポート サーバーをインストールした場合、レポート サーバー データベースにフェールオーバー クラスターを使用する必要はありません。別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用してデータベースをホストできます。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー データベース &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [レポート サーバー データベースの作成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
  
