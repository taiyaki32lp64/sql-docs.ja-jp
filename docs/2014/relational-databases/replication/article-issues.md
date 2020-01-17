---
title: '[アーティクルの問題点] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.articleissues.f1
ms.assetid: bde57da2-dd47-412f-9df7-9224968b2448
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9093ac313f0b72671e647461318793c21f476c75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032026"
---
# <a name="article-issues"></a>[アーティクルの問題点]
  **[アーティクルの問題点]** ページでは、見つかったアーティクルの条件と、その条件の結果として必要となるすべての変更が一覧表示されます。 次の表は、可能性のある問題点と、レプリケーションおよび既存のアプリケーションを適切に機能させるために必要となるアクションについて示しています。  
  
|アーティクルの問題点|詳細|必要なアクション|  
|-------------------|-------------|---------------------|  
|Uniqueidentifier 列がテーブルに追加される。|レプリケーションでは、サブスクリプションの更新を許可するマージ パブリケーションまたはトランザクション パブリケーションにおけるすべてのアーティクルに対して、 **uniqueidentifier** データ型の列が必要です。|レプリケーションでは、パブリッシュされたテーブルに **uniqueidentifier** データ型の列がない場合は、最初のスナップショットが生成されるときに、その列が自動的に追加されます。 これらのテーブルを参照する INSERT ステートメントと UPDATE ステートメントが、確実に列リストを使用する必要があります。 また、列の追加に十分な空き容量がディスク上にあることを確認する必要もあります。|  
|IDENTITY 列には NOT FOR REPLICATION オプションが必要。|レプリケーションでは、すべての IDENTITY 列が NOT FOR REPLICATION オプションを使用する必要があります。 パブリッシュされた IDENTITY 列がこのオプションを使用していない場合は、INSERT コマンドが正しくレプリケートしない可能性があります。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 以前を実行しているパブリッシャーで作成されたパブリケーションに適用されます。 すべての IDENTITY 列に対して NOT FOR REPLICATION プロパティを指定する必要があります。|  
|IDENTITY プロパティはサブスクライバーに転送されない。|このパブリケーションでは、サブスクライバーでの更新を許可しません。 IDENTITY 列がサブスクライバーに転送されるとき、IDENTITY プロパティは転送されません。 たとえば、パブリッシャーで INT IDENTITY として定義されている列は、サブスクライバーでは INT として定義されます。|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 以前を実行しているパブリッシャーで作成されたパブリケーションに適用されます。 必要なアクションはありません。|  
|ビューが参照するテーブルが必要。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パブリッシュされるビューとインデックス付きビューによって参照されるすべてのテーブルが、サブスクライバーで使用できる必要があります。 参照するテーブルがこのパブリケーション内のアーティクルとしてパブリッシュされていない場合は、これを手動でサブスクライバーに作成する必要があります。|**[戻る]** ボタンを使用して、 **[アーティクル]** ページへ移動します。 必要なオブジェクトをすべて追加します。|  
|ストアド プロシージャが参照するオブジェクトが必要。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パブリッシュされたストアド プロシージャによって参照される、テーブルやユーザー定義関数などすべてのオブジェクトが、サブスクライバーで使用できる必要があります。 参照するオブジェクトがこのパブリケーション内のアーティクルとしてパブリッシュされていない場合は、これを手動でサブスクライバーに作成する必要があります。|**[戻る]** ボタンを使用して、 **[アーティクル]** ページへ移動します。 必要なオブジェクトをすべて追加します。|  
  
## <a name="see-also"></a>関連項目  
 [データとデータベース オブジェクトのパブリッシュ](publish/publish-data-and-database-objects.md)   
 [パブリケーションの作成](publish/create-a-publication.md)  
  
  
