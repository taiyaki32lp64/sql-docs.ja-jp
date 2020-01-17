---
title: スクリプト生成ウィザードでサポートされるオブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9b1a48c19ad6e6b0e33d2b7f0d9ad326d866e00
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262284"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>スクリプト生成ウィザードでサポートされるオブジェクト
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  スクリプトの生成とパブリッシュ ウィザードは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]によってサポートされるオブジェクトのサブセットをサポートします。  
  
## <a name="supported-objects"></a>サポート対象のオブジェクト  
 次の表は、スクリプトの生成とパブリッシュ ウィザードでサポートされる、パブリッシュできるオブジェクトの一覧です。  
  
||||||  
|-|-|-|-|-|  
|アプリケーション ロール|データベース ロール|スキーマ|ユーザー定義集計|ビュー*|  
|アセンブリ|DEFAULT 制約|ストアド プロシージャ*|ユーザー定義データ型|XML スキーマ コレクション|  
|CHECK 制約|フルテキスト カタログ|シノニム|ユーザー定義関数||  
|CLR (共通言語ランタイム) ストアド プロシージャ*|インデックス|テーブル|ユーザー定義テーブル||  
|CLR ユーザー定義関数|Rule|ユーザー**|ユーザー定義型||  
  
 \* 暗号化されずにパブリッシュされます。  
  
 ** データベースに存在するシステム ユーザー以外のユーザーはすべてロールとしてパブリッシュされます。  
  
  
