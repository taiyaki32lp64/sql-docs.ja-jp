---
title: SQL Server レプリケーションのインストール | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3fd70d208960af1f121795bfdf8a657ceaf59f21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775295"
---
# <a name="install-sql-server-replication"></a>SQL Server レプリケーションのインストール
  レプリケーション コンポーネントのインストールは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードまたはコマンド プロンプトを使用して行うことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールする場合、または既存のインスタンスを変更する場合はレプリケーションをインストールします。  
  
 レプリケーション コンポーネントのインストール後、レプリケーションを使用する前にサーバーを構成する必要があります。 詳細については、 [オンライン ブックの「](../../relational-databases/replication/configure-distribution.md) ディストリビューションの構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既存のインスタンスを変更するときにレプリケーション コンポーネントをインストールする場合は、インストール完了後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを停止して再起動する必要があります。 この操作により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがレプリケーション エージェント サブシステムを認識し、ジョブ ステップからレプリケーション エージェントを呼び出すことができるようになります。  
  
## <a name="installing-replication-by-using-setup"></a>セットアップ プログラムによるレプリケーションのインストール  
 **の新しいインスタンスをインストールするときにレプリケーションをインストールするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   レプリケーション管理オブジェクト (RMO) を含めてレプリケーション コンポーネントをインストールするには、インストール ウィザードの **[機能の選択]** ページで **[SQL Server レプリケーション]** を選択します。  
  
## <a name="installing-replication-from-the-command-prompt"></a>コマンド プロンプトによるレプリケーションのインストール  
 **の新しいインスタンスをインストールするときにレプリケーションをインストールするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   参照してください[コマンド プロンプトから SQL Server 2014 インストール](install-sql-server-from-the-command-prompt.md)します。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 をインストールします。](install-sql-server.md)   
 [コマンド プロンプトから SQL Server 2014 をインストールします。](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
