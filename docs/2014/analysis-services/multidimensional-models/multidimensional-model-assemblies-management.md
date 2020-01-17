---
title: 多次元モデルのアセンブリの管理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], assemblies
- calling user-defined functions
- user impersonation [Analysis Services]
- impersonation [Analysis Services]
- Data Mining Extensions [Analysis Services], assemblies
- MDX [Analysis Services], assemblies
- user-defined functions [Analysis Services]
- Analysis Services objects, assemblies
- assemblies [Analysis Services]
- application domains [Analysis Services]
ms.assetid: b2645d10-6d17-444e-9289-f111ec48bbfb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c4f57e12754fc8e32fba8f483a2dfc360d7edc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073526"
---
# <a name="multidimensional-model-assemblies-management"></a>多次元モデルのアセンブリの管理
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、標準偏差計算から階層内でのメンバーのスキャンまで、あらゆる動作を実現するためにデザインされた、多次元式 (MDX) 言語およびデータ マイニング拡張機能 (DMX) 言語で使用するための多数の組み込み関数が提供されています。 ただし、他のすべての複雑で強力な製品がそうであるように、この製品も常に機能の拡張を求められています。  
  
 このため、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスまたはデータベースにアセンブリを追加するための機能が用意されています。 アセンブリを使用すると、Microsoft Visual Basic .NET や Microsoft Visual C# など、任意の共通言語ランタイム (CLR) 言語を使用する外部ユーザー定義関数を作成できます。 Microsoft Visual Basic や Microsoft Visual C++ など、コンポーネント オブジェクト モデル (COM) オートメーション言語を使用することもできます。  
  
