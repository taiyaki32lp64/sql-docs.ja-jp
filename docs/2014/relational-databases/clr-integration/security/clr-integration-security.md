---
title: CLR 統合のセキュリティ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 12ca3fcb00122313c1d1e4aae8b64733be9140c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918996"
---
# <a name="clr-integration-security"></a>CLR 統合のセキュリティ
  セキュリティ モデル、[!INCLUDE[ssNoVersion](../../../includes/dnprdnshort-md.md)]共通言語ランタイム (CLR) を管理し、さまざまな種類内で実行されている CLR および CLR 以外のオブジェクトの間のアクセスをセキュリティで保護[!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)]ステートメントまたはサーバーで実行されている別の CLR オブジェクト。 オブジェクト間の呼び出しをリンクと呼びます。 このようなオブジェクトに対して実行されるセキュリティ チェックの種類は、関連するリンクの種類によって異なります。  
  
 CLR 統合のセキュリティ モデルは、次のことを目標にしています。  
  
-   既定では、実行されているマネージ ユーザー コードで[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の堅牢性を侵害する可能性のある操作の実行は、レベルの高い適切な権限によって保護されるようにする。  
  
-   マネージド ユーザー コードは、データベース内のユーザー データや他のユーザー コードに対して、未承認のアクセスを行わない。 ユーザー定義コードは、そのコードを呼び出したユーザー セッションのセキュリティ コンテキストで実行する。実行には、そのセキュリティ コンテキストにおける適切な特権を使用する。  
  
-   ユーザー コードからサーバー外部のリソースへのアクセスを禁止するための制御機能を備える。ユーザー コードの使用は、ローカル データのアクセスおよびコンピューティングに限定する。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プロセスで実行することによって、ユーザー定義コードがシステム リソースへの未承認のアクセス手段を獲得してはならない。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR のコード アクセス ベースのセキュリティ モデル。 このセクションでは、このようにセキュリティ モデルを組み合わせたアプローチによるメリットの一部を紹介します。  
  
 次の表は、このセクションのトピックを一覧表示します。  
  
 [CLR 統合のコード アクセス セキュリティ](clr-integration-code-access-security.md)  
 マネージド コードのコード アクセス セキュリティ (CAS) モデルについて説明します。  
  
 [ホスト保護属性と CLR 統合プログラミング](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 SAFE アセンブリと EXTERNAL_ACCESS アセンブリで許可されていないホスト保護属性 (HPA) の値に関する情報を提供します。  
  
 [CLR 統合のセキュリティのリンク](../../../database-engine/dev-guide/links-in-clr-integration-security.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内のユーザー コードが相互に呼び出すしくみを説明します。  
  
 [権限借用と CLR 統合のセキュリティ](../../../database-engine/dev-guide/impersonation-and-clr-integration-security.md)  
 権限借用を使用してマネージド コードが外部リソースにアクセスするしくみを説明します。  
  
 [部分的に信頼される呼び出し元の許容](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
 マネージド メソッドが別のアセンブリに含まれるクラスのメソッドを起動する際に生じる問題について説明します。  
  
 [アプリケーション ドメインと CLR 統合のセキュリティ](../../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)  
 アセンブリがアプリケーション ドメインに読み込まれるしくみを説明します。  
  
## <a name="see-also"></a>参照  
 [CLR 統合アセンブリの管理](../assemblies/managing-clr-integration-assemblies.md)  
  
  
