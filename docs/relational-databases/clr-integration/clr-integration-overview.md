---
title: CLR 統合の概要 |Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], about CLR integration
- extended stored procedures [SQL Server], vs. managed code
- objects [CLR integration]
- Transact-SQL vs. managed code
- managed code [SQL Server], vs. Transact-SQL
- managed code [SQL Server], vs. extended stored procedures
- execution at client vs. execution at server [CLR integration]
ms.assetid: 5aa176da-3652-4afa-a742-4c40c77ce5c3
author: rothja
ms.author: jroth
ms.openlocfilehash: d87768886150b06b23c6ff5053e4f0f524828904
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212398"
---
# <a name="clr-integration---overview"></a>CLR 統合 - 概要
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  CLR (共通言語ランタイム) は Microsoft .NET Framework の中核部分であり、あらゆる .NET Framework コードに対する実行環境を提供します。 CLR 内で実行されるコードを、マネージド コードと呼びます。 CLR では、JIT (Just-In-Time) コンパイル、メモリの割り当てと管理、タイプ セーフの確保、例外処理、スレッド管理、セキュリティなど、プログラムの実行に必要なさまざまな機能やサービスが提供されます。  詳細については、.NET Framework SDK を参照してください。  
  
 Microsoft SQL Server でホストされる CLR のことを CLR 統合と呼びます。この CLR 統合を使用すると、マネージド コードで、ストアド プロシージャ、トリガー、ユーザー定義関数、ユーザー定義型、ユーザー定義集計を作成できます。 マネージド コードは実行前にネイティブ コードにコンパイルされるので、シナリオによってはパフォーマンスの大幅な向上を図ることができます。  
  
 マネージド コードでは、アセンブリが特定の操作を実行できないように、CAS (コード アクセス セキュリティ) が使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、CAS を使用して、マネージド コードをセキュリティで保護し、オペレーティング システムやデータベース サーバーが危険にさらされる状況を回避しています。  
  
## <a name="advantages-of-clr-integration"></a>CLR 統合機能の利点  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] は、データに直接アクセスしたり、データベースを直接操作することを主眼に設計されています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] はデータへのアクセスやデータの管理に優れていますが、いわゆる本格的なプログラミング言語ではありません。 たとえば、[!INCLUDE[tsql](../../includes/tsql-md.md)] では、配列、コレクション、for-each ループ、ビット シフト、およびクラスはサポートされません。 このような構成要素の一部は [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して類似したものを作成することもできますが、マネージド コードにはこれらの構成要素に対するサポートが組み込まれています。 シナリオによっては、この特性が、特定のデータベースの機能をマネージド コードに実装するかどうかの決め手となることがあります。  
  
 Microsoft Visual Basic .NET および Microsoft Visual C# は、カプセル化、継承、多態性など、オブジェクト指向の機能を備えています。 関連のあるコードは、簡単にクラスや名前空間に編成することができます。 大量のサーバー コードを使用している場合も、この機能により、コードの編成と管理を簡略化できます。  
  
 計算や複雑な実行ロジックには、[!INCLUDE[tsql](../../includes/tsql-md.md)] よりもマネージド コードが適しています。また、マネージド コードでは、文字列処理や正規表現など、多数の複雑なタスクが幅広くサポートされています。 .NET Framework ライブラリの機能を使用すると、数千もの事前にビルドされたクラスやルーチンにアクセスすることができます。 このようなクラスやルーチンには、任意のストアド プロシージャ、トリガー、またはユーザー定義関数から簡単にアクセスできます。 BCL (基本クラス ライブラリ) には、文字列操作、高度な算術演算、ファイル アクセス、暗号化などの機能を提供するクラスがあります。  
  
> [!NOTE]  
>  これらのクラスの多くは、SQL Server の CLR コード内から使用できますが、サーバー側での使用が適していないクラス (ウィンドウ関連のクラスなど) にはアクセスできません。 詳細については、「[サポートされている .NET Framework ライブラリ](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)」を参照してください。  
  
 マネージド コードの利点の 1 つはタイプ セーフであることです。つまり、コードから各データ型へのアクセスは、正しく定義された許容される方法に限られます。 CLR は、マネージド コードが実行される前に、そのコードが安全であることを確認します。 たとえば、事前に書き込まれていないメモリからの読み取りが行われないように、コードがチェックされます。 また、CLR は、コードからアンマネージ メモリの操作が行われないようにする際にも役立ちます。  
  
 CLR 統合を使用すると、パフォーマンスが向上する可能性が高くなります。 詳細については、「 [CLR 統合のパフォーマンス](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)」を参照してください。  
 
