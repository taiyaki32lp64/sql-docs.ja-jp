---
title: パブリッシング ストアド プロシージャの実行 (トランザクション)
description: パブリッシャー側で実行され、ストアド プロシージャ実行アーティクルとしてトランザクション パブリケーションにパブリッシュされたテーブルに影響を与える方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], stored procedures and
- transactional replication, publishing stored procedure execution
ms.assetid: f4686f6f-c224-4f07-a7cb-92f4dd483158
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: ad8e489d753587912eb7369316c1413bd1eaf1c9
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321413"
---
# <a name="publishing-stored-procedure-execution-in-transactional-replication"></a>トランザクション レプリケーションにおけるパブリッシング ストアド プロシージャの実行
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  パブリッシャー側で実行され、パブリッシュされたテーブルに影響を与えるストアド プロシージャがある場合、それらのストアド プロシージャをストアド プロシージャ実行アーティクルとしてパブリケーションに含めることを検討してください。 プロシージャの定義 (CREATE PROCEDURE ステートメント) はサブスクリプションが初期化されるときにサブスクライバーにレプリケートされます。プロシージャがパブリッシャーで実行されるときに、レプリケーションは対応するプロシージャをサブスクライバーで実行します。 これにより、各行の個別の変更のレプリケーションが回避されてプロシージャの実行のみがレプリケートされるため、大量のバッチ操作が実行される場合にはパフォーマンスが著しく向上します。 たとえば、パブリケーション データベースで次のストアド プロシージャを作成するとします。  
  
```  
CREATE PROC give_raise AS  
UPDATE EMPLOYEES SET salary = salary * 1.10  
```  
  
 このプロシージャでは、社内 10,000 人の各従業員に 10% の昇給を行います。 パブリッシャーでこのストアド プロシージャを実行すると、各従業員の基本給が更新されます。 ストアド プロシージャの実行をレプリケートしない場合、この更新は大規模な何段階ものトランザクションとしてサブスクライバーに送信されます。  
  
```  
BEGIN TRAN  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 1'  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 2'  
```  
  
 これが 10,000 件の更新分について繰り返されます。  
  
 ストアド プロシージャの実行をレプリケートする場合、レプリケーションは、サブスクライバー側でストアド プロシージャを実行するコマンドのみを送信します。すべての更新をディストリビューション データベースに書き込んでからネットワークを経由してサブスクライバーに送信する必要はありません。  
  
```  
EXEC give_raise  
```  
  
> [!IMPORTANT]  
>  ストアド プロシージャのレプリケーションは、すべてのアプリケーションに適しているわけではありません。 サブスクライバーとは異なる行のセットがパブリッシャーに存在するようにアーティクルが行方向でフィルター選択される場合、両方で同じストアド プロシージャを実行すると異なる結果が返ります。 同様に、レプリケートされていない別のテーブルのサブクエリに基づいた更新の場合、パブリッシャー側とサブスクライバー側の両方で同じストアド プロシージャを実行しても異なる結果が返ります。  
  
 **ストアド プロシージャの実行をパブリッシュするには**  
  
