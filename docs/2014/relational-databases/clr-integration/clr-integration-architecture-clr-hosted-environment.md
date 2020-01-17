---
title: CLR ホスト環境 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- type-safe code [CLR integration]
- UNSAFE permission set
- run-time environments [CLR integration]
- common language runtime [SQL Server], about CLR integration
- application domains [CLR integration]
- host protection attributes [CLR integration]
- managed code [SQL Server], common language runtime
- permission sets [CLR integration]
- reliability [CLR integration]
- SAFE permission set
- code access security [CLR integration]
- EXTERNAL_ACCESS permission set
- verifying type safety
- scalability [CLR integration]
- hosted environments [CLR integration]
- HPAs [CLR integration]
ms.assetid: d280d359-08f0-47b5-a07e-67dd2a58ad73
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dbbc884a32f892830ec4b7b66e3a67c45fc37416
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922566"
---
# <a name="clr-hosted-environment"></a>CLR ホスト環境
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework CLR (共通言語ランタイム) は、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C++ など、多くの最新のプログラミング言語を実行する環境です。 CLR の特色には、ガベージ コレクションが行われるメモリ、プリエンプティブなスレッド処理、メタデータ サービス (型リフレクション)、コードの検証可能性、コード アクセス セキュリティなどがあります。 CLR では、クラスの検索と読み込み、メモリ内でのインスタンスのレイアウト、メソッド呼び出しの解決、ネイティブ コードの生成、セキュリティの設定、およびランタイム コンテキスト境界の設定にメタデータが使用されます。  
  
 CLR と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のランタイム環境では、メモリ、スレッド、および同期の処理方法が異なります。 このトピックでは、すべてのシステム リソースが統一的に管理されるように、これら 2 つのランタイムを統合する方法について説明します。 また、信頼性が高く、セキュリティで保護された実行環境をユーザー コードに提供するために、CLR CAS (コード アクセス セキュリティ) と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティを統合する方法についても説明します。  
  
## <a name="basic-concepts-of-clr-architecture"></a>CLR アーキテクチャの基本概念  
 .NET Framework では、プログラマは高級言語を使ってクラスを実装し、そのクラスの構造 (クラスのフィールドやプロパティなど) とメソッドを定義します。 このようなメソッドの一部は、静的関数にすることができます。 プログラムをコンパイルするとアセンブリと呼ばれるファイルが作成されます。このファイルには、MSIL ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] Intermediate Language) 形式のコンパイル済みコードと、依存アセンブリへのすべての参照を含むマニフェストが含まれます。  
  
> [!NOTE]  
>  アセンブリは CLR アーキテクチャの不可欠な要素です。 アセンブリは、.NET Framework のアプリケーション コードのパッケージ化、配置、およびバージョン管理の単位になります。 アセンブリを使用して、データベース内部にアプリケーション コードを配置し、完全なデータベース アプリケーションの管理、バックアップ、および復元を行うための統一された方法を提供できます。  
  
 アセンブリ マニフェストには、アセンブリに関するメタデータが含まれており、プログラムで定義されているすべての構造体、フィールド、プロパティ、クラス、継承関係、関数、およびメソッドの情報が記述されています。 マニフェストでは、アセンブリ ID の確立、アセンブリの実装を構成するファイルの指定、アセンブリを構成する型やリソースの指定、他のアセンブリに対するコンパイル時の依存関係の列挙、およびアセンブリを正しく実行するために必要な権限セットの指定を行います。 この情報を実行時に使用して、参照の解決、バージョン バインド ポリシーの設定、および読み込まれたアセンブリの整合性の検証が行われます。  
  
 .NET Framework では、アプリケーションがメタデータでキャプチャできる追加情報により、クラス、プロパティ、関数、およびメソッドに注釈を付けるためのカスタム属性がサポートされます。 すべての .NET Framework コンパイラでは、このような注釈を解釈せずに使用し、アセンブリ メタデータとして格納します。 このような注釈は、他のメタデータと同じ方法で調べることができます。  
  
 マネージド コードは、オペレーティング システムが直接実行するのではなく、CLR で MSIL として実行されます。 マネージド コード アプリケーションは、自動ガベージ コレクション、ランタイム型チェック、セキュリティ サポートなどの CLR サービスを使用します。 これらのサービスは、プラットフォームや言語に依存しない統一的な動作を、マネージド コード アプリケーションに提供するのに役立ちます。  
  
