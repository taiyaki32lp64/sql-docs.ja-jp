---
title: SQL Server のプロパティ ([サービス] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e4ae0c6b-6fd8-4325-b54e-1758fc659958
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 6b26b262e6451c909175e8cb4bac5f33dbe49164
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023949"
---
# <a name="sql-server-properties-service-tab"></a>[SQL Server のプロパティ] ダイアログ ボックス ([サービス] タブ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  **[MSSQLSERVER のプロパティ]** ダイアログ ボックスの **[サービス]** タブでは、以下のオプションの表示や指定を行います。  
  
## <a name="options"></a>オプション  
 **[バイナリ パス]**  
 このサービスで使用するプログラム ファイルの場所を一覧表示します。  
  
 **[エラー制御]**  
 1 は `SERVICE_ERROR_NORMAL`を示します。 コンピューターの起動時にこのサービスが開始しなかった場合は、スタートアップ プログラムによってログにエラーが記録され、ポップアップ メッセージ ボックスが表示されますが、スタートアップ操作は継続します。 この値は変更できません。  
  
 **終了コード**  
 エラーが発生した場合は、エラー番号がこのボックスに表示されます。 その番号を手掛かりにして障害のトラブルシューティングを行ってください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報でその番号を検索することも、技術サポート スタッフにその番号を連絡することも可能です。  
  
 **Host Name**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行しているコンピューターまたはクラスターの名前が表示されます。  
  
 **[名前]**  
 サービスの表示名が表示されます。  
  
 **プロセス ID**  
 Windows プロセス ID が表示されます。  
  
 **[サービスの種類]**  
 呼び出し側プロセスに提供されるサービスの種類が表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、いくつかのサービスがインストールされます。  
  
 **開始モード**  
 このサービスを以下のいずれかのモードに設定します。  
  
-   手動: このサービスは、コンピューターの起動時に自動的に開始しません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは他のツールを使用してこのサービスを開始する必要があります。  
  
-   \[自動]: このサービスは、コンピューターの起動時に開始を試みます。  
  
-   \[無効]: このサービスは開始できません。  
  
 **状態**  
 このサービスが実行中か、停止しているか、無効になっているかが表示されます。 " **...** " の場合は、状態の変更が保留になっています。  
  
  