-   SQL Server Management Studio:[トランザクション パブリケーションでのストアド プロシージャの実行のパブリッシュ (SQL Server Management Studio)](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
-   レプリケーション Transact-SQL プログラミング: [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) を実行し、パラメーター `@type` に対して値 "serializable proc exec" (推奨) または "proc exec" を指定します。 アーティクルの定義の詳細については、「[Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」 (アーティクルの定義) を参照してください。  
  
## <a name="modifying-the-procedure-at-the-subscriber"></a>サブスクライバーでのプロシージャの変更  
 既定では、パブリッシャー上のストアド プロシージャの定義は各サブスクライバーに反映されます。 ただし、サブスクライバーでストアド プロシージャを変更することもできます。 これは、パブリッシャーとサブスクライバーで異なるロジックを実行する場合に便利です。 たとえば、2 つの関数を持つパブリッシャー上のストアド プロシージャ、 **sp_big_delete**を考えてみます。このストアド プロシージャはレプリケートされたテーブル **big_table1** から 100 万行を削除し、レプリケートされていないテーブル **big_table2**を更新します。 ネットワーク リソースの需要を削減するには、 **sp_big_delete**をパブリッシュすることによって、100 万行の削除をストアド プロシージャとして反映する方が効率的です。 サブスクライバーでは、100 万行だけを削除し、 **big_table2** への更新を実行しないように **sp_big_delete**を変更できます。  
  
> [!NOTE]  
>  既定では、パブリッシャーで ALTER PROCEDURE を使用して行われたすべての変更はサブスクライバーに反映されます。 これを防ぐには、ALTER PROCEDURE を実行する前に、スキーマの変更の反映を無効にしてください。 スキーマ変更の詳細については、「[パブリケーション データベースでのスキーマの変更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
## <a name="types-of-stored-procedure-execution-articles"></a>ストアド プロシージャ実行アーティクルの種類  
 ストアド プロシージャの実行をパブリッシュするには、シリアル化可能なプロシージャ実行アーティクルとプロシージャ実行アーティクルの 2 種類の方法があります。  
  
-   シリアル化可能オプションでは、プロシージャがシリアル化可能なトランザクションのコンテキスト内で実行される場合にのみ、プロシージャの実行がレプリケートされるため、このオプションをお勧めします。 ストアド プロシージャがシリアル化可能なトランザクションの外から実行される場合、パブリッシュされたテーブルのデータに対する変更は一連の DML ステートメントとしてレプリケートされます。 この動作により、サブスクライバー上のデータとパブリッシャー上のデータの一貫性が保たれます。 これは、たとえば大規模なクリーンアップ操作などの、バッチ操作に特に便利です。  
  
-   プロシージャ実行オプションを使用すると、ストアド プロシージャ内の個々のステートメントが成功したかどうかにかかわらず、すべてのサブスクライバーに実行がレプリケートされる可能性があります。 さらに、ストアド プロシージャによって生じるデータの変更は複数のトランザクションで発生する可能性があるので、サブスクライバー上のデータとパブリッシャー上のデータに一貫性がなくなる可能性があります。 このような問題に対処するには、サブスクライバーが読み取り専用であることと、READ UNCOMMITTED より高い分離レベルを使用していることが必要です。 READ UNCOMMITTED を使用する場合、パブリッシュされたテーブルのデータに対する変更は一連の DML ステートメントとしてレプリケートされます。  
  
 次の例は、プロシージャのレプリケーションを、シリアル化可能なプロシージャ アーティクルとして設定することの利点を示します。  
  
```  
BEGIN TRANSACTION T1  
SELECT @var = max(col1) FROM tableA  
UPDATE tableA SET col2 = <value>   
   WHERE col1 = @var   
  
BEGIN TRANSACTION T2  
INSERT tableA VALUES <values>  
COMMIT TRANSACTION T2  
```  
  
 この例では、トランザクション T1 にある SELECT が、トランザクション T2 の INSERT よりも先に発生すると想定しています。  
  
 このプロシージャが、シリアル化可能なトランザクション内で実行 (分離レベルを SERIALIZABLE に設定して実行) されないと、トランザクション T2 では T1 の SELECT ステートメントの範囲内に新しい行を挿入し、それを T1 より先にコミットすることが許可されます。 これは、T1 よりも先にサブスクライバーで挿入が適用されることも意味します。 サブスクライバーに T1 が適用されると、SELECT によってパブリッシャーとは異なる値が返される可能性があり、UPDATE からの出力が異なる結果になる可能性もあります。  
  
 このプロシージャが、シリアル化可能なトランザクションの中で実行される場合には、トランザクション T2 で、T2 の SELECT ステートメントの範囲に挿入を行うことが許可されません。 T1 がコミットするまでブロックされて、サブスクライバーでの結果が同じになるようにします。  
  
 シリアル化可能なトランザクション内でプロシージャを実行するときにはロックがより長く保持されるので、コンカレンシーが少なくなることもあります。  
  
## <a name="the-xact_abort-setting"></a>XACT_ABORT の設定  
 ストアド プロシージャの実行をレプリケートする場合、ストアド プロシージャを実行するセッションの設定では XACT_ABORT を ON に指定する必要があります。 XACT_ABORT が OFF に設定されていて、パブリッシャーでプロシージャの実行中にエラーが発生した場合、サブスクライバーでも同じエラーが発生し、ディストリビューション エージェントは失敗します。 XACT_ABORT を  ON に指定すると、パブリッシャーでプロシージャの実行中にエラーが発生した場合、実行全体がロールバックされ、ディストリビューション エージェントの失敗を回避できます。 XACT_ABORT 設定の詳細については、「[SET XACT_ABORT &#40;Transact-SQL&#41;](../../../t-sql/statements/set-xact-abort-transact-sql.md)」を参照してください。  
  
 XACT_ABORT を OFF に設定する必要がある場合は、ディストリビューション エージェントの **-SkipErrors** パラメーターを指定してください。 これで、エラーが発生した場合でも、エージェントは引き続きサブスクライバーに変更を適用できます。  
  
## <a name="see-also"></a>参照  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