## <a name="design-goals-of-clr-integration"></a>CLR 統合の設計目標  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の CLR ホスト環境 (CLR 統合) 内でユーザー コードを実行するときは、次の設計目標が適用されます。  
  
###### <a name="reliability-safety"></a>信頼性 (安全性)  
 ユーザーからの応答を要求するメッセージ ボックスの表示やプロセスの終了など、データベース エンジン プロセスの整合性に影響を与える操作は、ユーザー コードから実行できないようにする必要があります。 ユーザー コードからデータベース エンジンのメモリ バッファーや内部データ構造体への上書きを許可しないでください。  
  
###### <a name="scalability"></a>スケーラビリティ  
 スケジュール設定とメモリ管理の内部モデルは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と CLR で異なります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、協調動作する非プリエンプティブなスレッド モデルがサポートされます。このモデルでは、定期的に、またはスレッドがロックや I/O を待機しているときに、スレッドの実行が自主的に明け渡されます。 CLR では、プリエンプティブなスレッド モデルがサポートされます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部で実行されているユーザー コードから、オペレーティング システムのスレッド プリミティブを直接呼び出すことができると、そのユーザー コードは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] タスク スケジューラに適切に統合されず、システムのスケーラビリティを低下させる可能性があります。 CLR では仮想メモリと物理メモリが区別されませんが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では物理メモリが直接管理され、構成可能な制限内で物理メモリを使用する必要があります。  
  
 このようにスレッド処理、スケジュール設定、およびメモリ管理のモデルが異なるため、数千の同時実行ユーザー セッションをサポートするまで規模が拡大された RDBMS (リレーショナル データベース管理システム) では統合が課題になります。 アーキテクチャでは、スレッド処理、メモリ、および同期プリミティブの API (アプリケーション プログラミング インターフェイス) を直接呼び出すユーザー コードによってシステムのスケーラビリティが損なわれないことを保証する必要があります。  
  
###### <a name="security"></a>セキュリティ  
 データベースで実行されるユーザー コードがテーブルや列などのデータベース オブジェクトにアクセスする際には、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の認証規則と承認規則に従う必要があります。 また、データベース管理者は、データベースで実行しているユーザー コードからファイルやネットワーク アクセスなどのオペレーティング システム リソースへのアクセスを制御できる必要があります。 (Transact-SQL などの非マネージド言語とは異なり) このようなリソースにアクセスする API が用意されているマネージド プログラミング言語ではこのことが重要になります。 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] プロセス外のコンピューター リソースにアクセスするユーザー コードには、システムによりセキュリティで保護された方法が提供される必要があります。 詳細については、「 [CLR 統合のセキュリティ](security/clr-integration-security.md)」を参照してください。  
  
###### <a name="performance"></a>パフォーマンス  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]で実行されるマネージド ユーザー コードと、サーバーの外部で実行されるマネージド ユーザー コードのコンピューター処理パフォーマンスは同程度になる必要があります。 マネージド ユーザー コードからのデータ アクセスは、ネイティブ [!INCLUDE[tsql](../../../includes/tsql-md.md)] ほど高速ではありません。 詳細については、次を参照してください。 [CLR 統合のパフォーマンス](clr-integration-architecture-performance.md)します。  
  
## <a name="clr-services"></a>CLR サービス  
 CLR により、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との CLR 統合のデザイン目標を達成するのに役立つ多数のサービスが提供されます。  
  
