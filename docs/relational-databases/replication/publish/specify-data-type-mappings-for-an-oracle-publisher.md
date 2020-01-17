---
title: Oracle パブリッシャーでのデータ型マッピング
description: SQL Server Management Studio (SSMS) を使用して SQL Server で Oracle パブリッシャーのデータ型マッピングを指定する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8449d7c6c766824628c3352897c25303f10e3a29
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320765"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Oracle パブリッシャーのデータ型マッピングの指定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、Oracle パブリッシャーのデータ型マッピングを指定する方法について説明します。 Oracle パブリッシャーには一連の既定のデータ型マッピングが用意されていますが、パブリケーションによっては、こうした既定のマッピングとは異なるマッピングの指定が必要になる場合もあります。  
  
 **このトピックの内容**  
  
-   **Oracle パブリッシャーのデータ型マッピングを指定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 データ型マッピングは、 **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[データのマッピング]** タブで指定します。 このタブは、パブリケーションの新規作成ウィザードの **[アーティクル]** ページおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスから利用できます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[Oracle データベースからのパブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)」および「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
#### <a name="to-specify-a-data-type-mapping"></a>データ型マッピングを指定するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスでテーブルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[データのマッピング]** タブで、 **[サブスクライバーのデータ型]** 列からマッピングを選択します。  
  
    -   データ型によっては、可能なマッピングが 1 つしかない場合があります。このような場合、プロパティ グリッドの列は読み取り専用になります。  
  
    -   データ型によっては、複数のデータ型を選択できる場合があります。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、アプリケーションに別のマッピングが必要でない限り、既定のマッピングを使うことをお勧めします。 詳しくは、「 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)」をご覧ください。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 レプリケーションのストアド プロシージャを使用すると、カスタム データ型マッピングをプログラムから指定できます。 また、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータベース管理システム (DBMS) と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のデータベース管理システム間でデータ型をマップする場合に使用する既定のマッピングを設定することもできます。 詳しくは、「 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)」をご覧ください。  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Oracle パブリケーションのアーティクル作成時にカスタム データ型マッピングを定義するには  
  
1.  Oracle パブリケーションが存在しない場合は、Oracle パブリケーションを作成します。  
  
2.  ディストリビューターで [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 **\@use_default_datatypes** に **0** を指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
3.  ディストリビューターで [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) を実行して、パブリッシュ対象アーティクルに含まれる列の既存のマッピングを表示します。  
  
4.  ディストリビューターで [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)を実行します。 **\@publisher** に Oracle パブリッシャーの名前を指定し、 **\@publication**、 **\@article**、および **\@column** を指定して、パブリッシュする列を定義します。 マップする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型名を **\@type** に指定し、該当する **\@length**、 **\@precision**、および **\@scale** を指定します。  
  
5.  ディストリビューターで [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)を実行します。 これにより、Oracle パブリケーションからスナップショットを生成するときに使用するビューが作成されます。  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>データ型に対する既定のマッピングを指定するには  
  
1.  (省略可) ディストリビューターから任意のデータベースで [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)を実行します。 **\@source_dbms**、 **\@source_type**、 **\@destination_dbms**、 **\@destination_version** を指定します。また、マップ元 DBMS を識別するために必要なパラメーターが他にもあれば、それらを指定してください。 マップ先 DBMS で現在マップされているデータ型の情報は、出力パラメーターを使って返されます。  
  
2.  (省略可) ディストリビューター側の任意のデータベースに対して [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)を実行します。 **\@source_dbms** を指定し、さらに、結果セットをフィルター選択するために必要なパラメーターが他にもあれば、それらを指定します。 目的のマッピングの **mapping_id** を結果セットで確認してください。  
  
3.  ディストリビューターから任意のデータベースで [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)を実行します。  
  
    -   手順 2. で **mapping_id** の値を確認できた場合は、その値を **\@mapping_id** に指定します。  
  
    -   **mapping_id** がわからない場合は、 **\@source_dbms**、 **\@source_type**、 **\@destination_dbms**、 **\@destination_type** の各パラメーターを指定し、さらに、既存のマッピングを識別するために必要なパラメーターが他にもあれば、それらを指定します。  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>特定の Oracle データ型に対して有効なデータ型を見つけるには  
  
1.  ディストリビューターから任意のデータベースで [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)を実行します。 **\@source_dbms** に **ORACLE** を指定し、さらに、結果セットをフィルター選択するために必要なパラメーターが他にもあれば、それらを指定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、Oracle のデータ型 NUMBER の列を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータ型にマップします。既定では、 **numeric**データ型にマップされますが、ここでは、 **float**を使用して、Oracle パブリッシャーのデータ型マッピングを指定する方法について説明します。  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 次のクエリの例では、Oracle 9 データ型の **CHAR**について、既定のマッピングと代替マッピングを返します。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 次のクエリの例では、Oracle 9 データ型の **NUMBER** で、小数点以下桁数または有効桁数を指定しなかった場合に使用される既定のマッピングを返します。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## <a name="see-also"></a>参照  
 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [異種データベース レプリケーション](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Oracle パブリッシャーの構成](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  
