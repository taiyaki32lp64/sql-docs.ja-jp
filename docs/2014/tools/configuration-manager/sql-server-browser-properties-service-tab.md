---
title: SQL Server Browser のプロパティ ([サービス] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 98ace9b0-72d5-4b72-9b7b-11fbc490981a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6421b0a7d6703e2a5d126aa83b227166492558a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211158"
---
# <a name="sql-server-browser-properties-service-tab"></a>[SQL Server Browser のプロパティ] ダイアログ ボックス ([サービス] タブ)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser プログラムはサーバー上のサービスとして実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種リソースに関する着信要求を受信し、このコンピューター上にインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに関する情報を提供します。  
  
 **[SQL Server Browser のプロパティ]** ダイアログ ボックスの **[サービス]** タブでは、以下のオプションを表示できます。 **[開始モード]** 以外のプロパティはすべて読み取り専用です。  
  
## <a name="options"></a>および  
 **バイナリ パス**  
 このサービスが使用するプログラム ファイルの場所が表示されます。  
  
 **エラー制御**  
 1 は `SERVICE_ERROR_NORMAL`を示します。 コンピューターの起動時にこのサービスが開始しなかった場合は、スタートアップ プログラムによってログにエラーが記録され、ポップアップ メッセージ ボックスが表示されますが、スタートアップ操作は継続します。 この値は変更できません。  
  
 **終了コード**  
 エラーが発生した場合は、エラー番号がこのボックスに表示されます。 その番号を手掛かりにして障害のトラブルシューティングを行ってください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報でその番号を検索することも、技術サポート スタッフにその番号を連絡することも可能です。  
  
 **Host Name**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを実行しているコンピューターまたはクラスターの名前が表示されます。  
  
 **名前**  
 サービスの表示名が表示されます。  
  
 **プロセス ID**  
 Windows プロセス ID が表示されます。  
  
 **[サービスの種類]**  
 呼び出し側プロセスに提供されるサービスの種類が表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、いくつかのサービスがインストールされます。  
  
 **開始モード**  
 このサービスを以下のいずれかのモードに設定します。  
  
-   手動：このサービスは、コンピューターの起動時に自動的に開始されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは他のツールを使用してこのサービスを開始する必要があります。  
  
-   自動：このサービスは、このコンピューターの起動時に起動しようとします。  
  
-   無効になっています。このサービスを開始できません。  
  
 **State**  
 このサービスが実行中か、停止しているか、無効になっているかが表示されます。 " **...** " の場合は、状態の変更が保留になっています。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Browser サービス](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
