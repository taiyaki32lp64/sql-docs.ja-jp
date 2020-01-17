---
title: ジョブ応答の指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9fa238a639321e9464ca3de2cc074b516f7df1e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245994"
---
# <a name="specify-job-responses"></a>ジョブ応答の指定
  ジョブ応答では、ジョブの完了後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスで実行するアクションを指定します。 ジョブ応答により、データベース管理者はジョブの完了日時や実行頻度を確認できます。 以下に、一般的なジョブ応答を示します。  
  
-   電子メール、ポケットベル、または **net send** メッセージによってオペレーターに通知します。  
  
     オペレーターが事後の作業を実行する必要がある場合に、これらのジョブ応答のいずれかを使用します。 たとえば、バックアップ ジョブが正常に終了した場合、オペレーターは、バックアップ テープを取り出して、安全な場所に保管するように通知を受ける必要があります。  
  
-   Windows アプリケーション ログにイベント メッセージを書き込みます。  
  
     この応答は、失敗したジョブに対してのみ使用できます。  
  
-   ジョブを自動的に削除します。  
  
     このジョブを再実行する必要がないことが明らかな場合に、このジョブ応答を使用します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**[説明]**|**トピック**|  
|オペレーターにジョブの状態を通知する方法について説明します。|[Notify an Operator of Job Status](notify-an-operator-of-job-status.md)|  
|ジョブの状態を Windows アプリケーション ログに書き込む方法について説明します。|[Windows アプリケーション ログへのジョブ状態の書き込み](../../reporting-services/report-server/windows-application-log.md)|  
  
## <a name="see-also"></a>参照  
 [イベントの監視と応答](monitor-and-respond-to-events.md)  
  
  
