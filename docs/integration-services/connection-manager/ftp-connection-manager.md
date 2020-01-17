---
title: FTP 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0f1380370862b735e00799cbcb6a9ba46d69fd3f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294423"
---
# <a name="ftp-connection-manager"></a>FTP 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  FTP 接続マネージャーを使用すると、パッケージは、ファイル転送プロトコル (FTP) サーバーに接続できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる FTP タスクでは、この接続マネージャーを使用します。  
  
 FTP 接続マネージャーをパッケージに追加すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時に FTP 接続として解決される接続マネージャーを作成し、接続マネージャーのプロパティを設定し、接続マネージャーをパッケージの **Connections** コレクションに追加します。  
  
 接続マネージャーの **ConnectionManagerType** プロパティは、 **FTP**に設定されます。  
  
 FTP 接続マネージャーは、次の方法で構成できます。  
  
-   サーバー名とサーバー ポートを指定します。  
  
-   匿名アクセスを指定するか、または基本認証のユーザー名とパスワードを指定します。  
  
    > [!IMPORTANT]  
    >  FTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
-   タイムアウト、再試行回数、および一度にコピーするデータ量を指定します。  
  
-   FTP 接続マネージャーでパッシブ モードを使用するか、アクティブ モードを使用するかを指定します。  
  
 FTP 接続マネージャーの接続先である FTP サイトの構成によっては、接続マネージャーの次の既定値の変更が必要になる場合があります。  
  
-   サーバー ポートは 21 に設定されています。 FTP サイトがリッスンするポートを指定する必要があります。  
  
-   ユーザー名は "anonymous" に設定されています。 FTP サイトで必要になる資格情報を指定する必要があります。  
  
## <a name="activepassive-modes"></a>アクティブ/パッシブ モード  
 FTP 接続マネージャーは、アクティブ モードまたはパッシブ モードのどちらかを使用して、ファイルを送受信できます。 アクティブ モードでは、サーバーがデータ接続を開始し、パッシブ モードでは、クライアントがデータ接続を開始します。  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>FTP 接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティについては、「 [[FTP 接続マネージャー エディター]](../../integration-services/connection-manager/ftp-connection-manager-editor.md)」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="ftp-connection-manager-editor"></a>FTP 接続マネージャー エディター
  **[FTP 接続マネージャー エディター]** ダイアログ ボックスを使用すると、FTP サーバーに接続するためのプロパティを指定できます。  
  
> [!IMPORTANT]  
>  FTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 FTP 接続マネージャーの詳細については、「 [FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **サーバー名**  
 FTP サーバーの名前を指定します。  
  
 **[サーバー ポート]**  
 接続に使用する FTP サーバーのポート番号を指定します。 このプロパティの既定値は **21**です。  
  
 **User name**  
 FTP サーバーにアクセスするために使用するユーザー名を指定します。 このプロパティの既定値は **anonymous**です。  
  
 **パスワード**  
 FTP サーバーにアクセスするために使用するパスワードを指定します。  
  
 **[タイムアウト (秒)]**  
 タスクがタイムアウトするまでの秒数を指定します。この値に **0** を指定すると、時間は無制限になります。 このプロパティの既定値は **60**です。  
  
 **[パッシブ モードを使用する]**  
 サーバーまたはクライアントのどちらが接続を開始するかを指定します。 アクティブ モードではサーバーが接続を開始し、パッシブ モードではクライアントが接続を開始します。 このプロパティの既定値は **アクティブ モード**です。  
  
 **[再試行の回数]**  
 接続を試行する回数を指定します。 値 **0** は、無制限に再試行を行うことを示します。  
  
 **[チャンク サイズ (KB)]**  
 データを転送するためのチャンク サイズを KB 単位で指定します。  
  
 **[接続テスト]**  
 FTP 接続マネージャーを構成した後に、 **[接続テスト]** をクリックして、接続が利用可能であることを確認します。  
  
## <a name="see-also"></a>参照  
 [FTP タスク](../../integration-services/control-flow/ftp-task.md)   
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