###### <a name="type-safety-verification"></a>型の安全性の確認  
 タイプ セーフなコードとは、メモリ構造にアクセスする際に適切に定義された方法のみを使用するコードのことです。 たとえば、有効なオブジェクト参照を例として考えると、タイプ セーフなコードでは、実際のフィールド メンバーに対応してメモリの固定オフセット位置にアクセスできます。 一方、オブジェクトに属するメモリの範囲の内外を問わず、任意のオフセット位置でメモリにアクセスするコードは、タイプ セーフではありません。 アセンブリを CLR に読み込むと、JIT (Just-In-Time) コンパイルを使用して MSIL にコンパイルされる前に、ランタイムによって、コードのタイプ セーフティを判断するためにそのコードを調べる検証フェーズが実行されます。 この検証に正常に合格するコードを、検証可能なタイプ セーフなコードと呼びます。  
  
###### <a name="application-domains"></a>アプリケーション ドメイン  
 CLR では、マネージド コード アセンブリを読み込み、実行できるホスト プロセス内の実行領域として、アプリケーション ドメインの概念がサポートされます。 アプリケーション ドメインの境界でアセンブリどうしが分離されます。 アセンブリは、静的変数やデータ メンバーの可視性、およびコードを動的に呼び出す機能に関して分離されます。 また、アプリケーション ドメインはコードのロードとアンロード用のメカニズムでもあります。 アプリケーション ドメインをアンロードしないと、コードをメモリからアンロードできません。 詳細については、次を参照してください。[アプリケーション ドメインと CLR 統合セキュリティ](../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)します。  
  
###### <a name="code-access-security-cas"></a>CAS (コード アクセス セキュリティ)  
 CLR セキュリティ システムには、マネージド コードに権限を割り当てて、そのコードで実行できる操作の種類を制御する方法が用意されています。 コード アクセス権限は、コード ID (アセンブリの署名やコードの作成元など) に基づいて割り当てられます。  
  
 CLR では、コンピューター管理者が設定できるコンピューター全体のポリシーが規定されます。 このポリシーでは、コンピューターで実行される任意のマネージド コードに許可される権限が定義されます。 さらに、マネージド コードに新たな制限を指定するために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] などのホストで使用できるホストレベルのセキュリティ ポリシーがあります。  
  
 .NET Framework のマネージド API により、コード アクセス権限で保護されているリソースでの操作が公開される場合、そのリソースへのアクセスが行われる前に、API がそのアクセス権限を要求することになります。 この要求により、CLR セキュリティ システムが呼び出し履歴内のすべての単位のコード (アセンブリ) を包括的にチェックします。 この処理は、リソースにアクセスする権限が呼び出しチェーン全体に許可されている場合にのみ行われます。  
  
 Reflection.Emit API を使用してマネージド コードを動的に生成する機能は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の CLR ホスト環境の内部ではサポートされないことに注意してください。 このようなコードには実行するための CAS 権限がないので、コードは実行時に失敗します。 詳細については、次を参照してください。 [CLR 統合のコード アクセス セキュリティ](security/clr-integration-code-access-security.md)します。  
  
###### <a name="host-protection-attributes-hpas"></a>HPA (ホスト保護属性)  
 CLR には、.NET Framework の一部であるマネージド API に、特定の属性で注釈を付けるメカニズムが用意されています。このような属性は CLR のホストにとって意味のある属性です。 次に、このような属性の例を示します。  
  
-   SharedState。共有状態 (静的なクラス フィールドなど) を作成または管理する機能が API で公開されるかどうかを示します。  
  
-   Synchronization。スレッド間で同期を実行する機能が API で公開されるかどうかを示します。  
  
