---
title: Data Migration Assistant を使用した SQL Server のアップグレード
description: Data Migration Assistant を使用して、オンプレミスの SQL Server を新しいバージョンの SQL Server にアップグレードする方法、または Azure Vm に SQL Server する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: fc78354e3b422342e376bd7ebe75233dcd3ffaee
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056532"
---
# <a name="upgrade-sql-server-using-the-data-migration-assistant"></a>Data Migration Assistant を使用した SQL Server のアップグレード

Data Migration Assistant は、オンプレミスの SQL Server と、それ以降のバージョンの SQL Server へのアップグレード、または Azure Vm または Azure SQL Database での SQL Server への移行をシームレスに評価します。

この記事では、Data Migration Assistant を使用して、オンプレミスの SQL Server の SQL Server を以降のバージョンにアップグレードしたり、Azure Vm で SQL Server したりする手順について説明します。

## <a name="create-a-new-migration-project"></a>新しい移行プロジェクトを作成する

1. 左側のウィンドウで、 **[新規]** (+) を選択し、**移行**プロジェクトの種類を選択します。

2. オンプレミスの SQL Server をオンプレミスの SQL Server の新しいバージョンにアップグレードする場合は、ソースとターゲットのサーバーの種類を**SQL Server**に設定します。

3. **[作成]** を選択します。

   ![移行プロジェクトの作成](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>ソースとターゲットを指定する

1. ソース で、**ソースサーバーの詳細** セクションの **サーバー名** フィールドに SQL Server インスタンス名を入力します。 

2. ソース SQL Server インスタンスでサポートされている**認証の種類**を選択します。

3. ターゲットの場合は、 **[対象サーバーの詳細]** セクションの **[サーバー名]** フィールドに SQL Server インスタンス名を入力します。 

4. ターゲット SQL Server インスタンスでサポートされている**認証の種類**を選択します。

5. 接続は、 **[接続プロパティ]** セクションの **[暗号化接続]** を選択して暗号化することをお勧めします。

6. **[次へ]** をクリックします。

   ![[ソースとターゲットの指定] ページ](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>データベースの追加

1. **[データベースの追加]** ページの左ペインで、これらのデータベースを選択するだけで、移行する特定のデータベースを選択します。

   既定では、ソース SQL Server インスタンスのすべてのユーザーデータベースが移行対象として選択されます。

2. ページの右側にある [移行] 設定を使用して、次の手順に従って、データベースに適用される移行オプションを設定します。

   > [!NOTE]
   > 移行するすべてのデータベースに移行設定を適用するには、左側のウィンドウでサーバーを選択します。 左側のウィンドウでデータベースを選択して、特定の設定で個々のデータベースを構成することもできます。

    a. **バックアップ操作のためにソースとターゲットの SQL server がアクセスできる共有場所**を指定します。 ソース SQL Server インスタンスを実行しているサービスアカウントが、共有の場所に対する書き込み権限を持っていて、ターゲットサービスアカウントに共有場所に対する読み取り権限があることを確認します。

    b. 対象サーバー上のデータファイルとトランザクションログファイルを復元する場所を指定します。

    ![[データベースの追加] ページ](../dma/media/AddDatabases.png)

3. [**共有の場所] オプション**ボックスで、ソースとターゲットの SQL Server インスタンスがアクセスできる共有の場所を入力します。

4. ソースとターゲットの両方の SQL Server がアクセスできる共有の場所を指定できない場合は、 **[データベースのバックアップを、対象サーバーの読み取りと復元が可能な別の場所にコピーする]** を選択します。 次に、[**復元するバックアップの場所]** ボックスに値を入力します。 

   Data Migration Assistant を実行しているユーザーアカウントが、バックアップの場所に対する読み取り権限を持っていること、および対象サーバーの復元元の場所に対する書き込み権限を持っていることを確認してください。

   ![データベースのバックアップを別の場所にコピーするオプション](../dma/media/CopyDatabaseDifferentLocation.png)

5. **[次へ]** を選択します。

Data Migration Assistant は、バックアップフォルダー、データ、およびログファイルの場所に対して検証を実行します。 検証が失敗した場合は、オプションを修正し、 **[次へ]** を選択します。

## <a name="select-logins"></a>ログインの選択

1. 移行する特定のログインを選択します。

   > [!IMPORTANT]
   > 移行用に選択したデータベース内の1人以上のユーザーにマップされているログインを選択してください。   

   既定では、移行の対象となるすべての SQL Server および Windows ログインが、移行の対象として選択されます。

2. **[移行の開始]** を選択します。

   ![ログインを選択して移行を開始します](../dma/media/SelectLogins.png)

## <a name="view-results"></a>結果の表示

**[結果の表示]** ページで移行の進行状況を監視できます。

![[結果の表示] ページ](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>移行結果のエクスポート

1. **[結果の表示]** ページの下部にある **[レポートのエクスポート]** をクリックして、移行結果を CSV ファイルに保存します。

2. ログインの移行の詳細については、保存したファイルを確認してから、変更を確認してください。

## <a name="see-also"></a>参照

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: 構成設定](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: ベストプラクティス](../dma/dma-bestpractices.md)
