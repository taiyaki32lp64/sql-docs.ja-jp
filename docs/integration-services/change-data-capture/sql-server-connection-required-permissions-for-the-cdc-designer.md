---
title: CDC デザイナーで使用する SQL Server 接続に必要な権限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dee01068864d087548d0f6def2179787bf66fc55
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294554"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>CDC デザイナーで使用する SQL Server 接続に必要な権限

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC デザイナー コンソールのタスクを実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続情報が必要です。 このトピックでは、 **との接続を設定するために** [SQL Server への接続] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ダイアログ ボックスで指定できる情報について説明します。  
  
 **‭[SQL Server への接続]** ダイアログ ボックスは必要なときに開きます。たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報がない場合や、情報は存在しても接続に必要な権限がない場合などです。  
  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続が必要となる各種のタスクと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン/ユーザーに必要な権限について説明します。  
  
|タスク|最低限の権限|  
|----------|-------------------------|  
|関連する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用した CDC サービスおよびインスタンスの一覧表示|`db_datareader` ロール|  
|CDC インスタンスの開始/停止|`db_datareader` ロールと `db_datawriter` ロール|  
|CDC インスタンスの状態の表示|`db_owner` ロール|  
|新しい Oracle CDC インスタンス データベースの作成|`dbcreator` 固定サーバー ロール|  
|新しい Oracle CDC インスタンスの作成|`db_datareader` ロール<br /><br /> `db_owner` ロール|  
|配置スクリプトの取得|`db_datareader` ロールと `db_datawriter` ロール<br /><br /> `db_owner` ロール|  
|構成の変更およびキャプチャ インスタンスの追加/削除|`db_datareader` ロールと `db_datawriter` ロール<br /><br /> `db_owner` ロール|  
  
## <a name="see-also"></a>参照  
 [CDC デザイナー コンソールへのアクセス](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [インスタンスの作成のための SQL サーバー接続](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
