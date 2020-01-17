---
title: SQL Server リソースへの依存関係の追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: dfaad71ac357ed261643267c7eab019b91548fa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063823"
---
# <a name="add-dependencies-to-a-sql-server-resource"></a>SQL Server リソースへの依存関係の追加
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、フェールオーバー クラスター マネージャー スナップインを使用して、AlwaysOn フェールオーバー クラスター インスタンス (FCI) リソースに依存関係を追加する方法について説明します。 フェールオーバー クラスター マネージャー スナップインは、Windows Server フェールオーバー クラスタリング (WSFC) サービスのクラスター管理アプリケーションです。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#Restrictions)、[前提条件](#Prerequisites)  
  
-   **SQL Server リソースに依存関係を追加するには、次のものを使用します:** [Windows フェールオーバー クラスター マネージャー](#WinClusManager)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループに他のリソースを追加する場合、そのリソースには必ず独自の固有の SQL ネットワーク名リソースと独自の SQL IP アドレス リソースが必要であることに注意してください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]以外の既存の SQL ネットワーク名リソースおよび SQL IP アドレス リソースを使用しないでください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースが他のリソースと共有されると、次の問題が発生する場合があります。  
  
-   予期しない障害が発生する。  
  
-   サービス パックを正常にインストールできない。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムが正常に実行されない。 この問題が発生した場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の追加インスタンスをインストールしたり、定期的なメンテナンスを実行したりできません。  
  
 さらに次の問題も考慮してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションを使用した FTP: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションで FTP を使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスでは、FTP サービスを使用するように設定された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストールと同じ物理ディスクのいずれかを、ご利用の FTP サービスで使用する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースの依存関係: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループにリソースを追加し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を使用できるようにするために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースに依存している場合は、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] エージェント リソースに依存関係を追加することを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はお勧めしています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースに依存関係を追加しないでください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターで高い可用性を維持するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント リソースに障害が発生した場合に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループが影響を受けないように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント リソースを構成します。  
  
-   ファイル共有とプリンター リソース: ファイル共有リソースやプリンター クラスター リソースをインストールするときは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターと同じ物理ディスク リソースに配置しないでください。 同じ物理ディスク リソースにインストールすると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を実行しているコンピューターのパフォーマンスが低下したり、サービスが失われたりする場合があります。  
  
-   MS DTC の考慮事項: オペレーティング システムをインストールし FCI を構成してから、フェールオーバー クラスター マネージャー スナップインを使用して、クラスター内で機能するように [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) を構成する必要があります。 MS DTC のクラスター化に失敗しても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは中断しませんが、MS DTC が適切に構成されていない場合は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のアプリケーション機能に影響が生じる可能性があります。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループに MS DTC をインストールし、MS DTC に依存する他のリソースがある場合は、このグループがオフラインまたはフェールオーバー中であると、MS DTC を使用できません。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、可能であれば、独自の物理ディスク リソースがある独自のグループに MS DTC を配置することをお勧めします。  
  
###  <a name="Prerequisites"></a> 前提条件  
 複数のディスク ドライブで構成される WSFC リソース グループに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールし、いずれかのドライブにデータを保存するように選択すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースはそのドライブにのみ依存するように設定されます。 別のディスクにデータやログを保存するには、まず、そのディスクに対する依存関係を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースに追加する必要があります。  
  
##  <a name="WinClusManager"></a> フェールオーバー クラスター マネージャー スナップインの使用  
 **SQL Server リソースに依存関係を追加するには**  
  
-   フェールオーバー クラスター マネージャー スナップインを開きます。  
  
-   依存させる適切な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースが含まれているグループを検索します。  
  
-   ディスクのリソースがこのグループに既にある場合は、手順 4. に進みます。 それ以外の場合は、ディスクが含まれるグループを見つけます。 そのグループと、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が含まれているグループが同じノードに所有されていない場合は、ディスクのリソースが含まれているグループを、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループを所有するノードに移動します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースを選択し、 **[プロパティ]** ダイアログ ボックスを開きます。 **[依存関係]** タブを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 依存関係のセットにディスクを追加します。  
  
  
