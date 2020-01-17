---
title: 外部ツールの引数 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b1f1cff589dfe005011c025b6083821d259f6e9f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267060"
---
# <a name="arguments-for-external-tools"></a>外部ツールの引数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
引数とは、 **[ツール]** メニューから外部ツールを起動したときに、Studio 環境によって値が提供される変数です。 **[外部ツール]** ダイアログ ボックスを使用して、メモ帳などの外部ツールを **[ツール]** メニューに追加できます。  
  
外部ツールの引数は、次の表のとおりです。  
  
|[オブジェクト名]|引数|[説明]|  
|--------|------------|---------------|  
|**項目のパス**|$(ItemPath)|現在のソースの完全なファイル名 (ドライブ + パス + ファイル名として定義されます)。ソース以外のウィンドウがアクティブな場合は空白です。|  
|**項目のディレクトリ**|$(ItemDir)|現在のソースのディレクトリ (ドライブ + パスとして定義されます)。ソース以外のウィンドウがアクティブな場合は空白です。|  
|**項目のファイル名**|$(ItemFilename)|現在のソースのファイル名 (ファイル名として定義されます)。ソース以外のウィンドウがアクティブな場合は空白です。|  
|**項目の拡張子**|$(ItemExt)|現在のソースのファイル名の拡張子。|  
|**カレント行***|$(CurLine)|エディター内でカーソルが置かれている現在の行位置。|  
|**カレント列***|$(CurCol)|エディター内でカーソルが置かれている現在の列位置。|  
|**カレント テキスト***|$(CurText)|現在のテキスト (現在のカーソル位置にある単語、または選択中の単一行です)。|  
|**ターゲット パス**|$(TargetPath)|ターゲットの完全なファイル名 (ドライブ + パス + ファイル名として定義されます)。|  
|**ターゲット ディレクトリ**|$(TargetDir)|ターゲットのディレクトリ。|  
|**ターゲット名**|$(TargetName)|ターゲットのファイル名。|  
|**ターゲットの拡張子**|$(TargetExt)|ターゲットのファイル名の拡張子。|  
|**プロジェクト ディレクトリ**|$(ProjDir)|現在のプロジェクトのディレクトリ (ドライブ + パスとして定義されます)。|  
|**プロジェクト ファイル名**|$(ProjFileName)|現在のプロジェクトのファイル名 (ドライブ + パス + ファイル名として定義されます)。|  
|**ソリューション ディレクトリ**|$(SolutionDir)|現在のソリューションのディレクトリ (ドライブ + パスとして定義されます)。|  
|**ソリューション ファイル名**|$(SolutionFileName)|現在のソリューションのファイル名 (ドライブ + パス + ファイル名として定義されます)。|  
  
\* カレント行、カレント列、およびカレント テキストは、ステータス バーに表示されている、テキスト エディター内の現在のカーソル位置に基づきます。  
  
## <a name="see-also"></a>参照  
[[外部ツール] ダイアログ ボックス](../ssms/external-tools-dialog-box.md)  
[一般的なユーザー インターフェイス要素](../ssms/general-user-interface-elements.md)  
  
