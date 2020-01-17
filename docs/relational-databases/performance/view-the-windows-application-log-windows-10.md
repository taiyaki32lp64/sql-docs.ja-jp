---
title: Windows アプリケーション ログの表示 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2d6045c17028c16dfb2b90de15042dd18e3a91a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986618"
---
# <a name="view-the-windows-application-log-windows-10"></a>Windows アプリケーション ログの表示 (Windows 10)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Windows アプリケーション ログを使用するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が構成されている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各セッションで新しいイベントがそのログに書き込まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログとは異なり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを開始するたびに新しいアプリケーション ログが作成されることはありません。  
  
## <a name="view-the-windows-application-log"></a>Windows アプリケーション ログを表示する  
  
1. **[検索バー]** に「**イベント ビューアー**」と入力し、**イベント ビューアー** デスクトップ アプリを選択します。
  
2. **イベント ビューアー**で、 **[アプリケーションとサービス ログ]** を開きます。

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントは、 **[ソース]** 列に **MSSQLSERVER** (名前付きインスタンスの場合は **MSSQL$** _<instance_name>_ ) と表示されます。 また、SQL Server エージェントのイベントは SQLSERVERAGENT と表示されます ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのイベントは **SQLAgent$** \<*instance_name*> と表示されます)。 Microsoft Search サービスのイベントは " **Microsoft Search**" と表示されます。  
  
4. 別のコンピューターのログを表示するには、 **[イベント ビューアー (ローカル)]** を右クリックします。 **[別のコンピューターへ接続]** を選択し、フィールドに入力して **[コンピューターの選択]** ダイアログ ボックスの設定を完了します。  
  
5. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントのみを表示するには、必要に応じて **[表示]** メニューで **[フィルター]** を選択します。 **[イベント ソース]** 一覧で **[MSSQLSERVER]** を選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのイベントのみを表示するには、 **[イベント ソース]** ボックスの一覧で **[SQLSERVERAGENT]** を選択します。  
  
6. イベントについての詳細情報を表示するには、イベントをダブルクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server エラー ログの表示 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
