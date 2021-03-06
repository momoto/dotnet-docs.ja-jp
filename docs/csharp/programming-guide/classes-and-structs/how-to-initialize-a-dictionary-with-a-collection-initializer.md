---
title: コレクション初期化子を使用してディクショナリを初期化する方法 - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 12/20/2018
helpviewer_keywords:
- collection initializers [C#], with Dictionary
ms.assetid: 25283922-f8ee-40dc-a639-fac30804ec71
ms.openlocfilehash: 22f80365b974df66999ac68f7bc2a9ffa7d445a5
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596810"
---
# <a name="how-to-initialize-a-dictionary-with-a-collection-initializer-c-programming-guide"></a>コレクション初期化子を使用してディクショナリを初期化する方法 (C# プログラミング ガイド)

<xref:System.Collections.Generic.Dictionary%602> にはキーと値のペアのコレクションが含まれています。 その <xref:System.Collections.Generic.Dictionary%602.Add*> メソッドは、それぞれキーと値に対する 2 つのパラメーターを受け取ります。 `Add` メソッドが複数のパラメーターを受け取る <xref:System.Collections.Generic.Dictionary%602> またはコレクションを初期化する 1 つの方法は、次の例に示すように、各パラメーターのセットを中かっこで囲むことです。 もう 1 つのオプションは、インデックス初期化子を使用することです。これも次の例に示されています。

## <a name="example"></a>例

次のコード例では、<xref:System.Collections.Generic.Dictionary%602> が型 `StudentName` のインスタンスで初期化されています。  最初の初期化では、`Add` メソッドを 2 つの引数と共に使用します。 コンパイラにより、`int` キーと `StudentName` 値の各ペアに対して、`Add` への呼び出しが生成されます。 2 回目の初期化では、`Dictionary` クラスのパブリック読み取り/書き込みインデクサー メソッドを使用します。

[!code-csharp[InitializerExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/HowToDictionaryInitializer.cs#HowToDictionaryInitializer)]  

最初の宣言のコレクションの各要素の中かっこの 2 つのペアに注目してください。 最も内側の中かっこは `StudentName` のオブジェクト初期化子を囲み、最も外側の中かっこは、`students` <xref:System.Collections.Generic.Dictionary%602> に追加されるキーと値のペアの初期化子を囲んでいます。 最後に、ディクショナリのコレクション初期化子全体が中かっこで囲まれています。 2 回目の初期化では、代入の左辺はキーで、右辺は `StudentName` のオブジェクトの初期化子を使用する値です。

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [オブジェクト初期化子とコレクション初期化子](./object-and-collection-initializers.md)
