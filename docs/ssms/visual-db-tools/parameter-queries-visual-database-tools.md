---
title: パラメーター クエリ (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- parameter queries [SQL Server]
ms.assetid: 4897c41a-324a-47b8-a30b-cbc9e9e19a8b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8c7f9d141edc20a981618b29776e8f9e7106bd19
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263251"
---
# <a name="parameter-queries-visual-database-tools"></a>パラメーター クエリ (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
値を変えるだけで、繰り返し利用できるクエリを作成することが必要になる場合があります。 たとえば、ある著者によって書かれたすべての `title_ids` を検索するクエリを頻繁に実行するような場合です。 著者の ID または名前を変更するだけで、要求のたびに同じクエリを実行できます。  
  
値を変更できるクエリを作成するには、クエリでパラメーターを使用します。 パラメーターとは、クエリの実行時に与えられる値のプレースホルダーです。 パラメーターを含む SQL ステートメントの例を次に示します。"?" は、著者の ID を表すパラメーターを示します。  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
## <a name="where-you-can-use-parameters"></a>パラメーターの使用例  
パラメーターは、リテラル値 (文字列または数値) のプレースホルダーとして使用できます。 最も一般的には、パラメーターは個別の行またはグループに対する検索条件のプレースホルダーとして、つまり SQL ステートメントの WHERE 句または HAVING 句内で使用されます。  
  
式の中でプレースホルダーとしてパラメーターを使用することもできます。 たとえば、クエリを実行するたびに異なる割引き値を指定して、割引き価格を計算できます。 この計算は、次の式で行います。  
  
```  
(price * ?)  
```  
  
## <a name="specifying-unnamed-and-named-parameters"></a>無名パラメーターと名前付きパラメーターの指定  
指定できるパラメーターは、無名パラメーターと名前付きパラメーターの 2 種類です。 無名パラメーターは疑問符 (?) です。リテラル値の入力を要求する、またはリテラル値を代入するクエリ内の任意の位置に挿入できます。 たとえば、無名パラメーターを使って `titleauthor` テーブルで著者の ID を検索する場合は、 [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) に次のようなステートメントが作成されます。  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
[クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)でこのクエリを実行すると、 [[クエリ パラメーター] ダイアログ ボックス](../../ssms/visual-db-tools/query-parameters-dialog-box-visual-database-tools.md) にパラメーター名として "?" が表示されます。  
  
パラメーターに名前を割り当てることもできます。 名前付きパラメーターは、クエリに複数のパラメーターがある場合に特に便利です。 たとえば、名前付きパラメーターを使って `authors` テーブルで著者の姓名を検索する場合は、SQL ペインに次のようなステートメントが作成されます。  
  
```  
SELECT au_id  
FROM authors  
WHERE au_fname = %first name% AND  
      au_lname = %last name%  
```  
  
> [!TIP]  
> 名前付きパラメーター クエリを作成する前に、プレフィックスとサフィックスを定義する必要があります。  
  
クエリおよびビュー デザイナーでこのクエリを実行すると、 [[クエリ パラメーター] ダイアログ ボックス](../../ssms/visual-db-tools/query-parameters-dialog-box-visual-database-tools.md) に名前付きパラメーターのリストが表示されます。  
  
## <a name="see-also"></a>参照  
[パラメーターを使用したクエリ (Visual Database Tools)](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[サポートされるクエリの種類 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