> [!WARNING]
>  CLR では、セキュリティ境界としてサポートされなくなった、.NET Framework のコード アクセス セキュリティ (CAS) が使用されます。 `PERMISSION_SET = SAFE` で作成された CLR アセンブリが、外部のシステム リソースにアクセスし、非管理対象コードを呼び出し、sysadmin 特権を取得できる場合があります。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 以降、CLR アセンブリのセキュリティを強化するために `sp_configure` という `clr strict security` オプションが導入されました。 `clr strict security` は既定で有効になり、`SAFE` および `EXTERNAL_ACCESS` アセンブリを `UNSAFE` とマークされている場合と同様に扱います。 `clr strict security` オプションを旧バージョンとの互換性のために無効にすることはできますが、これは推奨されません。 Microsoft では、master データベースで `UNSAFE ASSEMBLY` アクセス許可が付与されている対応するログインを含む証明書または非対称キーで、すべてのアセンブリに署名することをお勧めします。 詳しくは、「[CLR の厳密なセキュリティ](../../database-engine/configure-windows/clr-strict-security.md)」をご覧ください。 
  
## <a name="choosing-between-transact-sql-and-managed-code"></a>Transact-SQL とマネージド コードの選択  
 ストアド プロシージャ、トリガー、およびユーザー定義関数を記述する際には、従来の [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用するか、Visual Basic .NET や Visual C# などの .NET Framework 言語を使用するかを判断する必要があります。 データ アクセスに使用する手続き型のロジックが、コード中にない場合や非常に少ない場合は、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用します。 複雑なロジックで CPU を集中的に使用する関数やプロシージャ、または .NET Framework の BCL を使用する場合は、マネージド コードを使用します。  
  
### <a name="choosing-between-execution-in-the-server-and-execution-in-the-client"></a>サーバー側での実行とクライアント側での実行の選択  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] とマネージド コードのどちらを使用するかを判断する際には、コードをサーバー コンピューターで実行するか、またはクライアント コンピューターで実行するかを判断する必要があります。 [!INCLUDE[tsql](../../includes/tsql-md.md)] とマネージド コードは、どちらもサーバー側で実行することができます。 サーバー側でコードを実行すると、コードとデータが近くにあるため、サーバーの処理能力を活用できます。 逆に、データベース サーバーでプロセッサを集中的に使用するタスクを実行することが好ましくない場合もあります。 現在、多くのクライアント コンピューターは高性能なので、できるだけ多くのコードをクライアント側で実行して、この処理能力を活用することもできます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] はクライアント側で実行することはできませんが、マネージド コードはクライアント側で実行することができます。  
  
## <a name="choosing-between-extended-stored-procedures-and-managed-code"></a>拡張ストアド プロシージャとマネージド コードの選択  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャでは実行不可能な機能を実行するために、拡張ストアド プロシージャを構築できます。 ただし、拡張ストアド プロシージャでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスの整合性を侵害する可能性があります。一方、マネージド コードは、タイプ セーフなので、SQL Server プロセスの整合性を侵害することはありません。 さらに、CLR のマネージド コードと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の間では、メモリ管理、スレッドやファイバーのスケジュール設定、同期サービスが、より密接に統合されます。 CLR 統合を使用すると、拡張ストアド プロシージャを使用するよりも安全に、[!INCLUDE[tsql](../../includes/tsql-md.md)] では記述できないタスクを実行するのに必要なストアド プロシージャを記述することができます。 CLR 統合と拡張ストアドプロシージャの詳細については、「 [Clr 統合のパフォーマンス](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [.NET Framework  のインストール](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)  
 [CLR 統合  のアーキテクチャ](https://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)  
 [CLR データベースオブジェクトからのデータアクセス](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CLR 統合の概要](../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
  
  
