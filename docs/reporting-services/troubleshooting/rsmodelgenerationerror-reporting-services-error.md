---
title: rsModelGenerationError - Reporting Services エラー | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 870f1fbc49e99e2cd43c6adb857137776c275550
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574087"
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Reporting Services エラー
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|rsRenderingError|  
|イベント ソース|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|コンポーネント|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|メッセージ テキスト|モデルの生成中にエラーが発生しました。 (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>説明  
 レポート モデルを生成できませんでした。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 以前のバージョンでは、このエラーは、System.Data.DataSet オブジェクトでデータベース スキーマ内のテーブルまたはリレーションシップを処理できない場合に表示される可能性があります。たとえば、1 つのテーブル内の同じ列に 2 つの外部キーが定義されている場合などです。  
  
## <a name="user-action"></a>ユーザーの操作  
 このメッセージが表示される原因となった具体的な理由を特定するには、\Microsoft SQL Server\\<SQL Server Instance\>\Reporting Services\LogFiles にあるレポート サーバーのログ ファイルを確認します。  
  
## <a name="internal-only"></a>内部使用のみ  
  
