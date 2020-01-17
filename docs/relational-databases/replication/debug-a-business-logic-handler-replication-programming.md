---
title: ビジネス ロジック ハンドラーのデバッグ (レプリケーション プログラミング)
description: ビジネス ロジック ハンドラーを使用して、マージ サブスクリプションの同期時にカスタム ビジネス ロジックを呼び出す方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- merge replication business logic handlers [SQL Server replication]
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b001e9e53c30ba57b2a56b0bd57571668ae2770c
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321779"
---
# <a name="debug-a-business-logic-handler-replication-programming"></a>ビジネス ロジック ハンドラーのデバッグ (レプリケーション プログラミング)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  マージ サブスクリプションの同期時にカスタム ビジネス ロジックを呼び出すには、ビジネス ロジック ハンドラーを使用します。 詳細については、「[Execute Business Logic During Merge Synchronization](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)」(マージ同期中のビジネス ロジックの実行) をご覧ください。  
  
 マージ レプリケーション競合回避モジュール (replrec.dll) は、ビジネス ロジックを含むマネージド コード アセンブリを呼び出します。 ほとんどの場合、replrec.dll とカスタム ビジネス ロジックは、マージ エージェントが実行されるコンピューター (プル サブスクリプションの場合はサブスクライバー、プッシュ サブスクリプションの場合はディストリビューター) で実行されます。 Web 同期の場合、または [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーの場合、競合回避モジュールとカスタム ビジネス ロジックは Web サーバーで実行されます。  
  
### <a name="to-debug-a-business-logic-handler-on-a-local-computer"></a>ローカル コンピューターでビジネス ロジック ハンドラーをデバッグするには  
  
1.  パブリッシングとディストリビューションを構成し、パブリケーションを作成し、パブリケーションへのサブスクリプションを作成します。 詳細については、「[パブリッシングおよびディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)」と「[パブリケーションの作成](../../relational-databases/replication/publish/create-a-publication.md)」をご参照ください。  
  
2.  ビジネス ロジック ハンドラーを作成して登録します。 詳細については、「 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)」を参照してください。  
  
3.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio で、マージ エージェントをプログラムで同期的に起動するレプリケーション管理オブジェクト (RMO) プロジェクトを作成します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
4.  ビジネス ロジック ハンドラー コードのデバッグ対象のメソッドまたはクラス コンストラクター内にブレークポイントを設定します。 ビジネス ロジック ハンドラーで実装可能なメソッドに詳細については、 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> メソッドのトピックを参照してください。  
  
5.  ビジネス ロジック ハンドラーをデバッグ モードでビルドし、手順 1. で登録した場所にアセンブリとデバッグ シンボル ファイル (.pdb) を配置します。  
  
    > [!NOTE]  
    >  デバッグを簡素化するには、ビジネス ロジック ハンドラー プロジェクトとサブスクリプションを同期するプロジェクトの両方を含む単一の Visual Studio .NET ソリューションを作成します。 その場合は、同期プロジェクトをスタートアップ プロジェクトとして設定し、デバッグ時に手順 1. で登録した場所にビジネス ロジック アセンブリを配置するようにビルド環境を構成します。  
  
6.  サブスクリプションまたはパブリケーション データベースに対して、挿入、更新、削除のいずれかのコマンドを実行します。 コマンドと実行場所は、デバッグ対象のメソッドによって異なります。  
  
7.  手順 3. のプロジェクトをデバッグ モードで起動し、サブスクリプションを同期します。  
  
8.  他のブレークポイントを設定しておらず、適切なコマンドがレプリケートされたと仮定すると、ビジネス ロジック ハンドラー内のブレークポイントに達したときに実行が停止します。  
  
### <a name="to-debug-a-business-logic-handler-on-a-web-server-using-web-synchronization-or-for-a-sql-server-compact-subscriber"></a>Web 同期を使用する Web サーバーまたは SQL Server Compact サブスクライバーに対してビジネス ロジック ハンドラーをデバッグするには  
  
1.  パブリッシングとディストリビューションを構成し、パブリケーションを作成し、パブリケーションへのプル サブスクリプションを作成します。 パブリケーションでは、Web 同期または [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーをサポートする必要があります。  
  
2.  ビジネス ロジック ハンドラーを作成して登録します。 詳細については、「 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)」を参照してください。  
  
3.  ビジネス ロジック ハンドラー コードのデバッグ対象のメソッドまたはクラス コンストラクター内にブレークポイントを設定します。 ビジネス ロジック ハンドラーで実装可能なメソッドに詳細については、 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> メソッドのトピックを参照してください。  
  
4.  ビジネス ロジック ハンドラーをデバッグ モードでビルドし、手順 1. で登録した場所にある Web サーバーにアセンブリとデバッグ シンボル ファイル (.pdb) を配置します。  
  
    > [!NOTE]  
    >  アセンブリが使用中であるためにビジネス ロジック ハンドラーのビルドに失敗した場合は、Web サーバーでコマンド プロンプトからコマンド `iisreset` を入力し、Web サーバーをリセットします。  
  
5.  Web 同期を有効にしてサブスクリプションを同期します。 同期中に、Web サーバーは登録されたアセンブリを読み込みます。  
  
6.  Visual Studio .NET デバッガーを使用し、Web サーバー上の以下のプロセスのいずれかにアタッチします。  
  
    -   w3wp.exe - Windows Server 2003。  
  
    -   inetinfo.exe - Windows 2000 および Windows XP。  
  
7.  **[出力]** ウィンドウで、デバッグ出力を確認し、登録されたアセンブリのシンボルが正しく読み込まれたことを確認します。 シンボルが読み込まれていない場合は、適切な .pdb ファイルが手順 4. でコピーされたことを確認し、手順 5. を繰り返します。  
  
8.  サブスクリプションまたはパブリケーション データベースに対して、挿入、更新、削除のいずれかのコマンドを実行します。 コマンドと実行場所は、デバッグ対象のメソッドによって異なります。  
  
9. Visual Studio デバッガーを使用し、w3wp.exe プロセスにアタッチします。  
  
10. Web 同期を使用して、サブスクリプションを再び同期します。  
  
11. 他のブレークポイントを設定しておらず、適切なコマンドがレプリケートされたと仮定すると、ビジネス ロジック ハンドラー内のブレークポイントに達したときに実行が停止します。  
  
## <a name="see-also"></a>参照  
 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
