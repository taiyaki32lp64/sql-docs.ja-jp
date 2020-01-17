---
title: レポート サーバーのプロパティ ([サービス] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 2a2e1dbf-02b9-4893-aaf0-c0e4a2c9b4f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef0f55049e5ae9c96eed10fb1f39d7f3d95a19f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62506774"
---
# <a name="report-server-properties-service-tab"></a>[SQL Server Reporting Services のプロパティ] ダイアログ ボックス ([サービス] タブ)
  このサービスは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のレポート サーバー サービスです。 グレー表示になっているプロパティ値をこのアプリケーションで変更することはできません。  
  
## <a name="options"></a>および  
 **バイナリ パス**  
 このサービスが使用するプログラム ファイルの場所が表示されます。  
  
 **[エラー制御]**  
 1 は、"SERVICE_ERROR_NORMAL" を示します。 コンピューターの起動時にこのサービスが開始しなかった場合は、スタートアップ プログラムによってログにエラーが記録され、ポップアップ メッセージ ボックスが表示されますが、スタートアップ操作は継続します。 この値は変更できません。  
  
 **終了コード**  
 エラーが発生した場合は、エラー番号がこのボックスに表示されます。 その番号を手掛かりにして障害のトラブルシューティングを行ってください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報でその番号を検索することも、技術サポート スタッフにその番号を連絡することも可能です。  
  
 **Host Name**  
 フルテキスト検索を実行しているコンピューターまたはクラスターの名前が表示されます。  
  
 **名前**  
 サービスの表示名が表示されます。  
  
 **プロセス ID**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows プロセス ID が表示されます。  
  
 **[SQL サービスの種類]**  
 呼び出し側プロセスに提供されるサービスの種類です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、いくつかのサービスがインストールされます。  
  
 **開始モード**  
 このサービスを以下のいずれかのモードに設定します。  
  
-   手動：このサービスは、コンピューターの起動時に自動的に開始されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは他のツールを使用してこのサービスを開始する必要があります。  
  
-   自動：このサービスは、このコンピューターの起動時に起動しようとします。  
  
-   無効になっています。このサービスを開始できません。  
  
 **State**  
 このサービスが実行中か、停止しているか、無効になっているかが表示されます。  
  
## <a name="see-also"></a>参照  
 [[SQL Server のサービス]](../../../2014/tools/configuration-manager/sql-server-services.md)  
  
  
