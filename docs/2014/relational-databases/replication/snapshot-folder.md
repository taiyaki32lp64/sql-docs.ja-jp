---
title: '[スナップショット フォルダー] | Microsoft Docs'
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4346b7752c9d4ace22a50cb1b4768c0c7d5df1fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676522"
---
# <a name="snapshot-folder"></a>[スナップショット フォルダー]
  ディストリビューションの構成ウィザードとパブリケーションの新規作成ウィザードには、 **[スナップショット フォルダー]** ページが表示されます。 このウィザードで有効にしたすべてのパブリッシャーでは、このページで指定したスナップショット フォルダーの場所が既定で使用されます (後から **[ディストリビューターのプロパティ]** ダイアログ ボックスを使用して有効にしたパブリッシャーには、この既定のスナップショット フォルダーが適用されません)。 ディストリビューションの構成ウィザードまたは **[ディストリビューターのプロパティ]** ダイアログ ボックスの **[パブリッシャー]** ページで、この既定をオーバーライドできます。  
  
 スナップショット フォルダーは、共有として指定したディレクトリです。このフォルダーの読み取りと書き込みをするエージェントには、このフォルダーへのアクセスを可能にする十分な権限が必要です。 フォルダーの適切なセキュリティ保護の詳細については、「[スナップショット フォルダーのセキュリティ保護](security/secure-the-snapshot-folder.md)」を参照してください。 レプリケーションを実装する前に、レプリケーション エージェントがスナップショット フォルダーに接続できることをテストします。 各エージェントで使用されるアカウントを使用してログオンした後、スナップショット フォルダーへのアクセスを試行します。  
  
## <a name="options"></a>および  
 **Snapshot folder**  
 スナップショット ファイルを保存するフォルダーのパスを入力します。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] はスナップショット フォルダーの場所に、ネットワーク共有を使用することをお勧めします。 ローカル パス (C:\\ など、ドライブ文字で始まるパス) を使用した場合、他のコンピューター上のエージェントがアクセスできません。  
  
## <a name="see-also"></a>参照  
 [スナップショット フォルダーの代替位置](alternate-snapshot-folder-locations.md)   
 [[ディストリビューションの構成]](configure-distribution.md)   
 [パブリッシングとディストリビューションの構成](configure-publishing-and-distribution.md)   
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](view-and-modify-distributor-and-publisher-properties.md)   
 [スナップショットを使用したサブスクリプションの初期化](initialize-a-subscription-with-a-snapshot.md)  
  
  
