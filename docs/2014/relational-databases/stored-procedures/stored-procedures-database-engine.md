---
title: ストアド プロシージャ (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- storing programs as stored procedures
- stored procedures [SQL Server], about stored procedures
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fdbca3ed012e082c899a5015faabc5c0019fcd75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68197110"
---
# <a name="stored-procedures-database-engine"></a>ストアド プロシージャ (データベース エンジン)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のストアド プロシージャは、1 つ以上の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、または [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイム (CLR) メソッドの参照のグループです。 プロシージャは、以下ができるために、他のプログラミング言語の構造に似ています。  
  
-   入力パラメーターを受け取り、呼び出し元のプログラムに出力パラメーターの形式で複数の値を返す。  
  
-   データベース内での操作を実行するプログラミング ステートメントを含む。 これには他のプロシージャの呼び出しも含まれます。  
  
-   呼び出し元のプログラムにステータス値を返し、成功、失敗、および失敗の原因を示す。  
  
## <a name="benefits-of-using-stored-procedures"></a>ストアド プロシージャを使用する利点  
 プロシージャを使用する利点の一部を次に示します。  
  
 サーバー/クライアント ネットワーク トラフィックの低減  
 プロシージャ内のコマンドは単一バッチのコードとして実行されます。 これにより、ネットワークではプロシージャを実行するための呼び出しのみが送信されるため、サーバーとクライアント間でのネットワーク トラフィックを大幅に低減できます。 プロシージャによって提供されるコードのカプセル化が存在しない場合は、ネットワークでコードの各行を送信する必要があります。  
  
 セキュリティの強化  
 ユーザーおよびクライアント プログラムが基になるデータベース オブジェクトに直接アクセスできる権限を持っていない場合でも、プロシージャにより複数のユーザーおよびクライアント プログラムが基になるデータベース オブジェクトに操作を実行できるようになります。 プロシージャにより、実行するプロセスとアクティビティが制御され、基になるデータベース オブジェクトが保護されます。 これにより個々のオブジェクト レベルで権限を与える必要がなくなり、セキュリティ階層が簡素化されます。  
  
 CREATE PROCEDURE ステートメントに [EXECUTE AS](/sql/t-sql/statements/execute-as-clause-transact-sql) 句を指定し、別のユーザーの権限を借用したり、ユーザーまたはアプリケーションが基のオブジェクトおよびコマンドに直接アクセスできる権限を持たなくても特定のデータベース アクティビティを実行できるようにすることができます。 たとえば、TRUNCATE TABLE など、許可する権限のない操作があります。 TRUNCATE TABLE を実行するには、指定されたテーブルの ALTER 権限がユーザーに許可されている必要があります。 ところが場合によっては、テーブルの ALTER 権限をユーザーに許可することは望ましくありません。これは、実質的にはテーブルの切り捨て以外の操作も実行できる権限をそのユーザーに許可することになるためです。 TRUNCATE TABLE ステートメントをモジュール内に組み込み、テーブルを変更する権限が許可されているユーザーとしてそのモジュールを実行するように指定すると、テーブルの切り捨てを行うための権限を、そのモジュールの EXECUTE 権限が許可されたユーザーに拡張できます。  
  
 ネットワークを介してプロシージャを呼び出すと、プロシージャの実行の呼び出しのみが表示されます。 したがって、悪意のあるユーザーがテーブルやデータベース オブジェクト名を表示したり、独自の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを埋め込んだり、重要なデータを検索したりすることができません。  
  
 プロシージャ パラメーターを使用することで、SQL インジェクション攻撃から保護することができます。 パラメーター入力は実行可能コードとしてではなく、リテラル値として処理されるため、攻撃者はプロシージャ内の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントにコマンドを挿入してセキュリティを損なうことが難しくなります。  
  
 プロシージャは暗号化できるため、ソース コードを難読化することができます。 詳細については、「 [SQL Server の暗号化](../security/encryption/sql-server-encryption.md)」を参照してください。  
  
 コードの再利用  
 繰り返し実行するデータベース操作のコードは、プロシージャにカプセル化するのに最適です。 これにより同じコードを再作成する必要がなくなり、コードの矛盾を低減して、必要な権限を持つユーザーまたはアプリケーションがコードにアクセスして実行できるようになります。  
  
 メンテナンスの簡素化  
 クライアント アプリケーションがプロシージャを呼び出し、データ層内にデータベース操作を維持する場合は、基のデータベースの変更に対してプロシージャのみを更新することが必要になります。 アプリケーション層は別に維持され、データベース レイアウト、リレーションシップ、またはプロセスの変更について認識する必要がありません。  
  
 パフォーマンスの向上  
 既定では、初回実行時にプロシージャがコンパイルされ、以降の実行時に再利用される実行プランが作成されます。 クエリ プロセッサは新しいプランを作成する必要がないため、通常のプロシージャの実行はそれほど時間がかかりません。  
  
 プロシージャにより参照されるテーブルまたはデータに大幅な変更があると、事前にコンパイルされているプランによりプロシージャの実行が遅くなる場合があります。 この場合には、プロシージャを再コンパイルするか、新しい実行プランを強制することにより、パフォーマンスを向上できます。  
  
## <a name="types-of-stored-procedures"></a>ストアド プロシージャの種類  
 ユーザー定義  
 ユーザー定義プロシージャは、ユーザー定義データベース、または **リソース** データベースを除くすべてのシステム データベースに作成できます。 プロシージャは [!INCLUDE[tsql](../../includes/tsql-md.md)] に開発するか、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイム (CLR) メソッドの参照として開発できます。  
  
 一時  
 一時プロシージャは、ユーザー定義プロシージャの 1 形式です。 一時プロシージャは永続的なプロシージャと同様ですが、一時プロシージャは **tempdb**に格納されることが異なります。 一時プロシージャには、ローカル一時プロシージャとグローバル一時プロシージャの 2 種類があります。 この 2 種類の一時テーブルでは、名前、表示設定、および可用性が異なります。 ローカル一時プロシージャ名の先頭には、番号記号 (#) が 1 つ付いています。このプロシージャは、作成したユーザーの現在の接続でのみ表示され、この接続が閉じられたときに削除されます。 グローバル一時プロシージャ名の先頭には、番号記号が 2 つ (##) 付いています。このプロシージャは、作成されるとすべてのユーザーに表示され、このプロシージャを使用する最後のセッションの終了時に削除されます。  
  
 System  
 システム プロシージャは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に含まれています。 物理的には内部の非表示 **リソース** データベースに格納されますが、論理的には各システム データベースとユーザー定義データベースの **sys** スキーマに表示されます。 さらに、 **msdb** データベースには、警告とジョブのスケジュール設定に使用される **dbo** スキーマ内にシステム ストアド プロシージャも含まれます。 システム プロシージャ名には **sp_** というプレフィックスが付くため、ユーザー定義プロシージャ名を付けるときにこのプレフィックスを使用しないようにすることをお勧めします。 すべてのシステム プロシージャの一覧については、「[システム ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から外部プログラムへの、さまざまなメンテナンス作業に使用するためのインターフェイスになるシステム プロシージャがサポートされます。 そのような拡張プロシージャには xp_ プレフィックスが付きます。 すべての拡張プロシージャの一覧については、「[汎用拡張ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql)」を参照してください。  
  
 拡張ユーザー定義  
 拡張プロシージャを使用すると、C などのプログラミング言語で外部ルーチンを作成できます。これらのプロシージャは DLL なので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで動的に読み込んで実行できます。  
  
> [!NOTE]  
>  拡張ストアド プロシージャは、今後のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションはできるだけ早く修正してください。 代わりに CLR プロシージャを作成してください。 この方法では、拡張プロシージャの記述に代わる、より堅牢でセキュリティ保護された手段が提供されます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**タスクの説明**|**トピック**|  
|ストアド プロシージャの作成方法を説明する|[ストアド プロシージャの作成](../stored-procedures/create-a-stored-procedure.md)|  
|ストアド プロシージャの変更方法を説明する|[ストアド プロシージャの変更](../stored-procedures/modify-a-stored-procedure.md)|  
|ストアド プロシージャの削除方法を説明する|[ストアド プロシージャの削除](../stored-procedures/delete-a-stored-procedure.md)|  
|ストアド プロシージャの実行方法を説明する|[ストアド プロシージャの実行](../stored-procedures/execute-a-stored-procedure.md)|  
|ストアド プロシージャの権限の許可方法を説明する|[ストアド プロシージャに対する権限の許可](../stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|ストアド プロシージャからアプリケーションにデータを返す方法を説明する|[ストアド プロシージャからデータを返す](../stored-procedures/return-data-from-a-stored-procedure.md)|  
|ストアド プロシージャの再コンパイル方法を説明する|[ストアド プロシージャの再コンパイル](../stored-procedures/recompile-a-stored-procedure.md)|  
|ストアド プロシージャ名の変更方法を説明する|[ストアド プロシージャの名前の変更](../stored-procedures/rename-a-stored-procedure.md)|  
|ストアド プロシージャの定義の表示方法を説明する|[ストアド プロシージャの定義の表示](view-the-definition-of-a-stored-procedure.md)|  
|ストアド プロシージャの依存関係の表示方法を説明する|[ストアド プロシージャの依存関係の表示](view-the-dependencies-of-a-stored-procedure.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
 [CLR ストアド プロシージャ](../../database-engine/dev-guide/clr-stored-procedures.md)  
  
  
