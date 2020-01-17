---
title: System.Data.dll の型およびメンバーが許可されていません |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4233bc1ddd98d6fe678d9d37f1acd7a4b66b687e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874364"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>System.Data.dll の許可されない型およびメンバー
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共通言語統合 (CLR) のプログラミングには、型またはメンバーを持つの使用が許可されない、`HostProtectionAttribute`を指定する、`System.Security.Permissions.HostProtectionResource`列挙の値を持つ`ExternalProcessMgmt`、 `ExternalThreading`、 `MayLeakOnAbort`、 `SecurityInfrastructure`、 `SelfAffectingProcessMgmnt`、`SelfAffectingThreading`、 **SharedState**、 `Synchronization`、または`UI`します。 次の表は、ホスト保護属性 (HPA) 値が許可されない System.Data.dll アセンブリのメンバーおよび型を示しています。  
  
> [!NOTE]  
>  この一覧は、サポートされているアセンブリから作成されたものです。 詳細については、次を参照してください。[サポートされている .NET Framework ライブラリ](../clr-integration/database-objects/supported-net-framework-libraries.md)します。  
  
|型またはメンバー|HPA 値|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState、Synchronization|  
|System.Xml.XmlDataDocument|Synchronization|  
  
## <a name="see-also"></a>参照  
 [ホスト保護属性と CLR 統合プログラミング](host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll の許可されない型およびメンバー](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Mscorlib.dll の許可されない型およびメンバー](disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.dll の許可されない型およびメンバー](disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll の許可されない型およびメンバー](disallowed-types-and-members-in-system-core-dll.md)  
  
  
