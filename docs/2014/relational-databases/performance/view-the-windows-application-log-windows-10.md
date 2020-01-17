---
title: Windows アプリケーション ログの表示 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b18643f97a328dfee94bc5bfe125d6eddeae4efe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150436"
---
# <a name="view-the-windows-application-log-windows"></a>Windows アプリケーション ログの表示 (Windows)
  Windows アプリケーション ログを使用するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が構成されている場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各セッションで新しいイベントがそのログに書き込まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログとは異なり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを開始するたびに新しいアプリケーション ログが作成されることはありません。  
  
### <a name="to-view-the-windows-application-log"></a>Windows アプリケーション ログを表示するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[管理ツール]** の順にポイントして、 **[イベント ビューアー]** をクリックします。  
  
2.  イベント ビューアーで **[アプリケーション]** をクリックします。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントは、 **[ソース]** 列に **MSSQLSERVER** (名前付きインスタンスの場合は **MSSQL$** _<instance_name>_ ) と表示されます。 また、SQL Server エージェントのイベントは SQLSERVERAGENT と表示されます ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのイベントは **SQLAgent$** \<*instance_name*> と表示されます)。 Microsoft Search サービスのイベントは "**Microsoft Search**" と表示されます。  
  
4.  別のコンピューターのログを表示するには、 **[イベント ビューアー]** を右クリックし、 **[別のコンピューターへ接続]** をクリックします。次に、 **[コンピューターの選択]** ダイアログ ボックスで必要な項目を設定します。  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベントのみを表示する場合は、 **[表示]** メニューの **[フィルター]** をクリックし、 **[イベント ソース]** ボックスの一覧で **[MSSQLSERVER]** を選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのイベントのみを表示するには、 **[イベント ソース]** ボックスの一覧で **[SQLSERVERAGENT]** を選択します。  
  
6.  イベントについての詳細情報を表示するには、イベントをダブルクリックします。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エラー ログの表示 &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
  
