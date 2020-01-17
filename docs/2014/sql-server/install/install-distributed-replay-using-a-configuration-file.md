---
title: 構成ファイルを使用して分散再生のインストール |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3259232c-6963-4c9c-9d10-ae42aa262eef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9db8127a9a43478d891d5955190bd594fb6647b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094581"
---
# <a name="install-distributed-replay-using-a-configuration-file"></a>構成ファイルを使用した 分散再生のインストール
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップには、ユーザー入力およびシステムの既定値に基づいて構成ファイルを生成する機能が用意されています。 管理ツールをインストールするように指定すると、構成ファイルを使用して、3 つの 分散再生コンポーネント (管理ツール、分散再生コントローラー、および分散再生クライアント) を配置できます。 SQL Server セットアップでは、分散再生ユーティリティ コンポーネントのインストール、修復、およびアンインストールがサポートされています。  
  
 セットアップでは、コマンド ラインからのみ構成ファイルを使用できます。 以下に、構成ファイルを使用する際のパラメーターの処理順序について説明します。  
  
-   構成ファイルによって、パッケージの既定値が上書きされます。  
  
-   コマンド ライン値によって、構成ファイル内の値が上書きされます。  
  
 構成ファイルを使用する方法の詳細については、次を参照してください。 [SQL Server 2014 を使用したインストール、構成ファイル](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)します。  
  
> [!IMPORTANT]  
>  分散再生をインストールした後、コントローラー コンピューターとクライアント コンピューターのファイアウォール ルールを作成し、ターゲット サーバー上で各クライアント コンピューターの権限を付与する必要があります。 詳細については、「 [インストール後の手順の実行](../../tools/distributed-replay/complete-the-post-installation-steps.md)」を参照してください。  
  
### <a name="to-generate-a-configuration-file"></a>構成ファイルを生成するには  
  
1.  セットアップ ウィザードに従って **[インストールの準備完了]** ページまで進みます。 構成ファイルのパスは、 **[インストールの準備完了]** ページの [構成ファイルのパス] セクションで指定します。  
  
2.  INI ファイルを生成するには、インストールを実際に完了しなくてもセットアップを取り消します。  
  
### <a name="to-install-distributed-replay-using-the-configuration-file"></a>構成ファイルを使用して 分散再生をインストールするには  
  
-   コマンド プロンプトからインストールを実行し、ConfigurationFile パラメーターを使用して ConfigurationFile.ini を指定します。  
  
 **サンプル構文**  
  
 次の例では、コマンド プロンプトで構成ファイルを指定する方法を示しています。  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  構成ファイルでパスワードを構成することはできないため、コマンドラインで両方のパスワードを指定する必要があります。  
  
  
