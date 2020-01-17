---
title: '[順序のプロパティ] ([全般] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sequence.general.f1
ms.assetid: 0187f413-cdf0-48a2-b2e6-9b3578cd5811
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 846e7960e9aca4bfb5deea8f50eae3c8a2f58c70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184442"
---
# <a name="sequence-properties-general-page"></a>[順序のプロパティ]\([全般] ページ)
  シーケンス オブジェクトを作成し、そのプロパティを指定します。 シーケンスは、シーケンスが作成された仕様に従って数値のシーケンスを生成するユーザー定義のスキーマ バインド オブジェクトです。 数値のシーケンスは、定義された間隔で昇順または降順に生成され、要求に応じて再起動 (繰り返し) するように構成できます。 ID 列とは異なり、シーケンスは、特定のテーブルに関連付けられていません。 アプリケーションは、シーケンス オブジェクトを参照して、次の値を受け取ります。 シーケンスとテーブルの関係は、アプリケーションによって制御されます。 ユーザー アプリケーションは、シーケンス オブジェクトを参照し、複数の行とテーブル間で値を調整できます。  
  
 挿入時に生成される ID 列値とは異なり、アプリケーションで [NEXT VALUE の関数](/sql/t-sql/functions/next-value-for-transact-sql)を呼び出すことで、行を挿入せずに次のシーケンス番号を取得できます。 一度に複数のシーケンス番号を取得するには、 [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql) を使用します。  
  
 **CREATE SEQUENCE** および **NEXT VALUE FOR** 関数を両方使用する場合の詳細およびシナリオについては、「 [シーケンス番号](sequence-numbers.md)」をご覧ください。  
  
 このページには 2 とおりの方法でアクセスできます。オブジェクト エクスプローラーで **[シーケンス]** を右クリックして **[新しいシーケンス]** をクリックするか、既存のシーケンスを右クリックして **[プロパティ]** をクリックします。 既存のシーケンスを右クリックして **[プロパティ]** をクリックした場合は、オプションは編集不可能です。 シーケンス オプションを変更するには、[ALTER SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-sequence-transact-sql) ステートメントを使用するか、シーケンス オブジェクトを削除してから再作成してください。  
  
## <a name="options"></a>および  
 **[シーケンス名]**  
 ここにシーケンス名を入力します。  
  
 **[シーケンス スキーマ]**  
 このシーケンスを所有するスキーマを指定します。  
  
 **データ型**  
 シーケンスを任意の整数型として定義できます。 この機能には、次が含まれます。  
  
|データ型|範囲|  
|---------------|-----------|  
|`tinyint`|0 ～ 255|  
|`smallint`|-32,768 ～ 32,767|  
|`int`|-2,147,483,648 ～ 2,147,483,647|  
|`bigint`|-9,223,372,036,854,775,808 ～ 9,223,372,036,854,775,807|  
  
-   `decimal` または `numeric` の場合、小数点以下を含みません。  
  
-   これらの種類のいずれかに基づいている、すべてのユーザー定義データ型 (別名型) です。  
  
 **Precision**  
 `decimal` データ型または `numeric` データ型については、有効桁数を指定します (小数点以下桁数は常に 0 です)。  
  
 **[開始値]**  
 シーケンス オブジェクトによって返される最初の値です。 **START** 値は、シーケンス オブジェクトの最小値以上および最大値以下にする必要があります。 新しいシーケンス オブジェクトの既定の開始値は、昇順のシーケンス オブジェクトの最小値および降順のシーケンス オブジェクトの最大値です。  
  
 **[増分]**  
 **NEXT VALUE FOR** 関数を呼び出すたびに必要なシーケンス オブジェクトの値を増分 (負の場合は減少) させるのに使用される値です。 増分値が負の値の場合はシーケンス オブジェクトは降順で、それ以外の場合は昇順です。 0 は増分として使用できません。  
  
 **最小値**  
 シーケンスのオブジェクトの境界を指定します。 新しいシーケンス オブジェクトの既定の最小値は、シーケンス オブジェクトのデータ型の最小値です。 これは、0、`tinyint`データ型とその他のすべてのデータ型の負の数。  
  
 **最大値**  
 シーケンスのオブジェクトの境界を指定します。 新しいシーケンス オブジェクトの既定の最大値は、シーケンス オブジェクトのデータ型の最大値です。  
  
 **制限に達するとサイクルのシーケンスが再起動します。**  
 オンにすると、最小値または最大値を超過した場合、シーケンス オブジェクトを最小値 (または降順シーケンス オブジェクトの最大値) から再起動することができます。  
  
> [!NOTE]  
>  サイクルは開始値からではなく最小値または最大値から再起動されます。  
  
 **[キャッシュ オプション]**  
 シーケンス値のキャッシュを作成し、シーケンス番号を作成するのに必要なディスク IO の数を最小限に抑えることで、シーケンス オブジェクトを使用するアプリケーションのパフォーマンスを向上できます。  
  
-   既定のキャッシュ サイズ - [!INCLUDE[ssDE](../../includes/ssde-md.md)] によってサイズが選択されますが、選択が一貫していない場合があるため、注意が必要です。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、予告なしにキャッシュ サイズの算出方法を変更する場合があります。  
  
-   キャッシュなし - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではシーケンス番号がキャッシュに格納されません。  
  
-   キャッシュ サイズ - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではシーケンス値をキャッシュに格納します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、現在の値とキャッシュに残された値の数を追跡します。 したがって、キャッシュを格納するために必要なメモリ量は、常にシーケンス オブジェクトのデータ型の 2 つのインスタンスと等しくなります。  
  
 CACHE オプションを使用してシーケンス番号を作成する際に予期しないシャットダウン (電源障害など) が発生すると、キャッシュ内のシーケンス番号が失われる可能性があります。  
  
 CREATE SEQUENCE のオプションの詳細については、「[CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 SCHEMA に対する **CREATE SEQUENCE**権限、 **ALTER**権限、または **CONTROL** 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [sys.sequences &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sequences-transact-sql)  
  
  
