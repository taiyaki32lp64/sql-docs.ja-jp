---
title: SMO 名前空間 |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], namespaces
- namespaces [SMO]
- SQL Server Management Objects, namespaces
ms.assetid: 7bfabe4d-9f4c-4bc9-b998-93bd2b50ee8a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5e606844d031bb4ab2c29d9dfd012c97601ca12f
ms.sourcegitcommit: b4962530f90234017073b3fdd2248936b2de4e69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71077541"
---
# <a name="smo-object-model-namespaces"></a>SMO オブジェクト モデル名前空間
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) にはさまざまな名前空間があります。 それぞれの名前空間は、SMO 内の機能の各領域を表しています。  
  
 で[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]は、SMO アセンブリは C:\Program are SQL Server\130\SDK\Assemblies フォルダーにあります。  
  
## <a name="namespaces"></a>名前空間  
 SMO 名前空間は次のとおりです。  
  
|クラス|関数|  
|-----------|--------------|  
|<xref:Microsoft.SqlServer.Management.Smo>|プログラムによって操作[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]するために使用されるインスタンスクラス、ユーティリティクラス、および列挙が含まれています。|  
|<xref:Microsoft.SqlServer.Management.Common>|接続クラスなど、レプリケーション管理オブジェクト (RMO) および SMO に共通のクラスが含まれています。|  
|<xref:Microsoft.SqlServer.Management.Smo.Agent>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを表すクラスが含まれています。|  
|<xref:Microsoft.SqlServer.Management.Smo.Wmi>|WMI プロバイダーを表すクラスが含まれています。|  
|<xref:Microsoft.SqlServer.Management.Smo.RegisteredServers>|登録済みサーバーを表すクラスが含まれています。|  
|<xref:Microsoft.SqlServer.Management.Smo.Mail>|データベース メールを表すクラスが含まれています。|  
|<xref:Microsoft.SqlServer.Management.Smo.Broker>|[!INCLUDE[ssSB](../../includes/sssb-md.md)] を表すクラスが含まれています。|  
  
  
