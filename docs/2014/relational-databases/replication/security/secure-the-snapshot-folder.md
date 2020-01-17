---
title: スナップショット フォルダーのセキュリティ保護 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], security
ms.assetid: 3cd877d1-ffb8-48fd-a72b-98eb948aad27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3612a8b2006978a8098a406a6557d6c9f0f1f7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960489"
---
# <a name="secure-the-snapshot-folder"></a>スナップショット フォルダーのセキュリティ保護
  スナップショット フォルダーは、スナップショット ファイルが格納されるディレクトリです。このディレクトリは、スナップショットの格納専用に使用することをお勧めします。 スナップショット エージェントにこのフォルダーへの書き込み権限を許可し、マージ エージェントまたはディストリビューション エージェントがこのフォルダーへのアクセスに使用する Windows アカウントにのみ読み取り権限を許可します。 リモート コンピューターのスナップショット フォルダーにアクセスするには、エージェントに関連付けられている Windows アカウントがドメイン アカウントである必要があります。  
  
> [!NOTE]  
>  管理者はユーザー アカウント制御 (UAC) を使用して、自身の昇格したユーザーの権利 ( *権限*とも呼ばれる) を管理できます。 UAC が有効になっているオペレーティング システムで実行する場合は、管理者は管理者自身の管理権限を使用しません。 代わりに、標準ユーザー (管理者以外のユーザー) としてほとんどの操作を実行し、必要な場合にのみ一時的に管理権限を使用します。 UAC により、スナップショット共有への管理アクセスが妨げられる場合があります。 このため、スナップショット エージェント、ディストリビューション エージェント、およびマージ エージェントによって使用される Windows アカウントに、スナップショット共有の権限を明示的に与える必要があります。 この操作は、Windows アカウントが Administrators グループのメンバーである場合にも必要です。  
  
 ディストリビューションの構成ウィザードまたはパブリケーションの新規作成ウィザードを使用してディストリビューターを構成すると、スナップショット フォルダーの既定の場所は、X:\Program Files\Microsoft SQL Server\\ *\<instance>* \MSSQL\ReplData というローカル パスになります。 リモート ディストリビューターやプル サブスクリプションを使用する場合は、ローカル パスではなく UNC ネットワーク共有 (\\\\<*computername>* \snapshot など) を指定する必要があります。  
  
 スナップショット フォルダーへのアクセス許可を付与する方法は、フォルダーへのアクセス方法によって異なります。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Server 2003 では、次のダイアログ ボックス タブを使用します。  
  
-   ローカル パスを指定する場合は、フォルダーの **[プロパティ]** ダイアログ ボックスの **[セキュリティ]** タブを使用してアクセス許可を付与します。  
  
-   ネットワーク共有を指定する場合は、フォルダーの **[プロパティ]** ダイアログ ボックスの **[共有]** タブを使用してアクセス許可を付与します。  
  
    > [!NOTE]  
    >  ディストリビューター上でレプリケーション エージェントを実行する場合は、フォルダーの **[プロパティ]** ダイアログ ボックスの **[セキュリティ]** タブを使用して、エージェントの実行に使用する Windows アカウントにアクセス許可を付与してください。 ネットワーク共有を使用する場合も、この操作を行います。 また、パブリッシャーとディストリビューターが同じコンピューター上にある場合は、プッシュ サブスクリプションのマージ エージェントとディストリビューション エージェント、およびスナップショット エージェントに対してもこの操作を行ってください。  
  
 ローカル パスおよびネットワーク共有のアクセス許可の設定の詳細については、Windows のマニュアルを参照してください。  
  
> [!NOTE]  
>  パブリケーションが削除された場合、レプリケーションは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのセキュリティ コンテキストでスナップショット フォルダーを削除しようとします。 このアカウントに十分な権限がない場合は、十分な権限を持つアカウントでログインして、手動でフォルダーを削除してください。 フォルダーを削除するには、ローカル パスの場合は **変更** 特権が、ネットワーク共有の場合は **フル コントロール** 特権が必要です。  
  
## <a name="delivering-snapshots-through-ftp"></a>FTP によるスナップショットの配信  
 セキュリティの観点から、スナップショットは UNC 共有に格納することをお勧めします。ただし、スナップショットを FTP 共有に格納して、FTP を使ってサブスクライバーに配信することもできます。 FTP サーバーを構成する際には、仮想ディレクトリが公開する UNC 共有で、パブリケーションのスナップショット エージェントによる書き込みアクセスが許可されていることを確認してください。  
  
 FTP でスナップショットを取得するようにサブスクライバーを構成するには、まず FTP サーバーで FTP のログインとパスワードを設定し、スナップショット ファイルをダウンロードできるようにサブスクライバーに読み取りアクセス ("get") を許可します。  
  
 FTP でスナップショットを配信する場合は、「[FTP でのスナップショットの配信](../publish/deliver-a-snapshot-through-ftp.md)」を参照してください。  
  
 FTP でスナップショットにアクセスするためのパスワードの設定と変更については、「 [Secure the Publisher](secure-the-publisher.md)」の「FTP スナップショット配信」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [スナップショット フォルダーの代替位置](../alternate-snapshot-folder-locations.md)   
 [Initialize a Subscription with a Snapshot (スナップショットを使用したサブスクリプションの初期化)](../initialize-a-subscription-with-a-snapshot.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [SQL Server レプリケーションのセキュリティ](view-and-modify-replication-security-settings.md)   
 [FTP によるスナップショットの転送](../transfer-snapshots-through-ftp.md)  
  
  
