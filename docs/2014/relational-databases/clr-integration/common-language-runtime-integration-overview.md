---
title: 共通言語ランタイム (CLR) 統合の概要 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7764c6e8e45b56e43e592e70b1c85b8d4744b69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919313"
---
# <a name="common-language-runtime-clr-integration-overview"></a>CLR (共通言語ランタイム) 統合の概要
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、.NET Framework for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows の CLR (共通言語ランタイム) コンポーネントが統合されました。 CLR では、言語間の統合、コード アクセス セキュリティ、オブジェクトの有効期間の管理、デバッグとプロファイルのサポートなどのサービスがマネージド コードに提供されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のユーザーやアプリケーション開発者にとっての CLR 統合とは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET や [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# などの .NET Framework 言語を使用して、ストアド プロシージャ、トリガー、ユーザー定義型、ユーザー定義関数 (スカラー関数とテーブル値関数)、ユーザー定義集計関数を記述できるようになることを意味します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、.NET Framework Version 4 が付属します。  
  
 次に、この統合の主な利点のいくつかを示します。  
  
-   **優れたプログラミング モデル。** .NET Framework 言語では、以前 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の開発者が使用できなかった構造や機能が提供されるので、多くの点で Transact-SQL よりも優れています。 また、開発者は .NET Framework ライブラリの機能も使用できます.NET Framework ライブラリには、プログラミングに関する問題を、迅速かつ効率的に解決する際に使用できる幅広いクラスのセットが用意されています。  
  
-   **強化された安全性とセキュリティ。** マネージ コードは、データベース エンジンによってホストされている共通言語ランタイム環境で実行されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではこれを利用して、旧バージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 拡張ストアド プロシージャに代わる、より安全で確実な機能を提供します。  
  
-   **データ型や集計関数を定義する機能。** ユーザー定義型とユーザー定義集計は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のストレージ機能とクエリ機能を拡張する新しい 2 つのマネージド データベース オブジェクトです。  
  
-   **標準化された環境による効率的な開発。** データベース開発は、今後リリースされる [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio .NET 開発環境に統合されます。 開発者は、データベース オブジェクトやスクリプトの開発およびデバッグを行う際に、中間層またはクライアント層の .NET Framework コンポーネントやサービスを作成する場合と同じツールを使用できます。  
  
-   **強化されたパフォーマンスとスケーラビリティの可能性があります。** .NET Framework 言語のコンパイル モデルと実行モデルは、多くの状況で、Transact-SQL を超える優れたパフォーマンスを提供します。  
  
 このセクションのトピックでは、次の内容について説明します。  
  
 [CLR 統合の概要](clr-integration-overview.md)  
 CLR 統合を使用してビルドできるオブジェクトの種類について説明します。また、CLR 統合を使用してデータベース オブジェクトをビルドする場合の要件を確認します。  
  
 [CLR 統合における新機能](clr-integration-what-s-new.md)  
 このリリースの新機能について説明します。  
  
 [CLR 統合のアーキテクチャ](../../database-engine/dev-guide/architecture-of-clr-integration.md)  
 CLR 統合の設計目標について説明します。  
  
 [CLR 統合の有効化](clr-integration-enabling.md)  
 CLR 統合を有効にする方法を説明します。  
  
## <a name="see-also"></a>関連項目  
 [.NET Framework のインストール](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [CLR 統合のパフォーマンス](clr-integration-architecture-performance.md)  
  
  
