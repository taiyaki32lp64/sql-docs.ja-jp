---
title: '[MSSQLSERVER のプロトコルのプロパティ] ダイアログ ボックス ([フラグ] タブ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 4d38e6e9-f95f-4e79-ae45-89f631037528
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c14273ab80c955536d8e4f754c7af48355547b96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058469"
---
# <a name="protocols-for-mssqlserver-properties-flags-tab"></a>[MSSQLSERVER のプロトコルのプロパティ] ダイアログ ボックス ([フラグ] タブ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  サーバーに証明書がインストールされている場合、 **[MSSQLSERVER のプロトコルのプロパティ]** ダイアログ ボックスの **[フラグ]** タブを使用して、プロトコルの暗号化の表示や指定を行います。インスタンス オプションを非表示に設定することもできます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の設定を有効または無効にするには、 **[ForceEncryption]** を再起動する必要があります。  
  
 接続を暗号化するには、証明書を付けて [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] を提供する必要があります。 証明書がインストールされていない場合、インスタンスが起動されると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により自己署名入りの証明書が生成されます。 この自己署名入りの証明書は、信頼されている証明機関から発行された証明書の代わりに使用することはできますが、この証明書では認証機能や否認不可機能は提供されません。  
  
> [!CAUTION]  
>  自己署名入りの証明書を使用して暗号化された SSL (Secure Sockets Layer) 接続では、強力なセキュリティは提供されません。 このような接続では、man-in-the-middle アタックによる被害を受けやすくなります。 実稼働環境やインターネットに接続しているサーバーでは、自己署名入りの証明書を使用した SSL 接続は使用しないことをお勧めします。  
  
 暗号化の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続の暗号化」をご覧ください。  
  
 ログイン プロセスは常に暗号化されます。 **[ForceEncryption]** が **[はい]** に設定されているときは、クライアントとサーバーのすべての接続が暗号化されます。そのため、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] に対するクライアント接続は、サーバー証明書のルート機関を信頼するように構成する必要があります。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[!INCLUDE[ssDE](../../includes/ssde-md.md)] への暗号化接続を有効にする方法 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー)」をご覧ください。  
  
## <a name="cluster-servers"></a>クラスター サーバー  
 フェールオーバー クラスターで暗号化を使用する場合は、フェールオーバー クラスター内のすべてのノードに対して、仮想サーバーの完全に修飾された DNS 名でサーバー証明書をインストールする必要があります。 たとえば、"test1. *\<your company>* .com" および "test2. *\<your company>* .com" というノードを持つ 2 ノードのクラスターと、"virtsql" という仮想サーバーがあるとします。この場合、"virtsql. *\<your company>* .com" の証明書を両方のノードにインストールする必要があります。 その後、 **SQL Server 構成マネージャー** で **[ForceEncryption]** チェック ボックスをオンにすれば、フェールオーバー クラスターの暗号化を構成できます。  
  
## <a name="options"></a>オプション  
 **[ForceEncryption]**  
 プロトコルを強制的に暗号化します。 暗号化とは、データを読み取り不可能な形式に変更することにより、秘密情報を保護する方法です。 仮に転送プロセスで転送パケットが閲覧されることがあっても、暗号化していればデータは安全です。 チャネル バインドを使用するには、 **[強制的に暗号化]** を **[オン]** に設定し、 **[詳細設定]** タブで **[拡張保護]** を構成します。  
  
 **[HideInstance]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [参照] **ボタンを使用してこの** インスタンスを表示しようとするクライアントに対してこのインスタンスを公開しません。 サーバー上の名前付きのインスタンスの場合、接続するには、クライアント アプリケーションはプロトコル エンドポイント情報を指定する必要があります。 たとえば、 **tcp:server,5000**など、ポート番号または名前付きパイプ名を指定します。 詳しくは、「 [Logging In to SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)」をご覧ください。  
  
 詳細については、オンライン ブックの「データベース エンジンへの暗号化接続を有効にする方法 (構成マネージャー)」を参照してください。  
  
  
