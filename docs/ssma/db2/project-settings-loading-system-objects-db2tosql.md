---
title: プロジェクトの設定 (システム オブジェクトの読み込み) (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5c12a2ddb97c6d599e5adfc57277e0a5f64288e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060188"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>プロジェクトの設定 (システム オブジェクトの読み込み) (DB2ToSQL)
[システム オブジェクトの読み込み] ページ、**プロジェクト設定** ダイアログ ボックスでは、SSMA に変換し、読み込む DB2 システム オブジェクトを指定できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
システム オブジェクトの読み込み ウィンドウが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   上のすべての SSMA プロジェクトの設定を指定する、**ツール**メニューの **プロジェクト設定の既定の**設定は表示またはから変更する必要な移行プロジェクトの種類を選択します **。移行ターゲット バージョン**をクリックしてドロップダウン**全般**クリックし、左側のウィンドウの下部にある**システム オブジェクトの読み込み**します。  
  
-   現在のプロジェクトの設定を指定する、**ツール**メニューの [**プロジェクトの設定**、] をクリックして**全般**左側のウィンドウの下部にあるをクリックして**システム オブジェクトの読み込み**します。  
  
## <a name="default-settings"></a>既定の設定  
システム オブジェクトの変換では、システム リソースが消費され、時間がかかります。 パフォーマンスを向上させるのには、SSMA は、次の一覧に示すように、最もよく使用されるシステムのオブジェクトのみを選択します。  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS です。標準  
  
-   SYS.UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
DB2 オブジェクトは、その他のシステム オブジェクトを参照してください、それらのオブジェクトを選択する必要があります。 DB2 データベース オブジェクトによって参照されているシステム オブジェクトを選択しない場合は、SSMA で変換エラーを報告します。 システム オブジェクトの不足によって発生する変換エラーが発生した場合は、このダイアログ ボックスで、不足しているオブジェクトを選択します。 必要に応じて変換をし繰り返すことができます。  
  
