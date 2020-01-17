---
title: '[フルテキスト インデックス] ダイアログ ボックス (Visual Database Tools) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 926e3d42d21e24d9a3e76d10966e3d90381ca843
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68254615"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>[フルテキスト インデックス] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
このダイアログ ボックスを使用すると、データベース テーブルのテキスト ベースの列に対するフルテキスト検索用にフルテキスト インデックスを作成できます。 フルテキスト インデックスは、通常のインデックスに基づくため、最初に通常のインデックスを作成する必要があります。 通常のインデックスは、単一の非 null 列に作成する必要があります。大きな値を格納している列ではなく、小さな値を格納している列を選択するのが最も適切です。  
  
> [!NOTE]
> フルテキスト インデックスを作成する場合、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、Enterprise Manager などの外部ツールを使用して、あらかじめデータベースのフルテキスト カタログを作成しておく必要があります。  
> 
> [!NOTE]
> フルテキスト インデックスの機能は、 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで利用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2012 の各エディションがサポートする機能](https://msdn.microsoft.com/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)」を参照してください。  
  
## <a name="options"></a>オプション  
**[選択されたフルテキスト インデックス]**  
既存のフルテキスト インデックスを一覧表示します。 インデックスを選択すると、右のグリッドにそのインデックスのプロパティが表示されます。 一覧が空の場合、テーブルにフルテキスト インデックスは定義されていません。  
  
**[追加]**  
新しいフルテキスト インデックスを作成します。  
  
**削除**  
**[選択されたフルテキスト インデックス]** ボックスの一覧で選択したフルテキスト インデックスを削除します。  
  
**[全般] カテゴリ**  
展開して **[列]** および **[フルテキスト カタログ名]** を表示します。  
  
**[列]**  
フルテキスト検索ができる列の名前を、コンマ区切りの一覧として表示します。 完全な一覧を表示するには、プロパティ フィールドの左側にある省略記号ボタン ( **[...]** ) をクリックします。  
  
**Full-Text Catalog Name**  
フルテキスト インデックスが格納されているフルテキスト カタログの名前を表示します。 インデックスを別のカタログに格納するには、カタログ名をクリックし、ドロップダウン リストから別のカタログを選択します。  
  
> [!NOTE]  
> カタログは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Enterprise Manager などの外部ツールで、あらかじめ作成しておく必要があります。  
  
**[IDENTITY] カテゴリ**  
展開してインデックスの名前フィールドを表示します。  
  
**[名前]**  
システムが指定したフルテキスト インデックスの名前を表示します。  
  
**[テーブル デザイナー] カテゴリ**  
展開してインデックスの実行方法を指定するプロパティを表示します。  
  
**Active**  
該当するフルテキスト インデックスを使用して、フルテキスト検索を現在実行できるかどうかを示します。  
  
**[トラッキング設定の変更]**  
該当するインデックスの変更履歴の状態を示します([手動]、[自動]、または [オフ])。  
  
**[クロールの完了]**  
最近のクロールが完了したかどうかを示します。 このプロパティ値が [いいえ] の場合、クロールは現在進行中です。  
  
**[現在または最近のクロールの終了日時]**  
最近のクロールが終了した日時を表示します。  
  
**[現在または最近のクロール内のエラー]**  
現在のクロールまたは最近のクロールで発生したエラーの数を表示します。  
  
**[インデックス バージョン]**  
クロールが開始した時点での、テーブルのスキーマ バージョンを表示します。  
  
**[現在または最近のクロール内の行]**  
現在のクロールまたは最近のクロールで更新された行の数を表示します。  
  
**[現在または最近のクロールの開始日時]**  
現在のクロールまたは最近のクロールが開始した日時を表示します。  
  
**[次のクロールのタイムスタンプ]**  
次のクロールが開始する日時を表示します。  
  
**[現在または最近のクロールの種類]**  
現在のクロールまたは最近のクロールの種類を表示します(空き領域なし、インクリメンタル、更新、自動伝達)。  
  
**[一意のインデックス名]**  
一意の単一列インデックスを持つ、データベース内のすべての列の名前を一覧表示します。 これらの列は、フルテキスト インデックスの作成に使用できます。  
  
## <a name="see-also"></a>参照  
[フルテキスト インデックス作成ウィザードの使用](https://msdn.microsoft.com/3e9d9605-6525-4781-9168-fdaa06db3459)  
[CREATE FULLTEXT INDEX (Transact-SQL)](https://msdn.microsoft.com/8b80390f-5f8b-4e66-9bcc-cabd653c19fd)  
  
