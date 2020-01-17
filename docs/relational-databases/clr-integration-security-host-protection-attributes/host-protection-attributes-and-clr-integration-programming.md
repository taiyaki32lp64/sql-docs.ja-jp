---
title: 共通言語ランタイム (CLR) のホスト保護属性
description: 共通言語ランタイム (CLR) は、特定の属性を持つ .NET Framework の一部であるマネージアプリケーションプログラミングインターフェイス (Api) に注釈を付けるためのメカニズムを提供します。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
author: rothja
ms.author: jroth
ms.openlocfilehash: 733e4adc69570dd98e6e0ad5448820607ade6329
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258752"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>ホスト保護属性と CLR 統合プログラミング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  CLR (共通言語ランタイム) には、.NET Framework の一部であるマネージド API (アプリケーション プログラミング インターフェイス) に、特定の属性で注釈を付けるメカニズムが用意されています。このような属性は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降) など CLR のホストのための属性です。 このような HPA (ホスト保護属性) の例としては、次のものがあります。  
  
-   **Sharedstate**。共有状態を作成または管理する機能が API で公開されているかどうかを示します (静的クラスフィールドなど)。  
  
-   **同期**。これは、API がスレッド間で同期を実行する機能を公開するかどうかを示します。  
  
-   **Externalprocessmgmt**。 API がホストプロセスを制御する方法を公開するかどうかを示します。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、これらの属性が与えられると、CAS (コード アクセス セキュリティ) を使用して、ホストされた環境で許可されない HPA の一覧を指定します。 CA の要件は、 **SAFE**、 **EXTERNAL_ACCESS**、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **UNSAFE**の3つのアクセス許可セットのいずれかによって指定されます。 これら3つのセキュリティレベルのうちの1つは、アセンブリを**CREATE assembly**ステートメントを使用してサーバーに登録するときに指定します。 **SAFE**または**EXTERNAL_ACCESS**のアクセス許可セット内で実行されるコードで**は、特定**の型やメンバーが適用されないようにする必要があります。 詳細については、「[アセンブリの作成](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)」および「 [CLR 統合プログラミングモデルの制限](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)」を参照してください。  
  
 **Hostprotectionattribute**は、信頼性を向上させるためのセキュリティ権限ではありません。これは、ホストが許可しない可能性のある特定のコード構造 (型またはメソッド) を識別するためです。 **Hostprotectionattribute**を使用すると、ホストの安定性を保護するのに役立つプログラミングモデルが適用されます。  
  
## <a name="host-protection-attributes"></a>ホスト保護属性  
 HPA は、ホスト プログラミング モデルに適合しない型またはメンバーを識別して、次に示す信頼性に対する脅威を表します (リスクの低いものから順に並べています)。  
  
-   他の場合には特に害のない脅威  
  
-   サーバーで実行されるマネージ ユーザー コードの不安定化につながる脅威  
  
-   サーバー プロセス自体の不安定化につながる脅威  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Externalprocessmgmt**、 **externalスレッディング**、 **MayLeakOnAbort**、 **securityinfrastructure**、 **SelfAffectingProcessMgmnt**、 **SelfAffectingThreading**、 **sharedstate**、 **Synchronization**、または**UI**の値を持つ system.object を指定する**hostprotectionattribute**を持つ型またはメンバーを使用できないようにして**います。** これにより、状態の共有を可能にしたり、同期を実行するメンバーをアセンブリから呼び出すことができなくなります。さらに、終了時にリソース リークを発生させたり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスの整合性に影響を与える可能性があるメンバーの呼び出しも禁止されます。  
  
### <a name="disallowed-types-and-members"></a>許可されていない型とメンバー  
 次のトピックでは、 **Hostprotectionresource**値がで許可され[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ていない型とメンバーについて説明します。  
  
> [!NOTE]  
>  各トピックに含まれる一覧は、サポートされているアセンブリから作成されたものです。  詳細については、「[サポートされている .NET Framework ライブラリ](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Microsoft.VisualBasic.dll の許可されない型およびメンバー](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 HPA の値が許可されない Microsoft.VisualBasic.dll の型およびメンバーの一覧を示します。  
  
 [mscorlib.dll の許可されない型およびメンバー](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 HPA の値が許可されない mscorlib.dll の型およびメンバーの一覧を示します。  
  
 [System.dll の許可されない型およびメンバー](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 HPA の値が許可されない System.dll の型およびメンバーの一覧を示します。  
  
 [System.Data.dll の許可されない型およびメンバー](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 HPA の値が許可されない System.Data.dll の型およびメンバーの一覧を示します。  
  
 [System.Core.dll の許可されない型およびメンバー](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 HPA の値が許可されない System.Core.dll の型およびメンバーの一覧を示します。  
  
## <a name="see-also"></a>参照  
 [CLR 統合のコードアクセスセキュリティ](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 統合プログラミングモデルの制限事項](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [アセンブリの作成](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
