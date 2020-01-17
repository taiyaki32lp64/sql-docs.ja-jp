---
title: 外部データを仮想化する
description: このページでは、リレーショナル データ ソースに対して外部テーブルの作成ウィザードを使用する詳細な手順を説明します
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.metadata: seo-lt-2019
ms.openlocfilehash: f4bd7eec24be747fe6c0933d31467410bfecf2a9
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75227512"
---
# <a name="use-the-external-table-wizard-with-relational-data-sources"></a>リレーショナル データ ソースで外部テーブル ウィザードを使用する

SQL Server 2019 の主なシナリオの 1 つは、データを仮想化する機能です。 このプロセスにより、データを元の場所に置いたままにすることができます。 SQL Server インスタンスでデータを*仮想化*して、SQL Server 内の他のテーブルと同じようにクエリを行うことができます。 このプロセスにより、ETL プロセスの必要性が最小になります。 このプロセスは、PolyBase コネクタを使用することによって可能です。 データ仮想化の詳細については、「[PolyBase 入門](polybase-guide.md)」を参照してください。

このビデオでは、データの仮想化の概要を説明します。

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-Data-Virtualization/player?WT.mc_id=dataexposed-c9-niner]


## <a name="start-the-external-table-wizard"></a>外部テーブル ウィザードを起動する

[**azdata cluster endpoints list**](../../big-data-cluster/deployment-guidance.md#endpoints) コマンドを使用して取得した **sql-server-master** エンドポイントの IP アドレスまたはポート番号を使用して、マスター インスタンスに接続できます。 オブジェクト エクスプローラーで **[データベース]** ノードを展開します。 次に、既存の SQL Server インスタンスからデータを仮想化するデータベースのいずれかを選択します。 データベースを右クリックして **[外部テーブルを作成する]** を選択し、データ仮想化ウィザードを起動します。 データ仮想化ウィザードは、コマンド パレットから起動することもできます。 Windows では Ctrl + Shift + P キー、Mac では Cmd + Shift + P キーを使用します。

![データ仮想化ウィザード](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>データ ソースを選択する

いずれかのデータベースからウィザードを起動した場合、出力先のドロップダウン ボックスは自動的に入力されます。 また、このページでは出力先データベースを入力または変更するためのオプションもあります。 ウィザードでサポートされている外部データ ソースの種類は、SQL Server と Oracle です。

> [!NOTE]
>SQL Server が既定で強調表示されます。


![データ ソースを選択する](media/data-virtualization/select-data-source.png)

**[次へ]** をクリックして続行します。

## <a name="create-a-database-master-key"></a>データベースのマスター キーを作成する

このステップでは、データベースのマスター キーを作成します。 マスター キーの作成は必須です。 マスター キーにより、外部データ ソースによって使用される資格情報がセキュリティ保護されます。 マスター キーには強力なパスワードを選択してください。 また、**BACKUP MASTER KEY** を使用して、マスター キーをバックアップします。 バックアップを安全な場所に保存します。

![データベースのマスター キーを作成する](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> データベースのマスター キーを既にお持ちの場合は、この手順は自動的に省略されます。

## <a name="enter-external-data-source-credentials"></a>外部データ ソースの資格情報を入力する

このステップでは、外部データ ソースのオブジェクトを作成するための外部データ ソースと資格情報の詳細を入力します。 資格情報は、データ ソースに接続するためにデータベース オブジェクトによって使用されます。 外部データ ソースの名前を入力します。 例では Test になっています。 外部データ ソースの SQL Server 接続の詳細を提供します。 外部データ ソースを作成する**サーバー名**と**データベース名**を入力します。

次のステップで資格情報を構成します。 資格情報の名前を入力します。 この名前は、作成する外部データ ソースのサインイン情報を安全に格納するために使用されるデータベース スコープ資格情報です。 例では TestCred になっています。 ユーザー名とパスワードを入力して、データ ソースに接続します。

![外部データ ソースの資格情報](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>外部データ テーブルのマッピング

次のページで、外部ビューを作成するテーブルを選択します。 親データベースを選択すると、子テーブルも含まれます。 テーブルを選択すると、右側にマッピング テーブルが表示されます。 ここで、型を変更することができます。 また、選択した外部テーブル自体の名前を変更することもできます。

![外部データ ソースの資格情報](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>マッピング ビューを変更するには、別の選択したテーブルをダブルクリックします。

> [!IMPORTANT]
>外部テーブル ツールでは、写真型はサポートされていません。 写真型を持つ外部ビューを作成すると、テーブルの作成後にエラーが表示されます。 ただし、テーブルは作成されます。

## <a name="summary"></a>まとめ

このステップでは、選択内容の概要が表示されます。 データベース スコープの資格情報の名前と、出力先データベースに作成される外部データ ソース オブジェクトが提供されます。 **[スクリプトの生成]** を選択して、外部データ ソースを作成するために使用される構文を T-SQL でスクリプト化します。 **[作成]** を選択して、外部データ ソース オブジェクトを作成します。

![概要画面](media/data-virtualization/virtualize-data-summary.png)

**[作成]** を選択すると、出力先データベースに作成された外部データ ソース オブジェクトを確認できます。

![外部データ ソース](media/data-virtualization/external-data-sources.png)

**[スクリプトの生成]** を選択すると、外部データ ソース オブジェクトを作成するために生成される T-SQL クエリを確認できます。

![スクリプトの生成](media/data-virtualization/generated-script.png)

> [!NOTE]
> **[スクリプトの生成]** は、ウィザードの最後のページにのみ表示されるべきです。 現在は、すべてのページに表示されます。

## <a name="next-steps"></a>次のステップ

SQL Server のビッグ データ クラスターおよび関連するシナリオについて詳しくは、「[SQL Server ビッグ データ クラスターとは](../../big-data-cluster/big-data-cluster-overview.md)」をご覧ください。
