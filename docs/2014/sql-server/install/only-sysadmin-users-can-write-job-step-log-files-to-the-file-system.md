---
title: Sysadmin ユーザーがジョブ ステップ ログ ファイルをファイル システムに書き込むことができますのみ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84d04729e2f4c00c5d127a706727567c44855cd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093677"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>sysadmin ユーザーのみがジョブ ステップのログ ファイルをファイル システムに書き込むことができる
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、オプションで各ジョブ ステップのログが書き込まれます。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント  
  
## <a name="description"></a>説明  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントがのメンバーが所有するジョブのファイル システムにログを書き込むことができます、 **sysadmin**固定サーバー ロール。 ジョブの所有者のメンバーでない場合、 **sysadmin**ロールと、プロキシ アカウントが有効になっているかどうかは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントはプロキシ アカウントの資格情報を使用して、ファイル システムにログを記述することができます。  
  
 アップグレードした後、メンバーではないユーザーによって所有されているジョブの**sysadmin**固定サーバー ロールは、ファイル システムにログを書き込むことはできません。 これらのユーザーがテーブルにそのログを記述するオプションを選択する代わりに、 **msdb**データベース。 メンバー、 **sysadmin**ロール、ファイル システムにログ ファイルの書き込みもできます。  
  
## <a name="corrective-action"></a>修正措置  
 アップグレードした後、メンバーではないユーザーによって所有されているジョブの**sysadmin**ロールは引き続き実行するには、ログは作成されません。 テーブル以外のユーザーがメンバーへのジョブ ステップのログインの**sysadmin**ロールは、ジョブを手動で更新する必要があります。  
  
 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「ジョブの作成」、「ジョブ ステップの作成」、および「複数のジョブ ステップの処理」の各トピックを参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェントのアップグレードに関する問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
