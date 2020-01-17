---
title: フェールオーバー クラスターでの FILESTREAM の設定 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], setting up on a failover cluster
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3ef524c6ee823b80b25fa5cf5ee4584ba8b8d00c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912196"
---
# <a name="set-up-filestream-on-a-failover-cluster"></a>フェールオーバー クラスターでの FILESTREAM の設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、フェールオーバー クラスターで FILESTREAM を有効にする方法について説明します。 この手順を実行する前に、 [フェールオーバー クラスタリング](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) について理解し、FILESTREAM を有効にしておく必要があります。 FILESTREAM を有効にする方法の詳細については、「 [FILESTREAM の有効化と構成](../../relational-databases/blob/enable-and-configure-filestream.md)」をご覧ください。  
  
### <a name="to-set-up-filestream-on-a-failover-cluster"></a>フェールオーバー クラスターで FILESTREAM を設定するには  
  
1.  フェールオーバー クラスターのプライマリ ノードを設定します。  
  
     設定が完了したら、 **SQL Server 構成マネージャー**を使用してプライマリ ノードで FILESTREAM を有効にします。 これにより、Windows Admin 権限を必要とする設定が有効になります。 リモート アクセスが必要な場合は、 **[リモート クライアントに FILESTREAM データへのストリーム アクセスを許可する]** を選択します。 これにより、ファイル共有クラスター リソースが作成されます。  
  
2.  パッシブ ノードを設定します。  
  
     設定が完了したら、 **SQL Server 構成マネージャー**を使用してパッシブ ノードで FILESTREAM を有効にします。 **[Windows 共有名]** に指定する名前は、クラスター内のすべてのノードで同じにする必要があります。  
  
3.  パッシブ ノードをさらに追加するには、手順 2. を繰り返します。  
  
4.  すべてのノードを追加したら、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各インスタンスで sp_configure ストアド プロシージャを実行して処理を完了します。  
  
5.  クラスターに別のノードを追加して有効にするには、いつでも手順 2.、3.、および 4. を繰り返します。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [SQL Server のフェールオーバー クラスター インスタンスの削除 &#40;セットアップ&#41;](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  
