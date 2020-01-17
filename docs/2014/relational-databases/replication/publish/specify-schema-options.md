---
title: スキーマ オプションの指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e6826d28ec923de221e94b985b740a172bdaa7d5
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882166"
---
# <a name="specify-schema-options"></a>Specify Schema Options
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、スキーマのオプションを指定する方法について説明します。 テーブルまたはビューをパブリッシュするとき、パブリッシュされたオブジェクト用にレプリケートされるオブジェクトの作成オプションを制御できます。 アーティクルが作成されるときにこれらのオプションを設定することができ、後で変更することもできます。 アーティクルに対してオプションを明示的に指定しなかった場合、既定のオプションが定義されます。  
  
> [!NOTE]  
>  レプリケーションのストアド プロシージャを使用した場合の既定のスキーマ オプションは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使ってアーティクルを追加するときの既定のオプションとは異なる場合があります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
-   **スキーマ オプションを指定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーションの作成後にスキーマ オプションを変更する場合は、新しいスナップショットを生成する必要があります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   スキーマオプションの完全な一覧については、 [ &#40;sp_addarticle transact-sql&#41; ](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)と[sp_addmergearticle &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)の **\@schema_option**パラメーターを参照してください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 スキーマ オプション (制約やトリガーをサブスクライバーにコピーするかどうかなど) は、 **[アーティクルのプロパティ -** Article>] **ダイアログ ボックスの \<[プロパティ]** タブで指定します。 このタブは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで使用できます。 ウィザードの使用とダイアログ ボックスへのアクセスの詳細については、「[Create a Publication](create-a-publication.md)」(パブリケーションの作成) と「[パブリケーション プロパティの表示と変更](view-and-modify-publication-properties.md)」をご覧ください。  
  
#### <a name="to-specify-schema-options"></a>スキーマ オプションを指定するには  
  
1.  パブリケーションの新規作成ウィザードまたは **[パブリケーションのプロパティ -** Publication>] **ダイアログ ボックスの \<[アーティクル]** ページで、アーティクルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  スキーマ オプションの変更を適用するアーティクルを選択します。  
  
    -   **[反転表示された \<ObjectType> アーティクルのプロパティを設定]** をクリックし、 **[アーティクルのプロパティ - \<ObjectName>]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、 **[アーティクル]** ページのオブジェクト ペインで反転表示されたオブジェクトだけに適用されます。  
  
    -   **[すべての \<ObjectType> アーティクルのプロパティを設定]** をクリックし、 **[すべての \<ObjectType> アーティクルのプロパティ]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、パブリケーションが選択されていないオブジェクトも含めた、 **[アーティクル]** ページのオブジェクト ペインにあるこの種類のすべてのオブジェクトに適用されます。  
  
        > [!NOTE]  
        >  **[すべての \<ObjectType&gt; アーティクルのプロパティ]** ダイアログ ボックスで行われたプロパティの変更は、 **[アーティクルのプロパティ - \<ObjectName&gt;]** ダイアログ ボックスで以前行われたすべての変更をオーバーライドします。 たとえば、あるオブジェクトの種類のすべてのアーティクルに対して複数の既定を設定し、かつそれぞれのオブジェクトに対してプロパティを設定する場合には、最初にすべてのアーティクルに対する既定を設定します。 次に、それぞれのオブジェクトに対してプロパティを設定します。  
  
3.  **[アーティクルのプロパティ -** Article>]**ダイアログ ボックスの**[プロパティ]**タブの**[サブスクライバーへのオブジェクトと設定のコピー] **および \<[対象オブジェクト]** セクションで、オプションの値を設定します。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
5.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 スキーマ オプションは、1 つまたは複数のオプションについて、 [| (ビット演算 OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) を実行した結果を 16 進数値で指定します。 詳細については、「 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 」および「 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  ビットごとの演算を実行する際は、あらかじめ、スキーマ オプションの値を **binary** から **int** に変換しておく必要があります。 詳細については、「[CAST and CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)」を参照してください。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのアーティクルを定義するときにスキーマ オプションを指定するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)を実行します。 **\@パブリケーション**のアーティクルが属しているパブリケーションの名前、 **\@アーティクル**のアーティクルの名前、 **\@source_object**にパブリッシュされるデータベースオブジェクト、 **\@型**のデータベースオブジェクトの種類、および | を指定します。 [(ビットごとの OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) **\@schema_option**の1つ以上のスキーマオプションの結果。 詳しくは、「 [アーティクルを定義](define-an-article.md)」をご覧ください。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>マージ パブリケーションのアーティクルを定義するときにスキーマ オプションを指定するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)を実行します。 **\@パブリケーション**のアーティクルが属しているパブリケーションの名前、 **\@アーティクル**のアーティクルの名前、 **\@source_object**にパブリッシュされるデータベースオブジェクト、および | を指定します。 [(ビットごとの OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) **\@schema_option**の1つ以上のスキーマオプションの結果。 詳しくは、「 [アーティクルを定義](define-an-article.md)」をご覧ください。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの既存のアーティクルに設定されているスキーマ オプションを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)を実行します。 **\@パブリケーション**のアーティクルが属しているパブリケーションの名前と、 **\@アーティクル**のアーティクルの名前を指定します。 結果セットの **schema_option** 列の値を確認してください。  
  
2.  手順 1 の値、および必要なスキーマ オプションの値を使って [& (ビット演算 AND)](/sql/t-sql/language-elements/bitwise-and-transact-sql) 演算を実行し、対象のオプションが設定されているかどうかを確認します。  
  
    -   実行結果が **0**の場合、オプションは設定されていません。  
  
    -   実行結果がオプションの値の場合、そのオプションは既に設定されています。  
  
3.  オプションが設定されていなかった場合は、手順 1. の値と、必要なスキーマ オプション値を使って [| (ビット演算 OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 演算を実行します。  
  
4.  パブリッシャーのパブリケーション データベースで [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)を実行します。 **\@パブリケーション**のアーティクルが属しているパブリケーションの名前、 **\@アーティクル**のアーティクルの名前、 **\@プロパティ**に**schema_option**値、および手順 3. の16進数の結果を **\@値**に指定します。  
  
5.  スナップショット エージェントを実行して、新しいスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)」をご参照ください。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>マージ パブリケーションの既存のアーティクルのスキーマ オプションを変更するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)を実行します。 **\@パブリケーション**のアーティクルが属しているパブリケーションの名前と、 **\@アーティクル**のアーティクルの名前を指定します。 結果セットの **schema_option** 列の値を確認してください。  
  
2.  手順 1 の値、および必要なスキーマ オプションの値を使って [& (ビット演算 AND)](/sql/t-sql/language-elements/bitwise-and-transact-sql) 演算を実行し、対象のオプションが設定されているかどうかを確認します。  
  
    -   実行結果が **0**の場合、オプションは設定されていません。  
  
    -   実行結果がオプションの値の場合、そのオプションは既に設定されています。  
  
3.  オプションが設定されていなかった場合は、手順 1. の値と、必要なスキーマ オプション値を使って [| (ビット演算 OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 演算を実行します。  
  
4.  パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 **\@パブリケーション**のアーティクルが属しているパブリケーションの名前、 **\@アーティクル**のアーティクルの名前、 **\@プロパティ**に**schema_option**値、および手順 3. の16進数の結果を **\@値**に指定します。  
  
5.  スナップショット エージェントを実行して、新しいスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)」をご参照ください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](publish-data-and-database-objects.md)   
 [トランザクション レプリケーションのアーティクル オプション](../transactional/article-options-for-transactional-replication.md)  
  
  
