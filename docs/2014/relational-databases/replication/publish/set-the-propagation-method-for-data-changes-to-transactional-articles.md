---
title: データの変更をトランザクション アーティクルに反映する方法の設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db74bd7de8fcf3cdba6787fda18c510237d63372
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941081"
---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>データの変更をトランザクション アーティクルに反映する方法の設定
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、トランザクション アーティクルへのデータの変更の反映方法を設定する方法について説明します。  
  
 既定では、トランザクション レプリケーションは、各アーティクルのストアド プロシージャ セットを使用して変更内容をサブスクライバーに反映します。 これらのプロシージャはカスタム プロシージャに置換することができます。 詳しくは、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   **データの変更をトランザクション アーティクルに反映する方法を設定するために、使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   レプリケーションによって生成されたスナップショット ファイルを編集する場合には注意が必要です。 カスタム ストアド プロシージャのカスタム ロジックをテストしてサポートする必要があります。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ではカスタム ロジックをサポートしていません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 反映方法は、パブリケーションの新規作成ウィザードからアクセスできる **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[プロパティ]** タブで指定します。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](create-a-publication.md)」および「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-specify-the-propagation-method"></a>反映方法を指定するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスでテーブルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[ステートメントの配信]** セクションで、 **[INSERT 配信形式]** 、 **[UPDATE 配信形式]** 、 **[DELETE 配信形式]** の各メニューを使用して各操作の反映方法を指定します。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
#### <a name="to-generate-and-use-custom-stored-procedures"></a>カスタム ストアド プロシージャを生成して使用するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスでテーブルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
     **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[ステートメントの配信]** セクションで、該当する配信形式メニュー ( **[INSERT 配信形式]** 、 **[UPDATE 配信形式]** 、または **[DELETE 配信形式]** ) から CALL 構文を選択し、 **[INSERT ストアド プロシージャ]** 、 **[DELETE ストアド プロシージャ]** 、または **[UPDATE ストアド プロシージャ]** で使用するプロシージャ名を入力します。 CALL 構文の詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」の「ストアド プロシージャの呼び出し構文」を参照してください。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
5.  パブリケーションのスナップショットが生成されると、そのスナップショットには前の手順で指定したプロシージャが含まれています。 このプロシージャは指定した CALL 構文を使用しますが、レプリケーションが使用する既定のロジックを含んでいます。  
  
     スナップショットが生成された後、このアーティクルが属するパブリケーションのスナップショット フォルダーに移動し、アーティクルと同じ名前の **.sch** ファイルを見つけます。 メモ帳などのテキスト エディターでこのファイルを開き、挿入、更新、または削除の各ストアド プロシージャで CREATE PROCEDURE コマンドを検索し、プロシージャ定義を編集してデータの変更を反映するためのカスタム ロジックを指定します。 スナップショットが再生成された場合は、カスタム プロシージャを再作成する必要があります。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 トランザクション レプリケーションでは、パブリッシャーからサブスクライバーへの変更の反映方法を制御できます。この反映メソッドは、アーティクルの作成時やその後の変更時に、レプリケーションのストアド プロシージャを使用してプログラムから設定できます。  
  
