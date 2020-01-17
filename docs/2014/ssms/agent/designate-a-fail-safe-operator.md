---
title: 緊急時のオペレーターを指定する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54ec71df8efab1f60bfb7a5b9af448705e349d28
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211423"
---
# <a name="designate-a-fail-safe-operator"></a>Designate a Fail-Safe Operator
  緊急時のオペレーターとは、指定オペレーターが不在の場合に警告を受信するユーザーのことです。 このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告通知を受信する緊急時のオペレーターを設定する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **緊急時のオペレーターを指定する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   今後のバージョンの **では、** エージェントからポケットベル オプションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オプションが削除される予定です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  
  
-   SQL Server エージェントは、データベース メールを使用して、電子メールおよびポケットベルによる通知をオペレーターへ送信するように構成する必要があります。 詳細については、「 [オペレーターへの警告の割り当て](assign-alerts-to-an-operator.md)」を参照してください。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 緊急時のオペレーターを指定できるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-designate-a-fail-safe-operator"></a>緊急時のオペレーターを指定するには  
  
1.  **オブジェクト エクスプローラー** で、緊急時のオペレーターとして指定する SQL Server エージェント オペレーターを含むサーバーをプラス記号をクリックして展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** を選択します。  

3.  **SQL Server エージェントのプロパティ -** _server_name_ダイアログ ボックスで、**ページの選択**を選択します**警告システム**します。  
 
4.  **[緊急時のオペレーター]** の **[緊急時のオペレーターを有効にする]** チェック ボックスをオンにします。  
  
5.  **[オペレーター]** 一覧から、緊急時のオペレーターにするオペレーターを選択します。  
  
6.  次のチェック ボックスのいずれかまたはすべてを選択して、オペレーターへの通知方法を指定します。 **[電子メール]** 、 **[ポケットベル]** 、または **[Net Send]** 。  
  
7.  完了したら、 **[OK]** をクリックします。  
  
  
