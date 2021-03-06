---
title: ユーザー入力の検証 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24eef3e97f87d60db624605b19420e5fd562360b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213781"
---
# <a name="validating-user-input"></a>ユーザー入力の検証

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

データにアクセスするアプリケーションを作成する場合は、すべてのユーザー入力について、悪意がないと確認されるまでは、悪意があるものと見なす必要があります。 そうしないと、アプリケーションは攻撃に対して脆弱になる可能性があります。 発生する可能性がある攻撃の一種に、SQL インジェクションと呼ばれるものがあります。これは、後で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに渡され解析および実行が行われる文字列に、悪意のあるコードを挿入するというものです。 この攻撃を防ぐには、パラメータを持つストアド プロシージャを可能な限り使用し、ユーザー入力を常に検証する必要があります。

サーバーへの無駄なラウンド トリップを行わないようにするには、ユーザー入力の検証をクライアント コードで行うことが重要です。 同様に、ストアド プロシージャへのパラメータをサーバー上で検証し、有効でない入力や、クライアント側の検証をバイパスする入力を検出することも重要です。

SQL インジェクションと、この攻撃を避ける方法の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「SQL インジェクション」を参照してください。 ストアド プロシージャのパラメーターの検証の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「ストアド プロシージャ ([!INCLUDE[ssDE](../../includes/ssde_md.md)])」およびその下位のトピックを参照してください。

## <a name="see-also"></a>参照

[JDBC ドライバー アプリケーションのセキュリティ保護](../../connect/jdbc/securing-jdbc-driver-applications.md)
