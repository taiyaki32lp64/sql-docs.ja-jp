---
title: インデックスのディスク領域の例 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2beb1a7890786e31fb525b61963c235033882247
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63161797"
---
# <a name="index-disk-space-example"></a>インデックスのディスク領域の例
  インデックスを作成、再構築、または削除する場合は、古い (基になる) 構造と新しい (対象となる) 構造の両方を格納するディスク領域が、それぞれ適切なファイルとファイル グループで必要になります。 古い構造の割り当ては、インデックス作成トランザクションがコミットされるまで解除されません。 並べ替え操作用に一時ディスク領域が追加で必要になる場合もあります。 詳細については、「 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)」をご参照ください。  
  
 この例では、クラスター化インデックスを作成するために必要なディスク領域を判断します。  
  
 ここでは、クラスター化インデックスを作成する前の状態が、以下のとおりであるとします。  
  
-   既存のテーブル (ヒープ) には、100 万行が含まれている。 各行の長さは 200 バイトである。  
  
-   非クラスター化インデックス A には、100 万行が含まれている。 各行の長さは 50 バイトである。  
  
-   非クラスター化インデックス B には、100 万行が含まれている。 各行の長さは 80 バイトである。  
  
-   index create memory オプションは、2 MB に設定されている。  
  
-   既存のインデックスと新しいインデックスのすべてに、FILL FACTOR 値として 80 が使用される。 つまり、ページの使用率が 80% になります。  
  
    > [!NOTE]  
    >  クラスター化インデックスを作成した結果、行インジケーターを新しいクラスター化インデックス キーに置き換えるために、2 つの非クラスター化インデックスを再構築する必要があります。  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>オフライン インデックス操作に必要なディスク領域の計算  
 以下の手順では、インデックス操作中に使用する一時ディスク領域と、新しいインデックスを格納する永続的なディスク領域を計算します。 ここでの計算は概算です。結果は切り上げ、インデックスのリーフ レベルのサイズしか計算しません。 概算値には、チルダ (~) を付けています。  
  
1.  基になる構造のサイズを判断します。  
  
     ヒープ:100万 * 200 バイト ~ 200 MB  
  
     非クラスター化インデックス a:100万 * 50 バイト/80% ~ 63 MB  
  
     非クラスター化インデックス b:100万 * 80 バイト/80% ~ 100 MB  
  
     既存の構造の合計サイズ:363 MB  
  
2.  対象となるインデックス構造のサイズを判断します。 新しいクラスター化キーは、uniqueifier も含めて 24 バイトとします。 どちらの非クラスター化インデックスの行インジケーター (8 バイト長) も、このクラスター化キーに置き換えられます。  
  
     クラスター化インデックス:100万 * 200 バイト/80% ~ 250 MB  
  
     非クラスター化インデックス a:100万 * (50 - 8 + 24) バイト/80% ~ 83 MB  
  
     非クラスター化インデックス b:100万 * (80 ~ 8 + 24) バイト/80% ~ 120 MB  
  
     新しい構造体の合計サイズ:453 MB  
  
     基になる構造と対象の構造の両方をサポートするために、インデックス操作中に必要な合計のディスク領域は、816 MB (363 + 453) です。 現在基になる構造に割り当てられている領域は、インデックス操作がコミットされると、割り当てが解除されます  
  
