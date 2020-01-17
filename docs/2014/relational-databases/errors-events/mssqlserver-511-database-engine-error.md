---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee53135fb492185d91287f553b7b1f0ddf3cc8ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867797"
---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|511|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|ROW_TOOBIG|  
|メッセージ テキスト|1 行のサイズ %d が許容最大値 %d を超えているので行を作成できません。|  
  
## <a name="explanation"></a>説明  
 実行しようとした操作が最大行サイズを超えました。 通常、最大行サイズは 8,060 バイトです。 ストレージ形式によっては、データに使用できる行サイズを縮小するオーバーヘッドが含まれる場合があります。 たとえば、スパース列を使用する場合、最大行サイズは 8,018 バイトです。 行を追加または削除する操作や列のデータ型を変更する操作では、データ ページ上の行を書き直すことが必要になる場合があります。その後、元の行は削除されます。 これらの操作では、行サイズの制限を最大値の半分にすると効果的です。 これは、短時間ですが、元の行と変更された行の両方をデータ ページ上に含める必要があるためです。  
  
> [!WARNING]  
>  Null 以外の **varchar(max)** または **nvarchar(max)** の各列には、24 バイトの追加の固定割り当てが必要で、これは並べ替え操作中の 8,060 バイトの行制限におけるカウント対象となります。 これにより、テーブル内に作成できる Null 以外の **varchar(max)** または **nvarchar(max)** の列数について、暗黙的な制限が生じます。 テーブルの作成時やデータ挿入時に、最大行サイズが許容最大値の 8060 バイトを超えるという通常の警告以外の、特別なエラーは提供されません。 この大きな行サイズが原因で、クラスター化インデックス キーの更新や列セット全体の並べ替えなどの通常操作の一部でエラー (エラー 512 など) が発生する可能性があります。これは操作を実行するまでユーザーは予測することができません。  
  
## <a name="user-action"></a>ユーザーの操作  
 できる限り、行のサイズを縮小します。  
  
 問題の原因が行の直接の更新であると考えられる場合は、複数の手順でテーブルを変更する必要があります。 新しいテーブルを作成し、新しいテーブルにデータを転送します。 その後、元のテーブルを削除して新しいテーブルの名前を変更するか、元のテーブルを切り捨て、元のテーブル内の行を変更し、そのテーブルにデータを戻します。  
  
  
