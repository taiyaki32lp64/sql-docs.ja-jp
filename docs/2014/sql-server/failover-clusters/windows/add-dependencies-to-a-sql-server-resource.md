---
title: SQL Server リソースへの依存関係の追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- resource dependencies [SQL Server]
- failover clustering [SQL Server], dependencies
- clusters [SQL Server], dependencies
- dependencies [SQL Server], clustering
ms.assetid: 25dbb751-139b-4c8e-ac62-3ec23110611f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a29577d6027c43fd35a8b27db8b402123c89a4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035669"
---
# <a name="add-dependencies-to-a-sql-server-resource"></a>SQL Server リソースへの依存関係の追加
  このトピックでは、フェールオーバー クラスター マネージャー スナップインを使用して、AlwaysOn フェールオーバー クラスター インスタンス (FCI) リソースに依存関係を追加する方法について説明します。 フェールオーバー クラスター マネージャー スナップインは、Windows Server フェールオーバー クラスタリング (WSFC) サービスのクラスター管理アプリケーションです。  
  
-   **作業を開始する準備:** [制限事項と制約](#Restrictions)、[の前提条件](#Prerequisites)  
  
-   **SQL Server リソースに依存関係を追加するを使用します。** [Windows フェールオーバー クラスター マネージャー](#WinClusManager)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループに他のリソースを追加する場合、そのリソースには必ず独自の固有の SQL ネットワーク名リソースと独自の SQL IP アドレス リソースが必要であることに注意してください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]以外の既存の SQL ネットワーク名リソースおよび SQL IP アドレス リソースを使用しないでください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースが他のリソースと共有されると、次の問題が発生する場合があります。  
  
-   予期しない障害が発生する。  
  
-   サービス パックを正常にインストールできない。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムが正常に実行されない。 この問題が発生した場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の追加インスタンスをインストールしたり、定期的なメンテナンスを実行したりできません。  
  
 さらに次の問題も考慮してください。  
  
-   FTP[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]レプリケーション。インスタンスの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で FTP を使用する[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]レプリケーションでは、FTP サービスする必要がありますを使用して、同じ物理ディスクの 1 つのインストールと[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]FTP サービスを使用して設定します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースの依存関係:リソースを追加する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]グループと依存関係を持って、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ことを確認するリソース[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]が使用可能な[!INCLUDE[msCoName](../../../includes/msconame-md.md)]に依存関係を追加することをお勧めします、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]エージェントのリソース。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースに依存関係を追加しないでください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターで高い可用性を維持するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント リソースに障害が発生した場合に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループが影響を受けないように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント リソースを構成します。  
  
-   ファイル共有とプリンター リソース:ファイル共有リソースやプリンター クラスター リソースをインストールするときに、必要がありますに配置を実行しているコンピューターと同じ物理ディスク リソース[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。 同じ物理ディスク リソースにインストールすると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を実行しているコンピューターのパフォーマンスが低下したり、サービスが失われたりする場合があります。  
  
-   MS DTC の考慮事項:構成する必要があります、オペレーティング システムをインストールし、FCI の構成後[!INCLUDE[msCoName](../../../includes/msconame-md.md)]分散トランザクション コーディネーター (MS DTC)、フェールオーバー クラスター マネージャー スナップインを使用してクラスターで動作します。 MS DTC のクラスター化に失敗しても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは中断しませんが、MS DTC が適切に構成されていない場合は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のアプリケーション機能に影響が生じる可能性があります。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループに MS DTC をインストールし、MS DTC に依存する他のリソースがある場合は、このグループがオフラインまたはフェールオーバー中であると、MS DTC を使用できません。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、可能であれば、独自の物理ディスク リソースがある独自のグループに MS DTC を配置することをお勧めします。  
  
###  <a name="Prerequisites"></a> 前提条件  
 複数のディスク ドライブで構成される WSFC リソース グループに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールし、いずれかのドライブにデータを保存するように選択すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースはそのドライブにのみ依存するように設定されます。 別のディスクにデータやログを保存するには、まず、そのディスクに対する依存関係を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースに追加する必要があります。  
  
##  <a name="WinClusManager"></a> フェールオーバー クラスター マネージャー スナップインの使用  
 **SQL Server リソースに依存関係を追加するには**  
  
-   フェールオーバー クラスター マネージャー スナップインを開きます。  
  
-   依存させる適切な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースが含まれているグループを検索します。  
  
-   ディスクのリソースがこのグループに既にある場合は、手順 4. に進みます。 それ以外の場合は、ディスクが含まれるグループを見つけます。 そのグループと、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が含まれているグループが同じノードに所有されていない場合は、ディスクのリソースが含まれているグループを、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループを所有するノードに移動します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースを選択し、 **[プロパティ]** ダイアログ ボックスを開きます。 **[依存関係]** タブを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 依存関係のセットにディスクを追加します。  
  
  
