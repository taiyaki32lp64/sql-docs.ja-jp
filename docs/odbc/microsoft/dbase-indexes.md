---
title: dBASE インデックス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9a0a57c3dce920c6d5fbc2510932066cb5a2659
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096357"
---
# <a name="dbase-indexes"></a>dBASE インデックス
ODBC の dBASE ドライバーは自動的に開き、dBASE IV インデックス ファイルを更新します。 使用する必要があります、**インデックスの選択**dBASE III .ndx ファイルを関連付ける dBASE ファイルに ODBC データ ソース アドミニストレーターで表示されるダイアログ ボックス。  
  
 DBASE インデックスの作成に次の制限事項が適用されます。  
  
-   すべての列名は有効にする必要があります。  
  
-   すべての列は、同じ昇順または降順である必要があります。  
  
-   任意の 1 つのテキスト列の長さは 100 バイト未満である必要があります。  
  
-   1 つ以上の列が存在する場合は、テキスト列がありますすべての列と列のサイズの合計は 100 バイト未満である必要があります。  
  
-   メモ フィールドのインデックスを付けることはできません。  
  
-   現在のフィールドのセットのインデックスを指定しない必要があります (つまり、重複するインデックスは許可されません)。  
  
-   インデックス名は、dBASE インデックスの名前付け規則と一致する必要があります。 dBASE III は、各インデックスが別のファイルにそれぞれが .ndx 拡張機能であることが必要です。 DBASE IV の場合は、インデックスが 1 つの .mdx ファイルに格納されているタグの名前として作成されます。 .Mdx ファイルでは、同じ基本名をデータベース ファイルと (たとえば、Emp.mdx は Emp.dbf データベースのインデックス ファイル)。  
  
-   dBASE は、インデックスに同一のキー値を持つセットから 1 つのレコードを追加する、1 つとして一意のインデックスを定義します。
