---
title: CLR 統合プログラミングモデルの制限 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
ms.openlocfilehash: c019b50f896109a699869d748d8eef20b57d6edb
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212371"
---
# <a name="clr-integration-programming-model-restrictions"></a>CLR 統合プログラミング モデルの制限事項
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  マネージストアドプロシージャまたはその他のマネージデータベースオブジェクトを構築する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって実行される特定のコードチェックについて考慮する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、マネージコードアセンブリがデータベースに最初に登録されたとき、 **CREATE assembly**ステートメントを使用して、実行時にもチェックを実行します。 マネージド コードが実行時にもチェックされるのは、実行時に決して到達しないコード パスがアセンブリに含まれる場合があるためです。  このチェックにより、サード パーティ アセンブリを柔軟に登録できます。特に、クライアント環境での実行を目的に作成され、ホストされた CLR では実行されない "安全でない" コードを含むアセンブリをブロックしないようにすることができるため、サード パーティ アセンブリに柔軟に対応できます。 マネージコードが満たす必要のある要件は、アセンブリが**安全**、 **EXTERNAL_ACCESS** **、または安全と**して登録されているかどうかによって異なります。**安全である**ことが保証され、以下に示します。  
  
 マネージド コード アセンブリには、制限事項に加えてコード セキュリティ権限も付与されます。 共通言語ランタイム (CLR) では、マネージド コードに対してコード アクセス セキュリティ (CAS) というセキュリティ モデルがサポートされます。 このモデルでは、コードの ID に基づいてアセンブリに権限が許可されます。 **セーフ**、 **EXTERNAL_ACCESS**、**安全でない**アセンブリには、異なる CAS アクセス許可があります。 詳細については、「 [CLR 統合コードアクセスセキュリティ](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)」を参照してください。  
  
## <a name="create-assembly-checks"></a>CREATE ASSEMBLY チェック  
 **CREATE ASSEMBLY**ステートメントを実行すると、各セキュリティレベルに対して次のチェックが実行されます。  いずれかのチェックが失敗した場合、 **CREATE ASSEMBLY**は失敗し、エラーメッセージが表示されます。  
  
### <a name="global-any-security-level"></a>グローバル (すべてのセキュリティ レベル)  
 参照されるすべてのアセンブリは、次の条件のうち 1 つ以上を満たす必要があります。  
  
-   既にデータベースに登録されていること。  
  
-   サポートされているアセンブリの 1 つであること。 詳細については、「[サポートされている .NET Framework ライブラリ](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)」を参照してください。  
  
-   _>\<の場所_**から CREATE ASSEMBLY**を使用しており、参照されているすべてのアセンブリとその依存関係は *\<の場所 >* で使用できます。  
  
-   \<バイト**から CREATE ASSEMBLY**を使用してい_ます...>、_ すべての参照は空白で区切られたバイトを使用して指定されます。  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 すべての**EXTERNAL_ACCESS**アセンブリは、次の条件を満たしている必要があります。  
  
-   静的フィールドが情報の格納に使用されていないこと。 読み取り専用の静的フィールドは許可されます。  
  
-   PEVerify テストにパスしていること。 .NET Framework SDK には、MSIL コードと関連メタデータがタイプ セーフの要件を満たしていることをチェックするための PEVerify ツール (peverify.exe) が付属しています。  
  
-   同期**属性**クラスなどの同期は使用されません。  
  
-   ファイナライザー メソッドが使用されていないこと。  
  
 **EXTERNAL_ACCESS**アセンブリでは、次のカスタム属性は許可されません。  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   すべての**EXTERNAL_ACCESS**アセンブリ条件がチェックされます。  
  
## <a name="runtime-checks"></a>ランタイムチェック  
 コード アセンブリは、実行時に次の条件をチェックされます。 これらの条件のいずれかが見つからなかった場合、マネージド コードの実行が失敗し、例外がスローされます。  
  
### <a name="unsafe"></a>UNSAFE  
 バイト配列からの **()** メソッドの呼び出しによって明示的に、またはリフレクションを使用して暗黙的にアセンブリを読み込み**ます。** 名前空間を生成することはできません。  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 すべての**安全でない**条件がチェックされます。  
  
 サポートされているアセンブリの一覧の中で、次のホスト保護属性 (HPA) 値で注釈を付けられている型およびメンバーはすべて許可されません。  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 HPAs と、サポートされているアセンブリの許可されていない型およびメンバーの一覧については、「[ホスト保護属性と CLR 統合プログラミング](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)」を参照してください。  
  
### <a name="safe"></a>SAFE  
 すべての**EXTERNAL_ACCESS**条件がチェックされます。  
  
## <a name="see-also"></a>参照  
 [サポートされている .NET Framework ライブラリ](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [CLR 統合のコードアクセスセキュリティ](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [ホスト保護属性と CLR 統合プログラミング](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [アセンブリの作成](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