> [!NOTE]  
>  パブリッシュされたデータ行に適用される DML (データ操作言語) 操作には、挿入、更新、削除などがありますが、各種の操作に対して異なる反映メソッドを指定できます。  
  
 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>データ変更を Transact-SQL コマンドを使って反映するアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)を実行します。 パブリケーションのアーティクルが属し **\@**  **\@** ているパブリケーションの名前、アーティクルのアーティクル名、  **\@source_object**にパブリッシュされるデータベースオブジェクト、および値を指定します。次のパラメーターのうち少なくとも1つに対する**SQL**の。  
  
    -   ins_cmd- [INSERT](/sql/t-sql/statements/insert-transact-sql)コマンドのレプリケーションを制御します。  **\@**  
  
    -   upd_cmd- [UPDATE](/sql/t-sql/queries/update-transact-sql)コマンドのレプリケーションを制御します。  **\@**  
  
    -   del_cmd- [DELETE](/sql/t-sql/statements/delete-transact-sql)コマンドのレプリケーションを制御します。  **\@**  
  
    > [!NOTE]  
    >  上記のパラメーターに対して **SQL** を指定すると、各種のコマンドが適切な [!INCLUDE[tsql](../../../includes/tsql-md.md)] コマンドとしてサブスクライバーにレプリケートされます。  
  
     詳しくは、「 [アーティクルを定義](define-an-article.md)」をご覧ください。  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>データ変更を反映しないアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)を実行します。 パブリケーションのアーティクルが属し **\@**  **\@** ているパブリケーションの名前、アーティクルのアーティクル名、  **\@source_object**にパブリッシュされるデータベースオブジェクト、および値を指定します。次のパラメーターの少なくとも1つではあり**ません**。  
  
    -   ins_cmd- [INSERT](/sql/t-sql/statements/insert-transact-sql)コマンドのレプリケーションを制御します。  **\@**  
  
    -   upd_cmd- [UPDATE](/sql/t-sql/queries/update-transact-sql)コマンドのレプリケーションを制御します。  **\@**  
  
    -   del_cmd- [DELETE](/sql/t-sql/statements/delete-transact-sql)コマンドのレプリケーションを制御します。  **\@**  
  
    > [!NOTE]  
    >  上記のパラメーターに対して **NONE** を指定すると、対応するコマンドはサブスクライバーにレプリケートされません。  
  
     詳しくは、「 [アーティクルを定義](define-an-article.md)」をご覧ください。  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>ユーザーが変更したカスタム ストアド プロシージャを含むアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)を実行します。 **\@**  **\@** **パブリケーションのアーティクルが属しているパブリケーションの名前、アーティクルのアーティクル、source_objectにパブリッシュするデータベースオブジェクト、の値を指定します。\@** 値**0x02** (カスタムストアドプロシージャの自動生成を有効にする) と、次のパラメーターの少なくとも1つを含む **schema_optionビット\@** マスク。  
  
    -   ins_cmd- <strong>CALL sp_MSins_*article_name*</strong>の値を指定します。ここで、 **_article_name_** は **\@article**に指定された値です。  **\@**  
  
    -   **\@del_cmd** - <strong>CALL sp_MSdel_*article_name ** または ** XCALL sp_MSdel_</strong>article_name*** を指定します。ここで、<strong>article_name*は*</strong>article** に指定した値です。  
  
    -   upd_cmd- <strong>scall sp_MSupd_*article_name*</strong>、 <strong>CALL sp_MSupd_*article_name*</strong>、 <strong>XCALL sp_MSupd__article_name *</strong>、または<strong>MCALL sp_MSupd_* article_name *</strong>の値を指定します。  **\@** _**article_name**_ は、  **\@アーティクル**に指定された値です。  
  
    > [!NOTE]  
    >  上記コマンド パラメーターのそれぞれについて、レプリケーションによって生成されるストアド プロシージャに独自の名前を指定できます。  
  
    > [!NOTE]  
    >  CALL、SCALL、XCALL、MCALL の各構文の詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
     詳しくは、「 [アーティクルを定義](define-an-article.md)」をご覧ください。  
  
2.  スナップショットが生成された後、このアーティクルが属するパブリケーションのスナップショット フォルダーに移動し、アーティクルと同じ名前の **.sch** ファイルを見つけます。 このファイルを Notepad.exe で開き、挿入、更新、削除のストアド プロシージャに対応する CREATE PROCEDURE コマンドを見つけ、そのプロシージャ定義を編集して、データ変更を反映するためのカスタム ロジックを指定します。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>カスタム ストアド プロシージャにデータ変更を反映するカスタム スクリプトを含むアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)を実行します。 **\@**  **\@** **パブリケーションのアーティクルが属しているパブリケーションの名前、アーティクルのアーティクル、source_objectにパブリッシュするデータベースオブジェクト、の値を指定します。\@** 値**0x02** (カスタムストアドプロシージャの自動生成を有効にする) と、次のパラメーターの少なくとも1つを含む **schema_optionビット\@** マスク。  
  
    -   ins_cmd- <strong>CALL sp_MSins_*article_name*</strong>の値を指定します。ここで、 _**article_name**_ は **\@article**に指定された値です。  **\@**  
  
    -   **\@del_cmd** - <strong>CALL sp_MSdel_*article_name ** または ** XCALL sp_MSdel_</strong>article_name*** を指定します。ここで、<strong>article_name*は*</strong>article_ に指定した値です。  
  
    -   **\@upd_cmd** - *<strong>SCALL sp_MSupd_*article_name***、** CALL sp_MSupd_</strong>article_name***、*<strong>XCALL sp_MSupd_*article_name***、** MCALL sp_MSupd_</strong>article_name*** を指定します。ここで、<strong>article_name*は*</strong>article<strong> に指定した値です。  
  
    > [!NOTE]  
    >  上記コマンド パラメーターのそれぞれについて、レプリケーションによって生成されるストアド プロシージャに独自の名前を指定できます。  
  
    > [!NOTE]  
    >  CALL、SCALL、XCALL、MCALL の各構文の詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
     詳しくは、「 [アーティクルを定義](define-an-article.md)」をご覧ください。  
  
2.  パブリッシャーのパブリケーション データベースで、 [ALTER PROCEDURE](/sql/t-sql/statements/alter-procedure-transact-sql) ステートメントを使用して、挿入、更新、および削除のカスタム ストアド プロシージャに対応する [CREATE PROCEDURE](/sql/relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql) スクリプトが返されるように [sp_scriptpublicationcustomprocs](/sql/t-sql/statements/create-procedure-transact-sql) を編集します。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>既存のアーティクルの変更反映メソッドを変更するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)を実行します。 **\@パブリケーション**、**アーティクル、値 ins_cmd、upd_cmd、または del_cmd をプロパティに指定し、適切な反映方法を指定します。 \@**  **\@**  **\@値**。  
  
2.  変更対象の各反映メソッドについて、手順 1. を繰り返します。  
  
## <a name="see-also"></a>関連項目  
 [トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [パブリケーションを作成する](create-a-publication.md)  
  
  
