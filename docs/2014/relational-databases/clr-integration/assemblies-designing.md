---
title: アセンブリのデザイン |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ad5135eb8141cc84bc6e5bddc8bd8477f4699b9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874927"
---
# <a name="designing-assemblies"></a>アセンブリのデザイン
  このトピックでは、アセンブリをデザインするときに考慮する必要がある次の項目について説明します。  
  
-   アセンブリのパッケージ化  
  
-   アセンブリのセキュリティを管理します。  
  
-   アセンブリに関する制限事項  
  
## <a name="packaging-assemblies"></a>アセンブリのパッケージ化  
 アセンブリのクラスやメソッドには、複数の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ルーチンまたは型の機能を含めることができます。 ほとんどの場合、関連する機能を実行するルーチンの機能を 1 つのアセンブリ内にパッケージ化することが適切です。これは特に、このようなルーチンで、メソッドが相互に呼び出しを行うクラスが共有される場合に当てはまります。 たとえば、CLR (共通言語ランタイム) トリガーと CLR ストアド プロシージャのデータ エントリ管理タスクを実行するクラスを 1 つのアセンブリにパッケージ化することがあります。 これは、これらのクラスのメソッドは、関連性の低いタスクを実行するクラスのメソッドよりも相互に呼び出しを行う可能性が高いためです。  
  
 コードをアセンブリにパッケージ化しているときは、次のことを考慮する必要があります。  
  
-   CLR ユーザー定義関数に依存する CLR ユーザー定義型とインデックスにより、アセンブリに依存する持続データがデータベースに格納される可能性があります。 多くの場合、アセンブリに依存する持続データがデータベースに存在すると、アセンブリのコードを変更することが複雑になることがあります。 そのため、一般に、持続データの依存関係があるコード (ユーザー定義関数を使用するユーザー定義型やインデックスなど) とそのような持続データの依存関係がないコードは切り離した方が適切です。 詳細については、次を参照してください。[を実装するアセンブリ](assemblies-implementing.md)と[ALTER ASSEMBLY &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)します。  
  
-   マネージド コードの一部分で上位の権限が必要な場合、そのコードは、上位の権限を必要としないコードとは別のアセンブリにパッケージ化することをお勧めします。  
  
## <a name="managing-assembly-security"></a>アセンブリのセキュリティ管理  
 アセンブリでマネージド コードが実行されるときに、.NET コード アクセス セキュリティによって保護されているリソースにアセンブリがアクセスできる程度を制御できます。 作成またはアセンブリを変更するときに、次の 3 つのアクセス許可セットのいずれかのファイルを指定することによって行います。SAFE、EXTERNAL_ACCESS、または UNSAFE です。  
  
### <a name="safe"></a>SAFE  
 SAFE は既定の権限セットであり、最も強い制限です。 SAFE 権限を指定したアセンブリによって実行されるコードでは、ファイル、ネットワーク、環境変数、またはレジストリなどの外部システム リソースにアクセスできません。 SAFE コードでは、ローカルの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースのデータにアクセスしたり、ローカル データベースの外部にあるリソースへのアクセスを必要としない計算やビジネス ロジックを実行したりすることができます。  
  
 ほとんどのアセンブリでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の外部にあるリソースにアクセスしなくても計算やデータ管理タスクを実行できます。 そのため、アセンブリの権限セットとして SAFE を使用することをお勧めします。  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS を使用すると、アセンブリでファイル、ネットワーク、Web サービス、環境変数、およびレジストリなどの特定の外部システム リソースにアクセスできます。 EXTERNAL ACCESS 権限を持つ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインだけが EXTERNAL_ACCESS アセンブリを作成できます。  
  
 SAFE アセンブリおよび EXTERNAL_ACCESS アセンブリには検証可能なタイプ セーフのコードしか格納できません。 つまり、これらのアセンブリでクラスにアクセスするには、型定義で有効な整形式のエントリ ポイントを使用する必要があります。 そのため、これらのアセンブリでは、コードによって所有されていないメモリ バッファーに自由にアクセスすることはできません。 また、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プロセスの堅牢性に悪影響を与える可能性がある操作を実行することもできません。  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE を使用すると、アセンブリでは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の内外を問わずどちらのリソースにも無制限にアクセスできます。 UNSAFE アセンブリの内部で実行されているコードで、アンマネージ コードを呼び出すことができます。  
  
 また、UNSAFE を指定すると、CLR 検証機能によってタイプ セーフではないと見なされる操作をアセンブリのコードで実行できます。 これらの操作により、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プロセス空間のメモリ バッファーに制御なしにアクセスされる可能性があります。 UNSAFE アセンブリでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] または共通言語ランタイムのいずれかのセキュリティ システムが妨害されるおそれもあります。 UNSAFE 権限は、経験豊かな開発者や管理者によって信頼性の高いアセンブリにのみ与えるようにする必要があります。 メンバーのみ、 **sysadmin**固定サーバー ロールは、UNSAFE アセンブリを作成できます。  
  
## <a name="restrictions-on-assemblies"></a>アセンブリに関する制限事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、アセンブリのマネージド コードに特定の制限を設けて、これらのコードを信頼性および拡張性の高い方法で実行できるようにしています。 つまり、SAFE アセンブリと EXTERNAL_ACCESS アセンブリでは、サーバーの堅牢性を侵害する可能性のある操作を実行できません。  
  
### <a name="disallowed-custom-attributes"></a>禁止されているカスタム属性  
 アセンブリには次のカスタム属性で注釈を付けることができません。  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 また、SAFE アセンブリと EXTERNAL_ACCESS アセンブリには、次のカスタム属性で注釈を付けることができません。  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>禁止されている .NET Framework API  
 すべて[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]注釈が付けられた、許可されていないのいずれかの API **HostProtectionAttributes** SAFE と EXTERNAL_ACCESS アセンブリから呼び出すことはできません。  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>サポートされている .NET Framework アセンブリ  
 カスタム アセンブリで参照されているアセンブリは、CREATE ASSEMBLY を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に読み込む必要があります。 次の [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] アセンブリは既に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に読み込まれているため、CREATE ASSEMBLY を使用しなくてもカスタム アセンブリで参照できます。  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>参照  
 [アセンブリ&#40;データベース エンジン&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [CLR 統合のセキュリティ](security/clr-integration-security.md)  
  
  
