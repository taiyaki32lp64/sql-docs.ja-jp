---
title: CDC Service で使用する SQL Server 接続に必要な権限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9e968f9-180c-4fa0-a849-98f2b1942330
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e7528545f2b7cd50e4b612372dc35e65dcc2324a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298646"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-service"></a>CDC Service で使用する SQL Server 接続に必要な権限

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC Service 構成コンソールのタスクを実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続情報が必要です。 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]との接続を設定するために [SQL Server への接続] ダイアログ ボックスで指定できる情報について説明します。  
  
 ‭[SQL Server への接続] ダイアログ ボックスは必要なときに開きます。たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報がない場合や、情報は存在しても接続に必要な権限がない場合などです。  
  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続が必要となる各種のタスクと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン/ユーザーに必要な権限について説明します。  
  
|タスク|最低限の権限|  
|----------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを準備する。|`dbcreator` 固定サーバー ロール|  
|Oracle CDC サービスが使用する Oracle CDC Service-SQLServer ログインを作成する。|`public` 固定サーバー ロール|  
|MSXDBCDC に新しいサービスを登録するために使用する Oracle CDC Service ログインを作成する。|`db_datareader` ロールと `db_datawriter` ロール|  
|MSXDBCDC のサービスの登録を更新するために使用する Oracle CDC Service ログインを編集する。|`db_datareader` ロールと `db_datawriter` ロール|  
|MSXDBCDC のサービスの登録を更新するために使用する Oracle CDC Service ログインを削除する。|`db_datareader` ロールと `db_datawriter` ロール|  
  
## <a name="see-also"></a>参照  
 [SQL Server への接続](../../integration-services/change-data-capture/connection-to-sql-server.md)   
 [削除用の SQLServer への接続](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md)  
  
  
