---
title: フェールオーバー クラスター インスタンスの IP アドレスの変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- modifying IP addresses
- failover clustering [SQL Server], IP addresses
- IP addresses [SQL Server]
- clusters [SQL Server], IP addresses
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 93738cb12b13b5f7c6434acd7d7d86b5496d4fc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063790"
---
# <a name="change-the-ip-address-of-a-failover-cluster-instance"></a>フェールオーバー クラスター インスタンスの IP アドレスの変更
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、フェールオーバー クラスター マネージャー スナップインを使用して、Always On フェールオーバー クラスター インスタンス (FCI) の IP アドレス リソースを変更する方法について説明します。 フェールオーバー クラスター マネージャー スナップインは、Windows Server フェールオーバー クラスタリング (WSFC) サービスのクラスター管理アプリケーションです。  
  
-   **作業を開始する準備:** [セキュリティ](#Security)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 作業を開始する前に、次の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックのトピックを参照してください。[Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 FCI を保持または更新するには、FCI のすべてのノードにおいて、サービスとしてログオンする権限を持つローカル管理者である必要があります。  
  
##  <a name="WSFC"></a> フェールオーバー クラスター マネージャー スナップインの使用  
 **FCI の IP アドレス リソースを変更するには**  
  
1.  フェールオーバー クラスター マネージャー スナップインを開きます。  
  
2.  左側のペインで、 **[サービスとアプリケーション]** ノードを展開し、FCI をクリックします。  
  
3.  右側のペインの **[サーバー名]** カテゴリの下で、SQL Server インスタンスを右クリックし、 **[プロパティ]** をクリックして **プロパティ** ダイアログ ボックスを開きます。  
  
4.  **[全般]** タブで、IP アドレス リソースを変更します。  
  
5.  **[OK]** をクリックして、ダイアログ ボックスを閉じます。  
  
6.  右側のペインで、[SQL IP Address1 (フェールオーバー クラスターのインスタンス名)] を右クリックし、 **[オフラインにする]** をクリックします。 [SQL IP Address1 (フェールオーバー クラスターのインスタンス名)]、[SQL Network Name (フェールオーバー クラスターのインスタンス名)]、および [ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ] の状態が、[オンライン]、[オフライン待ち]、[オフライン] と変化していくのを確認できます。  
  
7.  右側のペインで、[ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]] を右クリックし、 **[オンラインにする]** をクリックします。 [SQL IP Address1 (フェールオーバー クラスターのインスタンス名)]、[SQL Network Name (フェールオーバー クラスターのインスタンス名)]、および [ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ] の状態が、[オフライン]、[オンライン待ち]、[オンライン] と変化していくのを確認できます。  
  
8.  フェールオーバー クラスター マネージャー スナップインを閉じます。  
  
  