-   ExternalProcessMgmt。ホスト プロセスを制御する方法が API で公開されるかどうかを示します。  
  
 これらの属性を例として考えると、ホストされている環境で禁止される必要がある SharedState 属性などの HPA の一覧をホストで指定できます。 この場合、CLR では禁止一覧の HPA で注釈が付けられている API がユーザー コードから呼び出されることを拒否します。 詳細については、次を参照してください。[ホスト保護属性と CLR 統合プログラミング](../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)します。  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>SQL Server と CLR の連携方法  
 ここでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と CLR のスレッド処理、スケジュール設定、同期、およびメモリ管理のモデルが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に統合されている様式について説明します。 特に、スケーラビリティ、信頼性、およびセキュリティの目標に照らし合わせて、この統合について解説します。 基本的には、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、CLR が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の内部でホストされているときに CLR のオペレーティング システムとして機能します。 CLR は、スレッド処理、スケジュール設定、同期、およびメモリ管理用に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって実装される低レベルのルーチンを呼び出します。 このようなルーチンは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エンジンの残りの部分で使用されるプリミティブと同じです。 このアプローチを使用すると、スケーラビリティ、信頼性、およびセキュリティに関するいくつかの利点が得られます。  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>スケーラビリティ:一般的なスレッド処理、スケジュール、および同期  
 CLR は、ユーザー コードを実行するため、および CLR 自体の内部で使用するために、スレッドを作成する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] API を呼び出します。 複数のスレッド間で同期するために、CLR は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 同期オブジェクトを呼び出します。 これにより、スレッドが同期オブジェクトを待機しているときに、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スケジューラは他のタスクのスケジュールを設定できます。 たとえば、CLR からガベージ コレクションが開始されると、CLR のすべてのスレッドがガベージ コレクションの終了を待機します。 CLR スレッドと CLR スレッドが待機している同期オブジェクトは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スケジューラに認識されるので、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、CLR に関連しない他のデータベース タスクを実行しているスレッドにスケジュールを設定できます。 また、これにより、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が CLR 同期オブジェクトによって取得されるロックに関連するデッドロックを検出し、デッドロックを除去する従来の技法を使用することもできます。  
  
 マネージド コードは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でプリエンプティブに実行されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スケジューラには、非常に長い間実行が明け渡されていないスレッドを検出して停止する機能が備わっています。 CLR スレッドを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スレッドにフックする機能は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スケジューラが CLR の "ランナウェイ" スレッドを識別し、それらのスレッドの優先度を管理できることを意味します。 このようなランナウェイ スレッドは中断され、キューに戻されます。 繰り返しランナウェイ スレッドとして識別されたスレッドは、実行中の他のワーカーを実行できるように、一定期間実行が許可されません。  
  
> [!NOTE]  
>  データにアクセスしたり、ガベージ コレクションを起動するのに十分なメモリを割り当てる実行時間の長いマネージド コードは、自動的に処理が明け渡されます。 データにアクセスしない、またはガベージ コレクションを起動するのに十分なマネージド メモリを割り当てない、実行時間の長いマネージド コードは、.NET Framework の System.Thread.Sleep() 関数を呼び出して、明示的に実行を明け渡す必要があります。  
  
###### <a name="scalability-common-memory-management"></a>スケーラビリティ:一般的なメモリ管理  
 CLR は、CLR のメモリの割り当ておよび割り当て解除を行うために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プリミティブを呼び出します。 CLR で使用されるメモリはシステムの総メモリ使用量の一部を占有するので、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はメモリの使用量を構成済みのメモリ制限内に抑えることができ、CLR と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が競い合ってメモリを確保することはありません。 また、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、システムのメモリが制約されているときに CLR からのメモリ要求を拒否し、他のタスクでメモリが必要なときにメモリ使用量を抑えるように CLR に要求することもできます。  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>信頼性:アプリケーション ドメインと回復不能な例外  
 .NET Framework API のマネージド コードで、メモリ不足やスタック オーバーフローなどの重大な例外が発生した場合、必ずそのようなエラーから回復し、API の実装に対して一貫性のある正しいセマンティクスを保証できるとは限りません。 これらの API により、このようなエラーへの応答でスレッドを中断する例外が発生します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でホストされているときは、CLR がスレッドの中断が発生したアプリケーション ドメインのすべての共有状態を検出することで、このようなスレッドの中断が処理されます。 CLR では、同期オブジェクトが存在するかどうかを確認することで、この処理を行います。 アプリケーション ドメインに共有状態が存在する場合は、アプリケーション ドメイン自体がアンロードされます。 アプリケーション ドメインをアンロードすると、そのアプリケーション ドメインで現在実行されているデータベース トランザクションが停止します。 共有状態が存在すると、例外が発生したユーザー セッション以外のユーザー セッションに、このような重大な例外の影響が拡大する可能性があるので、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と CLR では、共有状態が存在する可能性を減少させる手順が実行されます。 詳細については、.NET Framework のドキュメントを参照してください。  
  
