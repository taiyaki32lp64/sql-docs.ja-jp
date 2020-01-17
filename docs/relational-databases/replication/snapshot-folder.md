---
title: '[スナップショット フォルダー] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 92abee758d5eda99aebddc874550eb9cd2e87ca5
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769510"
---
# <a name="snapshot-folder"></a>[スナップショット フォルダー]
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

ディストリビューションの構成ウィザードとパブリケーションの新規作成ウィザードには、 **[スナップショット フォルダー]** ページが表示されます。 このウィザードで有効にしたすべてのパブリッシャーでは、このページで指定したスナップショット フォルダーの場所が既定で使用されます (後から **[ディストリビューターのプロパティ]** ダイアログ ボックスを使用して有効にしたパブリッシャーには、この既定のスナップショット フォルダーが適用されません)。 ディストリビューションの構成ウィザードまたは **[ディストリビューターのプロパティ]** ダイアログ ボックスの **[パブリッシャー]** ページで、この既定をオーバーライドできます。  
  
スナップショット フォルダーは、共有として指定したディレクトリです。このフォルダーの読み取りと書き込みをするエージェントには、このフォルダーへのアクセスを可能にする十分な権限が必要です。 フォルダーの適切なセキュリティ保護の詳細については、「[Secure the Snapshot Folder](../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。 レプリケーションを実装する前に、レプリケーション エージェントがスナップショット フォルダーに接続できることをテストします。 各エージェントで使用されるアカウントを使用してログオンした後、スナップショット フォルダーへのアクセスを試行します。  

Azure SQL Database マネージド インスタンスの場合、スナップショット フォルダーは Azure ファイル共有である必要があります。 
  
## <a name="options"></a>オプション  
 **Snapshot folder**  
 スナップショット ファイルを保存するフォルダーのパスを入力します。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] はスナップショット フォルダーの場所に、ネットワーク共有を使用することをお勧めします。 ローカル パス (C:\\ など、ドライブ文字で始まるパス) を使用した場合、他のコンピューター上のエージェントがアクセスできません。  
  
## <a name="see-also"></a>参照  
 [スナップショット オプションの変更](../../relational-databases/replication/snapshot-options.md)   
 [[ディストリビューションの構成]](../../relational-databases/replication/configure-distribution.md)   
 [パブリッシングとディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [スナップショットを使用したサブスクリプションの初期化](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
