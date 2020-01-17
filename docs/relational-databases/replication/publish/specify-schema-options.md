---
title: SQL Server レプリケーションのスキーマ オプションを指定する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e2ac7116c1d7c402ac2b15e4168c64339da34998
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908122"
---
# <a name="specify-schema-options-for-sql-server-replication"></a>SQL Server レプリケーションのスキーマ オプションを指定する
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
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
  
-   すべてのスキーマ オプションの一覧については、「[sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)」および「[sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」の `@schema_option` パラメーターをご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 スキーマ オプション (制約やトリガーをサブスクライバーにコピーするかどうかなど) は、 **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブで指定します。 このタブは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで使用できます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
#### <a name="to-specify-schema-options"></a>スキーマ オプションを指定するには  
  
1.  パブリケーションの新規作成ウィザードまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、アーティクルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  スキーマ オプションの変更を適用するアーティクルを選択します。  
  
    -   **[反転表示された \<ObjectType> アーティクルのプロパティを設定]** をクリックし、 **[アーティクルのプロパティ - \<ObjectName>]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、 **[アーティクル]** ページのオブジェクト ペインで反転表示されたオブジェクトだけに適用されます。  
  
    -   **[すべての \<ObjectType> アーティクルのプロパティを設定]** をクリックし、 **[すべての \<ObjectType> アーティクルのプロパティ]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、パブリケーションが選択されていないオブジェクトも含めた、 **[アーティクル]** ページのオブジェクト ペインにあるこの種類のすべてのオブジェクトに適用されます。  
  
        > [!NOTE]  
        >  **[すべての \<ObjectType&gt; アーティクルのプロパティ]** ダイアログ ボックスで行われたプロパティの変更は、 **[アーティクルのプロパティ - \<ObjectName&gt;]** ダイアログ ボックスで以前行われたすべての変更をオーバーライドします。 たとえば、あるオブジェクトの種類のすべてのアーティクルに対して複数の既定を設定し、かつそれぞれのオブジェクトに対してプロパティを設定する場合には、最初にすべてのアーティクルに対する既定を設定します。 次に、それぞれのオブジェクトに対してプロパティを設定します。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[サブスクライバーへのオブジェクトと設定のコピー]** および **[対象オブジェクト]** セクションで、オプションの値を設定します。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
5.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 スキーマ オプションは、1 つまたは複数のオプションについて、 [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) を実行した結果を 16 進数値で指定します。 詳細については、「 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 」および「 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  ビットごとの演算を実行する際は、あらかじめ、スキーマ オプションの値を **binary** から **int** に変換しておく必要があります。 詳細については、「[CAST and CONVERT &#40;Transact-SQL&#41;](../../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのアーティクルを定義するときにスキーマ オプションを指定するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前、`@article` にアーティクル名、`@source_object` にパブリッシュするデータベース オブジェクト、`@type` にデータベース オブジェクトの型を指定し、さらに、1 つまたは複数のスキーマ オプションに対する [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) の結果を `@schema_option` に指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>マージ パブリケーションのアーティクルを定義するときにスキーマ オプションを指定するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前、`@article` にアーティクル名、`@source_object` にパブリッシュするデータベース オブジェクトを指定し、さらに、1 つまたは複数のスキーマ オプションに対する [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) の結果を `@schema_option` に指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの既存のアーティクルに設定されているスキーマ オプションを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)を実行します。 `@publication` と `@article` に、それぞれアーティクルが属しているパブリケーションの名前およびアーティクル名を指定します。 結果セットの `schema_option` 列の値を確認します。  
  
2.  手順 1 の値、および必要なスキーマ オプションの値を使って [& (ビット演算 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 演算を実行し、対象のオプションが設定されているかどうかを確認します。  
  
    -   実行結果が **0**の場合、オプションは設定されていません。  
  
    -   実行結果がオプションの値の場合、そのオプションは既に設定されています。  
  
3.  オプションが設定されていなかった場合は、手順 1. の値と、必要なスキーマ オプション値を使って [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 演算を実行します。  
  
4.  パブリッシャーのパブリケーション データベースで [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前を、`@article` にアーティクル名を、`@property` の値に `schema_option` を指定し、さらに、手順 3 で得られた 16 進数値を `@value` に指定します。  
  
5.  スナップショット エージェントを実行して、新しいスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>マージ パブリケーションの既存のアーティクルのスキーマ オプションを変更するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)を実行します。 `@publication` と `@article` に、それぞれアーティクルが属しているパブリケーションの名前およびアーティクル名を指定します。 結果セットの **schema_option** 列の値を確認してください。  
  
2.  手順 1 の値、および必要なスキーマ オプションの値を使って [& (ビット演算 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 演算を実行し、対象のオプションが設定されているかどうかを確認します。  
  
    -   実行結果が **0**の場合、オプションは設定されていません。  
  
    -   実行結果がオプションの値の場合、そのオプションは既に設定されています。  
  
3.  オプションが設定されていなかった場合は、手順 1. の値と、必要なスキーマ オプション値を使って [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 演算を実行します。  
  
4.  パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前を、`@article` にアーティクル名を、`@property` の値に `schema_option` を指定し、さらに、手順 3 で得られた 16 進数値を `@value` に指定します。  
  
5.  スナップショット エージェントを実行して、新しいスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご参照ください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [トランザクション レプリケーションのアーティクル オプション](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