###### <a name="security-permission-sets"></a>セキュリティ:アクセス許可セット  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、データベースに配置されるコードの信頼性とセキュリティに関する要件をユーザーが指定できます。 アセンブリがデータベースにアップロードされると、アセンブリの作成者を指定できます 3 つのアクセス許可セットのいずれかのアセンブリ。SAFE、EXTERNAL_ACCESS および UNSAFE です。  
  
|||||  
|-|-|-|-|  
|権限セット|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|コード アクセス セキュリティ|実行のみ|実行および外部リソースへのアクセス|[無制限]|  
|プログラミング モデルの制限事項|はい|はい|制限なし|  
|検証可能性の要件|はい|[はい]|いいえ|  
|ネイティブ コードを呼び出す機能|いいえ|いいえ|はい|  
  
 SAFE は、許可されているプログラミング モデルの中でも多くの制限事項が関連付けられており、最も信頼性が高く、セキュリティで保護されたモードです。 SAFE アセンブリには、実行、計算の実行、およびローカル データベースへのアクセスを行うには十分な権限が許可されます。 SAFE アセンブリは検証可能なタイプ セーフである必要があり、アンマネージ コードを呼び出すことはできません。  
  
 UNSAFE は、データベース管理者のみが作成できる信頼性の高いコードに指定します。 この信頼性の高いコードにはコード アクセス セキュリティに関する制限がなく、アンマネージ (ネイティブ) コードを呼び出すことができます。  
  
 EXTERNAL_ACCESS には、両者の中間に位置するセキュリティ オプションが提供されます。このオプションにより、SAFE の信頼性保証を備えたまま、コードからデータベース外部のリソースにアクセスできます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、ホストレベルの CAS ポリシー層を使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] カタログに格納されている権限セットに基づいて上記の 3 つの権限セットのうちのいずれかを許可するホスト ポリシーを構成します。 データベース内部で実行するマネージド コードには、これらのコード アクセス権限セットのうちのいずれかが必ず許可されます。  
  
### <a name="programming-model-restrictions"></a>プログラミング モデルの制限  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のマネージド コードのプログラミング モデルでは、通常、複数の呼び出し間で保持される状態の使用や複数のユーザー セッション間での状態の共有を必要としない関数、プロシージャ、および型の記述が必要になります。 さらに、既に説明したように、共有状態が存在すると、アプリケーションのスケーラビリティや信頼性に影響を与える重大な例外が発生する可能性があります。  
  
 このような考慮事項を考えると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で使用するクラスの静的変数や静的なデータ メンバーを使用することはお勧めしません。 SAFE アセンブリと EXTERNAL_ACCESS アセンブリの場合、CREATE ASSEMBLY を使用するときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でアセンブリのメタデータが調べられ、静的なデータ メンバーや変数の使用が検出された場合はこのようなアセンブリを作成できません。  
  
 また、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、`SharedState`、`Synchronization`、および `ExternalProcessMgmt` などのホスト保護属性で注釈が付けられている .NET Framework API の呼び出しが禁止されます。 これにより、SAFE アセンブリと EXTERNAL_ACCESS アセンブリで、状態の共有、同期の実行、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プロセスの整合性に影響を与える可能性のあるすべての API が呼び出されなくなります。 詳細については、次を参照してください。 [CLR 統合プログラミング モデルの制限事項](database-objects/clr-integration-programming-model-restrictions.md)します。  
  
## <a name="see-also"></a>参照  
 [CLR 統合のセキュリティ](security/clr-integration-security.md)   
 [CLR 統合のパフォーマンス](clr-integration-architecture-performance.md)  
  
  