> [!IMPORTANT]  
>  COM アセンブリにより、セキュリティ上のリスクが生じる可能性があります。 このリスクやその他の考慮事項により、[!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)] では、COM アセンブリが非推奨とされました。 COM アセンブリは、今後のリリースではサポートされない可能性があります。  
  
 アセンブリにより、MDX と DMX のビジネス機能が拡張されます。 必要な機能はダイナミック リンク ライブラリ (DLL) などのライブラリに作成し、このライブラリはアセンブリとして [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに追加します。 ライブラリ内のパブリック メソッドは、ユーザー定義関数として、MDX および DMX 式、プロシージャ、計算、動作、およびクライアント アプリケーションに公開されます。  
  
 新しいプロシージャや関数を使用したアセンブリをサーバーに追加できます。 アセンブリを使用して、サーバーによって提供されていない独自の機能を拡張または追加できます。 アセンブリを使用することにより、多次元式 (MDX)、データ マイニング拡張機能 (DMX)、またはストアド プロシージャに新しい関数を追加できます。 カスタム アプリケーションの実行場所からアセンブリが読み込まれ、アセンブリ バイナリ ファイルのコピーは、データベースのデータと共にサーバーに保存されます。 アセンブリを削除すると、そのアセンブリのコピーもサーバーから削除されます。  
  
 2 つのさまざまな種類のアセンブリができます。COM と CLR です。 CLR アセンブリとは、C#、Visual Basic .NET、マネージド C++ など、.NET Framework プログラミング言語で開発されたアセンブリです。 COM アセンブリとは、サーバーに登録する必要がある COM ライブラリです。  
  
 アセンブリは、 <xref:Microsoft.AnalysisServices.Server> オブジェクトまたは <xref:Microsoft.AnalysisServices.Database> オブジェクトに追加できます。 サーバー アセンブリは、サーバーまたはサーバー内の任意のオブジェクトに接続している任意のユーザーが呼び出すことができます。 データベース アセンブリは、 <xref:Microsoft.AnalysisServices.Database> オブジェクトまたはデータベースに接続しているユーザーのみが呼び出すことができます。  
  
 単純な <xref:Microsoft.AnalysisServices.Assembly> オブジェクトは、基本情報 (名前と ID)、ファイル コレクション、およびセキュリティの仕様で構成されます。  
  
 デバッグ ファイルがアセンブリ ファイルと共に読み込まれた場合、ファイル コレクションは、読み込まれたアセンブリ ファイルとそれらに対応するデバッグ (.pdb) ファイルを参照します。 アセンブリ ファイルは、アプリケーションがファイルを定義した場所から読み込まれ、コピーは、データと共にサーバーに保存されます。 アセンブリ ファイルのコピーは、サービスが開始されるたびにアセンブリを読み込むために使用されます。  
  
 セキュリティの仕様には、アセンブリを実行するために使用される権限セットと権限の借用が含まれます。  
  
## <a name="calling-user-defined-functions"></a>ユーザー定義関数の呼び出し  
 アセンブリでのユーザー定義関数の呼び出しは、完全修飾名を使用する必要があるという点を除いて、固有の関数の呼び出しと同じように行われます。 たとえば、次の例に示すように、MDX によって予期される型を返すユーザー定義関数は MDX クエリに含まれます。  
  
```  
Select MyAssembly.MyClass.MyStoredProcedure(a, b, c) on 0 from Sales  
```  
  
 ユーザー定義関数は、CALL キーワードを使用して呼び出すこともできます。 レコードセットまたは void 値を返すユーザー定義関数には CALL キーワードを使用する必要があります。また、ユーザー定義関数が、現在のキューブやデータ マイニング モデルなどの、MDX または DMX のステートメントやスクリプトのコンテキスト内のオブジェクトに依存する場合は、CALL キーワードは使用できません。 MDX または DMX クエリの外部で呼び出される関数の一般的な使用方法は、AMO オブジェクト モデルを使用して管理機能を実行することです。 たとえば、MDX ステートメントで `MyVoidProcedure(a, b, c)` 関数を使用する場合、次の構文を使用します。  
  
```  
Call MyAssembly.MyClass.MyVoidProcedure(a, b, c)  
```  
  
 アセンブリは、一度共通のコードを開発して単一の場所に格納することで、データベースの開発を簡略化します。 クライアント ソフトウェア開発者は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の関数ライブラリを作成して、アプリケーションと共に配布することができます。  
  
 アセンブリおよびユーザー定義関数は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 関数ライブラリまたは他のアセンブリの関数名と重複させることができます。 完全修飾名を使用してユーザー定義関数を呼び出す限り、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は正しいプロシージャを使用します。 セキュリティ目的と、異なるクラス ライブラリで重複する名前を呼び出す可能性を排除するため、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ではストアド プロシージャに対して完全修飾名のみを使用する必要があります。  
  
 特定の CLR アセンブリからユーザー定義関数を呼び出すには、次に示すように、ユーザー定義関数の前にアセンブリ名、完全なクラス名、プロシージャ名を付けます。  
  
 *AssemblyName*.*FullClassName*.*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の旧バージョンとの互換性のため、次の構文を使用することもできます。  
  
 *AssemblyName*!*FullClassName*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 COM ライブラリが複数のインターフェイスをサポートしている場合は、次に示すように、インターフェイス ID を使用してプロシージャ名を解決することもできます。  
  
 *AssemblyName*!*InterfaceID*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
## <a name="security"></a>セキュリティ  
 アセンブリのセキュリティは、コード アクセス セキュリティ モデルである、.NET Framework セキュリティ モデルに基づいています。 .NET Framework は、ランタイムが完全に信頼されるコードと部分的に信頼されるコードの両方をホストできると仮定する、コード アクセス セキュリティ メカニズムをサポートしています。 .NET Framework コード アクセス セキュリティによって保護されるリソースは、通常、リソースへのアクセスを許可する前に対応する権限を要求する、マネージド コードによってラップされます。 権限の要求は、(アセンブリ レベルで) 呼び出し履歴内のすべての呼び出し側が、対応するリソース権限を持つ場合にのみ満たされます。  
  
 アセンブリでは、実行権限は `PermissionSet` オブジェクトの `Assembly` プロパティを使用して渡されます。 マネージド コードが取得する権限は、有効なセキュリティ ポリシーによって決定されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以外によるホスト環境では、エンタープライズ、コンピューター、およびユーザーの 3 つの有効なポリシー レベルがあります。 コードが取得する権限の有効なリストは、これら 3 つのレベルによって取得される権限の共通部分によって決定されます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって、ホスト時の CLR にホスト レベルのセキュリティ ポリシー レベルが提供されます。このポリシーは、常に有効な 3 つのポリシー レベルよりも下位の、追加のポリシー レベルです。 このポリシーは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]によって作成されるアプリケーション ドメインごとに設定されます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ホスト レベル ポリシーは、システム アセンブリの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 固定ポリシーと、ユーザー アセンブリのユーザー指定ポリシーの組み合わせです。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ホスト ポリシーのユーザー指定部分は、各アセンブリの 3 つの権限バケットの 1 つを指定するアセンブリの所有者に基づいています。  
  
