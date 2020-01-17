---
title: プロジェクトの設定 (システム オブジェクトの読み込み) (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: a5e8feb6c083c787d877cbc5491c533b8a35d740
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266606"
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>プロジェクトの設定 (システム オブジェクトの読み込み) (OracleToSQL)
[システム オブジェクトの読み込み] ページ、**プロジェクト設定** ダイアログ ボックスでは、SSMA に変換し、読み込む Oracle システム オブジェクトを指定できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
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
  
Oracle のオブジェクトは、その他のシステム オブジェクトを参照して、それらのオブジェクトを選択する必要があります。 Oracle データベース オブジェクトによって参照されているシステム オブジェクトを選択しない場合は、SSMA で変換エラーを報告します。 システム オブジェクトの不足によって発生する変換エラーが発生した場合は、このダイアログ ボックスで、不足しているオブジェクトを選択します。 必要に応じて変換をし繰り返すことができます。  
  
