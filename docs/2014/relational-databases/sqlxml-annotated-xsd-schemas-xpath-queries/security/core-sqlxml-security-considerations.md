---
title: SQLXML のセキュリティに関する考慮事項をコア |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- security [SQLXML], about security
ms.assetid: 330cd2ff-d5d5-4c8e-8f93-0869c977be94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc25af8e18e826ce6b8323d714f090ac3d571a97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010552"
---
# <a name="core-sqlxml-security-considerations"></a>SQLXML のセキュリティに関する主な注意点
  次に、データ アクセスに SQLXML を使用するときのセキュリティ ガイドラインを示します。  
  
-   SQLXMLOLEDB プロバイダーでは、`StreamFlags` プロパティへのアクセスが提供されます。このプロパティでは、特定の各インスタンスに対して有効または無効にする SQLXML 機能を示すフラグを設定できます。 このプロパティを使用して、必要なコンポーネントだけが有効になるよう、SQLXML の使用をカスタマイズすることをお勧めします。 詳細については、次を参照してください。 [SQLXMLOLEDB プロバイダー &#40;SQLXML 4.0&#41;](../../../database-engine/dev-guide/sqlxmloledb-provider-sqlxml-4-0.md)します。  
  
-   SQLXML エラーが発生した場合、返されるメッセージには、テーブル名、列名、種類の情報など、データベース スキーマに関する情報を含めることができます。 これらのエラーを扱うときには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストールに関する情報が関係のないユーザーに伝わらないよう注意する必要があります。  
  
-   SQLXML では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にクエリを実行したり更新を送信するにあたって、交換できるデータ量に制限は設定されません。また、処理前に SQLXML ペイロード内のデータのサイズに関してチェックは行われません。 SQLXML を使用してアプリケーションを開発する場合は、自身の責任で、システムにデータを処理する十分なメモリがあることを確認してください。 たとえば、サーバーに対してデータのクエリを実行するときには、クライアント側に、データを受信するだけの十分なメモリの空きがあることを確認する必要があります。 同様に、データをサーバーに読み込むときには、サーバー側に、データ処理に使用できるメモリと、データ保存に使用できるディスク保存領域が十分にあることを確認する必要があります。  
  
-   SQLXML では、動的に [!INCLUDE[tsql](../../../includes/tsql-md.md)] クエリと更新コマンドが生成され、実行のため [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。 これは、SQLXML がサーバーにクエリを実行して更新を適用する唯一の方法です。 結果は、(XML の) ストリームまたは行セットとして受信されます。  
  
-   SQLXML では、クエリ結果を受信しても、そのデータの内容に基づいて何らかの動作が行われるわけではありません。 データの種類や内容に基づいて追加処理は行われず、 操作を実行するためのコードとしてデータが使用されることはありません。  
  
-   XML テンプレートを実行すると、SQLXML では送信されたテンプレート内に含まれる XPath クエリと DBObject クエリが [!INCLUDE[tsql](../../../includes/tsql-md.md)] コマンドに変換され、そのコマンドが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に対して実行されます。 これらのコマンドは、既存のデータにのみ影響します。 SQLXML により生成されるコマンドでは、データベースの構造は変更されません。 データベースの構造を変更するには、ユーザーは明示的なコマンドを発行する必要があります。 たとえば、テンプレートの `sql:query` ブロックにコマンドを含めます。  
  
-   DBObject クエリと XPath ステートメントをマッピング ファイルに対して実行しても、SQLXML でデータベース内のデータは一切変更されません。  
  
-   SQLXML では、XML と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ モデルの違いに基づき、指定されたデータの形式が変更される場合があります。 たとえば、時間を指定する形式はこれら 2 つで異なるため、 SQLXML ではこの違いの解決が試みられます。 この結果、一部の精度情報が失われる場合があります。  
  
-   SQLXML では、データ処理は時間の制限なく、 エラーが発生するか処理が完了するまで続けられます。  
  
-   SQLXML ではファイル システムへの書き込みは行われません。 データベースから取得したデータを保存するには、ユーザーが自分でコードを作成する必要があります。  
  
-   SQLXML では、ユーザーはデータベースに対して任意の SQL クエリを実行できます。 この場合、ユーザーの設定なしで SQL データベースを公開することになるため、保護または制御されていないソースに対してこの機能は提供しないでください。  
  
-   アップデートグラムを実行すると、SQLXML では `updg:sync` ブロックが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに対する DELETE、UPDATE、および INSERT コマンドに変換されます。 これらのコマンドは、既存のデータにのみ影響します。 SQLXML により生成されるコマンドでは、データベースは変更されません。 データベースの構造を変更するには、ユーザーは明示的なコマンドを発行する必要があります。 たとえば、テンプレートの `sql:query` ブロックにコマンドを含めます。  
  
-   DiffGrams を実行すると、SQLXML では DiffGram が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに対する DELETE、UPDATE、および INSERT コマンドに変換されます。 これらのコマンドは、既存のデータにのみ影響します。 SQLXML により生成されるコマンドでは、データベースは変更されません。 データベースの構造を変更するには、ユーザーは明示的なコマンドを発行する必要があります。 たとえば、テンプレートの `sql:query` ブロックにコマンドを含めます。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0 のセキュリティに関する考慮事項](sqlxml-4-0-security-considerations.md)  
  
  
