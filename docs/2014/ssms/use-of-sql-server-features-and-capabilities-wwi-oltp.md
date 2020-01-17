---
title: 外部ツールの引数 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2365ec137329675e2cd88e7f5bf7e1781aa3308f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280492"
---
# <a name="arguments-for-external-tools"></a>外部ツールの引数
  引数とは、 **[ツール]** メニューから外部ツールを起動したときに、Studio 環境によって値が提供される変数です。 **[外部ツール]** ダイアログ ボックスを使用して、メモ帳などの外部ツールを **[ツール]** メニューに追加できます。  
  
 外部ツールの引数は、次の表のとおりです。  
  
|名前|引数|説明|  
|----------|--------------|-----------------|  
|**項目のパス**|$(ItemPath)|現在のソースの完全なファイル名 (ドライブ + パス + ファイル名として定義されます)。ソース以外のウィンドウがアクティブな場合は空白です。|  
|**項目のディレクトリ**|$(ItemDir)|現在のソースのディレクトリ (ドライブ + パスとして定義されます)。ソース以外のウィンドウがアクティブな場合は空白です。|  
|**項目のファイル名**|$(ItemFilename)|現在のソースのファイル名 (ファイル名として定義されます)。ソース以外のウィンドウがアクティブな場合は空白です。|  
|**項目の拡張子**|$(ItemExt)|現在のソースのファイル名の拡張子。|  
|**現在の行** <sup>1</sup>|$(CurLine)|エディター内でカーソルが置かれている現在の行位置。|  
|**現在の列**1|$(CurCol)|エディター内でカーソルが置かれている現在の列位置。|  
|**現在のテキスト**1|$(CurText)|現在のテキスト (現在のカーソル位置にある単語、または選択中の単一行です)。|  
|**ターゲット パス**|$(TargetPath)|ターゲットの完全なファイル名 (ドライブ + パス + ファイル名として定義されます)。|  
|**ターゲット ディレクトリ**|$(TargetDir)|ターゲットのディレクトリ。|  
|**ターゲット名**|$(TargetName)|ターゲットのファイル名。|  
|**ターゲットの拡張子**|$(TargetExt)|ターゲットのファイル名の拡張子。|  
|**プロジェクト ディレクトリ**|$(ProjDir)|現在のプロジェクトのディレクトリ (ドライブ + パスとして定義されます)。|  
|**プロジェクト ファイル名**|$(ProjFileName)|現在のプロジェクトのファイル名 (ドライブ + パス + ファイル名として定義されます)。|  
|**ソリューション ディレクトリ**|$(SolutionDir)|現在のソリューションのディレクトリ (ドライブ + パスとして定義されます)。|  
|**ソリューション ファイル名**|$(SolutionFileName)|現在のソリューションのファイル名 (ドライブ + パス + ファイル名として定義されます)。|  
  
 <sup>1</sup>ステータス バーで示すように、テキスト エディターでカーソルの位置に基づくが、現在の行、カレント列、または現在のテキスト。  
  
## <a name="see-also"></a>参照  
 [外部ツール ダイアログ ボックス](external-tools-dialog-box.md)   
 [一般的なユーザー インターフェイス要素](general-user-interface-elements.md)  
  
  
