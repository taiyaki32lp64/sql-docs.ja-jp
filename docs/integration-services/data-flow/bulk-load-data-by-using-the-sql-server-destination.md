---
title: SQL Server 変換先を使用してデータの一括読み込みを行う | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: 8f982f85-a82e-4e2d-9cd8-cd2f85402d8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bf8e8c7bafb72b90edfe108c5702ad330bc3e700
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293465"
---
# <a name="bulk-load-data-by-using-the-sql-server-destination"></a>SQL Server 変換先を使用してデータの一括読み込みを行う

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つのデータ ソースがあらかじめ含まれている必要があります。  
  
### <a name="to-load-data-using-a-sql-server-destination"></a>SQL Server 変換先を使用してデータの一括読み込みを行うには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先をデザイン画面にドラッグします。  
  
4.  変換先を、データ フロー内の変換元または直前の変換に連結します。連結するには、コネクタを変換先にドラッグします。  
  
5.  変換先をダブルクリックします。  
  
6.  **[SQL Server 変換先エディター]** の **[接続マネージャー]** ページで、既存の OLE DB 接続マネージャーを選択するか、または **[新規作成]** をクリックして新しい接続マネージャーを作成します。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
7.  データの読み込み先となるテーブルまたはビューを指定するには、次のいずれかの操作を行います。  
  
    -   既存のテーブルまたはビューを選択します。  
  
    -   **[新規作成]** をクリックし、 **[テーブルの作成]** ダイアログ ボックスで、テーブルまたはビューを作成する SQL ステートメントを記述します。  
  
        > [!NOTE]  
        >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
8.  **[マッピング]** をクリックし、 **[使用できる入力列]** 一覧にある列を、 **[使用できる変換先列]** 一覧の列にドラッグして、列をマップします。  
  
    > [!NOTE]  
    >  この変換先では、同じ名前の列は自動的にマップされます。  
  
9. **[詳細設定]** をクリックし、一括読み込みオプションの **[ID を保持する]** 、 **[NULL を保持する]** 、 **[テーブル ロック]** 、 **[CHECK 制約]** 、 **[トリガーを起動する]** を設定します。  
  
     必要に応じて、挿入する最初の入力行と最後の入力行、挿入操作が停止するまでに発生できるエラーの最大数、および挿入を並べ替える列を指定します。  
  
    > [!NOTE]  
    >  挿入の並べ替え順序は、列の一覧の表示順によって決定されます。  
  
10. **[OK]** をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md)   
 [Integration Services の変換](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../integration-services/data-flow/integration-services-paths.md)   
 [[データ フロー タスク]](../../integration-services/control-flow/data-flow-task.md)  
  
  