|設定する権限|説明|  
|------------------------|-----------------|  
|`Safe`|内部的な計算権限を提供します。 この権限バケットでは、.NET Framework 内の保護されたリソースにアクセスする権限は許可されません。 これは、`PermissionSet` プロパティで何も指定されていない場合に、アセンブリに既定の権限バケットです。|  
|`ExternalAccess`|外部システム リソースにアクセスする追加機能と共に、`Safe` 設定と同じアクセスを提供します。 この権限バケットはセキュリティの保証を提供するものではありませんが、信頼性の保証は提供されます (このシナリオを保証するのは可能です)。|  
|`Unsafe`|制限はありません。 この権限セットで実行されるマネージド コードに対する、セキュリティあるいは信頼性の保証はありません。 管理者によって指定されたカスタム権限であっても、すべての権限が、この信頼性のレベルで実行されるコードに与えられます。|  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]によって CLR がホストされるとき、スタックウォーク ベースの権限チェックはネイティブの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コードとの境界で停止されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] アセンブリ内のすべてのマネージド コードは常に、上記の 3 つの権限カテゴリのいずれかに分類されます。  
  
 COM (またはアンマネージ) アセンブリ ルーチンは、CLR セキュリティ モデルをサポートしません。  
  
### <a name="impersonation"></a>偽装  
 マネージド コードが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 外部のリソースにアクセスする場合、必ず適切な Windows セキュリティ コンテキスト内でアクセスが行われるようにするため、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はアセンブリの `ImpersonationMode` プロパティ設定に関連付けられているルールに従います。 `Safe` 権限設定を使用するアセンブリは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 外部のリソースにアクセスできないため、これらのルールは `ExternalAccess` 権限設定および `Unsafe` 権限設定を使用するアセンブリにのみ適用可能です。  
  
-   現在の実行コンテキストが Windows 認証ログインに対応しており、元の呼び出し側のコンテキストと同じ場合 (つまり、途中に EXECUTE AS が存在しない場合)、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は Windows 認証ログインの権限を借用してからリソースにアクセスします。  
  
-   元の呼び出し側のコンテキストを変更した中間の EXECUTE AS が存在する場合、外部リソースへのアクセスは失敗します。  
  
 `ImpersonationMode` プロパティは、`ImpersonateCurrentUser` または `ImpersonateAnonymous` に設定できます。 既定の設定、`ImpersonateCurrentUser` は、現在のユーザーのネットワーク ログイン アカウントでアセンブリを実行します。 場合、`ImpersonateAnonymous`設定を使用すると、実行コンテキストは、Windows ログインのユーザー アカウント iuser _ 対応*servername*サーバー。 これは、制限されたサーバー権限を持つ、インターネット ゲスト アカウントです。 このコンテキストで実行するアセンブリは、ローカル サーバーの制限されたリソースにのみアクセスできます。  
  
### <a name="application-domains"></a>アプリケーション ドメイン  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はアプリケーション ドメインを直接公開しません。 各アプリケーション ドメインは、同じアプリケーション ドメイン内で実行される一連のアセンブリにより、.NET Framework の `System.Reflection` 名前空間または他の方法を使用して実行時に互いを検出し、遅延バインドで互いの呼び出しを行うことができます。 このような呼び出しは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 認証ベース セキュリティによって使用される権限のチェック対象になります。  
  
 アプリケーション ドメインの境界と各ドメインで実行されるアセンブリは実装ごとに定義されるため、同じアプリケーション ドメインからアセンブリを検出できるとは限らないことに注意してください。  
  
## <a name="see-also"></a>参照  
 [ストアド プロシージャのセキュリティの設定](../multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)   
 [ストアド プロシージャの定義](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
