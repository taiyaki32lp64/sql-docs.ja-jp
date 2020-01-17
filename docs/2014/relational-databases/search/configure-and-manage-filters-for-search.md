---
title: 検索用フィルターの構成と管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: df228060a5b714d92c9ae200d91851e4b579839d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011580"
---
# <a name="configure-and-manage-filters-for-search"></a>検索用フィルターの構成と管理
  `varbinary`、`varbinary(max)`、`image`、または `xml` データ型列のドキュメントにインデックスを作成するには、追加の処理が必要です。 この処理はフィルターによって実行します。 フィルターは、ドキュメントから (フォーマットを解除して) 文字情報を抽出します。 次に、テーブル列に関連付けられている言語のワード ブレーカー コンポーネントにテキストを送ります。  
  
 フィルターは、ドキュメント型 (.doc、.pdf、.xls、.xml など) に固有です。 これらのフィルターは IFilter インターフェイスを実装しています。 ドキュメント型の一覧を参照するには、 [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) カタログ ビューに対してクエリを実行してください。  
  
 バイナリ ドキュメントは、単一の `varbinary(max)` 列または `image` 列に格納できます。 各ドキュメントについて、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はファイル拡張子を基に正しいフィルターを選択します。 ファイルが `varbinary(max)` 列または `image` 列に格納されている場合にはファイル拡張子が表示されないため、ファイル拡張子 (.doc、.xls、.pdf など) を型列と呼ばれるテーブル内の別の列に格納する必要があります。 この型列は、任意の文字ベースのデータ型で、文書ファイルの拡張子 (たとえば [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Word 文書の場合は .doc) を格納します。 **ドキュメント**テーブルに[!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]、**ドキュメント**型の列は、 `varbinary(max)`、型の列と**FileExtension**の種類は`nvarchar(8)`します。  
  
> [!NOTE]  
>  フィルターは、実装によっては、親オブジェクトに埋め込まれたオブジェクトを処理できます。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、フィルターが他のオブジェクトへのリンクをたどるように構成されていません。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、独自の XML フィルターと HTML フィルターがインストールされます。 さらに、オペレーティング システムに既にインストールされている [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 専用形式 (.doc、.xdoc、.ppt など) のフィルターもすべて  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によって読み込まれます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに現在読み込まれているフィルターを確認するには、次のように [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) ストアド プロシージャを使用します。  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 ただし、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 形式以外のフィルターを使用するには、事前にこれらのフィルターをサーバー インスタンスに読み込む必要があります。 追加のフィルターのインストールの詳細については、「 [登録済みのフィルターおよびワード ブレーカーの表示または変更](view-or-change-registered-filters-and-word-breakers.md)」を参照してください。  
  
 **既存のフルテキスト インデックスの型列を表示するには**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
## <a name="see-also"></a>関連項目  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)   
 [FILESTREAM と SQL Server のその他の機能との互換性](../blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
