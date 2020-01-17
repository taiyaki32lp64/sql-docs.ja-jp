---
title: SQL Server 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdest.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 818f78cd0b38aba0a7201eb28f49eb573ba32672
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770713"
---
# <a name="sql-server-destination"></a>SQL Server 変換先
  SQL Server 変換先はローカルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続し、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはビューに一括で読み込みます。 SQL Server 変換先は、リモート サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにアクセスするパッケージでは使用できません。 代わりに、このパッケージでは OLE DB 変換先を使用する必要があります。 詳細については、「 [OLE DB 変換先](ole-db-destination.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 SQL Server 変換先が含まれたパッケージを実行するユーザーには、"グローバル オブジェクトの作成" 権限が許可されている必要があります。 **[管理ツール]** のローカル セキュリティ ポリシー ツールを使用することにより、この権限をユーザーに許可できます。 SQL Server 変換先を使用するパッケージの実行時にエラー メッセージが表示された場合は、パッケージを実行しているアカウントに "グローバル オブジェクトの作成" 権限が許可されていることを確認してください。  
  
## <a name="bulk-inserts"></a>一括挿入  
 SQL Server 変換先を使用してリモートの SQL Server データベースにデータを一括読み込みしようとすると、次のようなエラー メッセージが表示されることがあります。"OLE DB レコードを使用できます。 ソース:"Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 説明: "SSIS ファイル マッピング オブジェクト 'Global\DTSQLIMPORT' を開けなかったので、一括読み込みできませんでした。 オペレーティング システム エラー コード 2 (指定されたファイルが見つかりません)。 Windows セキュリティ経由でローカル サーバーにアクセスしていることを確認してください。""  
  
 SQL Server 変換先で行われるのは、一括挿入タスクで行われるものと同じ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への高速なデータ挿入です。ただし、パッケージで SQL Server 変換先を使用することによって、データが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込まれる前に変換を列データに適用できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にデータを読み込む場合は、OLE DB 変換先ではなく SQL Server 変換先を使用することをお勧めします。  
  
### <a name="bulk-insert-options"></a>一括挿入オプション  
 SQL Server 変換先で高速読み込みデータ アクセス モードを使用する場合、次の高速読み込みオプションを指定できます。  
  
-   インポートしたデータ ファイルの ID 値を保持します。または、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって割り当てられた一意の値を使用します。  
  
-   一括読み込み操作中に、NULL 値を保持します。  
  
-   一括インポート操作中に、インポート先のテーブルまたはビュー上の制約を確認します。  
  
-   一括読み込み操作中に、テーブルレベルのロックを取得します。  
  
-   一括読み込み操作中に、変換先のテーブル上で定義されている挿入トリガーを実行します。  
  
-   一括挿入操作中に読み込む、入力の最初の行番号を指定します。  
  
-   一括挿入操作中に読み込む、入力の最後の行番号を指定します。  
  
-   一括読み込み操作が取り消されるまでに許可されるエラーの最大数を指定します。 インポートできない各行は、エラーとしてカウントされます。  
  
-   並べ替えられたデータが含まれる入力内の列を指定します。  
  
 一括読み込みオプションの詳細については、「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」を参照してください。  
  
#### <a name="performance-improvements"></a>パフォーマンスの強化  
 一括挿入、および一括挿入操作中のテーブル データへのアクセスのパフォーマンスを向上するには、既定のオプションを次のように変更する必要があります。  
  
-   一括インポート操作中に、インポート先のテーブルまたはビュー上の制約を確認しません。  
  
-   一括読み込み操作中に、変換先のテーブル上で定義されている挿入トリガーを実行しません。  
  
-   ロックをテーブルに適用しません。 これにより、一括挿入操作中、他のユーザーおよびアプリケーションはテーブルを引き続き使用できます。  
  
## <a name="configuration-of-the-sql-server-destination"></a>SQL Server 変換先の構成  
 SQL Server 変換先は、次の方法で構成できます。  
  
-   データの一括読み込み先となるテーブルまたはビューを指定します。  
  
-   CHECK 制約を実行するかどうかなどのオプションを指定することにより、一括読み込み操作をカスタマイズします。  
  
-   同じバッチ内ですべての行をコミットするか、バッチとしてコミットする行の最大数を設定するかのいずれかを指定します。  
  
-   一括読み込み操作のタイムアウトを指定します。  
  
 この変換先は、OLE DB 接続マネージャーを使用してデータ ソースに接続します。OLE DB 接続マネージャーでは、使用する OLE DB プロバイダーを指定します。 詳細については、「 [OLE DB 接続マネージャー](../connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトでは、OLE DB 接続マネージャーを作成できるデータ ソース オブジェクトも用意されます。 これにより、SQL Server 変換先でデータ ソースとデータ ソース ビューが使用できるようになります。  
  
 SQL Server 変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[SQL 変換先エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[SQL 変換先エディター] &#40;[接続マネージャー] ページ&#41;](../sql-destination-editor-connection-manager-page.md)  
  
-   [[SQL 変換先エディター] &#40;[マッピング] ページ&#41;](../sql-destination-editor-mappings-page.md)  
  
-   [[SQL 変換先エディター] &#40;[詳細設定] ページ&#41;](../sql-destination-editor-advanced-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [SQL Server 変換先のカスタム プロパティ](sql-server-destination-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [SQL Server 変換先を使用してデータの一括読み込みを行う](sql-server-destination.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [SQL Server 変換先を使用してデータの一括読み込みを行う](sql-server-destination.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   support.microsoft.com の技術記事「 [UAC 対応システムで "データを挿入するための SSIS 一括挿入を準備できません" というエラーが発生することがある](https://go.microsoft.com/fwlink/?LinkId=199482)」  
  
-   msdn.microsoft.com の技術記事: [Integration Services のパフォーマンス チューニング技法](https://go.microsoft.com/fwlink/?LinkId=233700)  
  
-   simple-talk.com の技術資料「 [SQL Server Integration Services を使用してデータの一括読み込みを行う](https://go.microsoft.com/fwlink/?LinkId=233701)」  
  
## <a name="see-also"></a>参照  
 [データ フロー](data-flow.md)  
  
  