3.  並べ替え用の追加の一時ディスク領域を判断します。  
  
     **tempdb** での並べ替え (SORT_IN_TEMPDB を ON に設定) と、対象の場所での並べ替え (SORT_IN_TEMPDB を OFF に設定) に必要な領域を示します。  
  
    1.  SORT_IN_TEMPDB が ON の場合、 **tempdb** には最大のインデックス (100 万行 * 200 バイト ～ 200 MB) を格納できるだけのディスク領域が必要です。 並べ替え操作では、FILL FACTOR については考慮されません。  
  
         追加のディスク領域 ( **tempdb** の場所内) は [index create memory サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) の値 (= 2 MB) と同じです。  
  
         SORT_IN_TEMPDB が ON の場合の一時ディスク領域の合計サイズは ~ 202 MB です。  
  
    2.  SORT_IN_TEMPDB が OFF (既定値) の場合、手順 2. で新しいインデックス用に算出した 250 MB のディスク領域が、並べ替えに使用されます。  
  
         追加のディスク領域 (対象の場所内) は [index create memory サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) の値 (= 2 MB) と同じです。  
  
         SORT_IN_TEMPDB が OFF の場合の一時ディスク領域の合計サイズは 2 MB です。  
  
 **tempdb**を使用すると、合計で 1,018 MB (816 + 202) がクラスター化インデックスと非クラスター化インデックスの作成用に必要になります。 **tempdb** を使用することで、インデックスの作成に使用する一時ディスク領域は増えますが、 **tempdb** がユーザー データベースとは異なるディスク セットにある場合、インデックスの作成に必要な時間を短縮できることがあります。 **tempdb**の使用の詳細については、「 [インデックスの SORT_IN_TEMPDB オプション](indexes.md)」を参照してください。  
  
 **tempdb**を使用しない場合は、合計で 818 MB (816 + 2) がクラスター化インデックスと非クラスター化インデックスの作成に必要になります。  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>オンライン クラスター化インデックス操作に必要なディスク領域の計算  
 クラスター化インデックスをオンラインで作成、削除、または再構築する場合、一時マッピング インデックスを構築および保持するために追加のディスク領域が必要になります。 一時マッピング インデックスには、テーブルの行ごとに 1 つのレコードが格納されます。レコードの内容は、古いブックマーク列と新しいブックマーク列を組み合わせたものです。  
  
 オンライン クラスター化インデックス操作に必要なディスク領域を計算するには、上記のオフライン インデックス操作用の手順を実行し、その結果と次の手順で得られる結果とを加算します。  
  
-   一時マッピング インデックスに必要な領域を判断します。  
  
     この例では、古いブックマークはヒープ (8 バイト) の行 ID (RID) と新しいブックマークはクラスター化キー (も含め、24 バイト、 `uniqueifier`)。 古いブックマークと新しいブックマーク間で重複する列はありません。  
  
     一時マッピング インデックスのサイズは、100 万行 * (8 バイト + 24 バイト) / 80% ~ 40 MB です。  
  
     SORT_IN_TEMPDB が OFF の場合は対象となる場所に必要なディスク領域に、SORT_IN_TEMPDB が ON の場合は **tempdb** に必要なディスク領域に、このディスク領域を加算する必要があります。  
  
 一時マッピング インデックスの詳細については、「 [インデックス DDL 操作に必要なディスク領域](disk-space-requirements-for-index-ddl-operations.md)」をご参照ください。  
  
## <a name="disk-space-summary"></a>ディスク領域のまとめ  
 次の表は、ディスク領域の計算結果をまとめたものです。  
  
|インデックス操作|構造の場所と必要なディスク領域|  
|---------------------|---------------------------------------------------------------------------|  
|SORT_IN_TEMPDB = ON に設定されたオフライン インデックス操作|操作中に領域の合計:1,018 MB。<br /><br /> -既存のテーブルとインデックス:363 MB\*<br /><br /> -<br />                    **tempdb**:202 MB *<br /><br /> -新しいインデックス:453 MB<br /><br /> 操作の完了後に必要な領域の合計:453 MB|  
|SORT_IN_TEMPDB = OFF に設定されたオフライン インデックス操作|操作中に領域の合計:816 MB。<br /><br /> -既存のテーブルとインデックス:363 MB *<br /><br /> -新しいインデックス:453 MB<br /><br /> 操作の完了後に必要な領域の合計:453 MB|  
|SORT_IN_TEMPDB = ON に設定されたオンライン インデックス操作|操作中に領域の合計:1058 MB。<br /><br /> -既存のテーブルとインデックス:363 MB\*<br /><br /> -**tempdb** (マッピング インデックスを含む)。242 MB *<br /><br /> -新しいインデックス:453 MB<br /><br /> 操作の完了後に必要な領域の合計:453 MB|  
|SORT_IN_TEMPDB = OFF に設定されたオンライン インデックス操作|操作中に領域の合計:856 MB。<br /><br /> -既存のテーブルとインデックス:363 MB *<br /><br /> -一時マッピング インデックス:40 MB\*<br /><br /> -新しいインデックス:453 MB<br /><br /> 操作の完了後に必要な領域の合計:453 MB|  
  
 *この領域は、インデックス操作がコミットされると、割り当てが解除されます。  
  
 この例では、同時実行ユーザーの更新操作や削除操作により作成されるバージョン レコード用に **tempdb** に必要な追加の一時ディスク領域については、計算していません。  
  
## <a name="related-content"></a>関連コンテンツ  
 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)  
  
 [インデックス操作用のトランザクション ログのディスク領域](transaction-log-disk-space-for-index-operations.md)  
  
  
