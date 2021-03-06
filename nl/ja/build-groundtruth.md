---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

この文書は、{{site.data.keyword.cloud}} 上の {{site.data.keyword.knowledgestudiofull}} に関するものです。前のバージョンの {{site.data.keyword.IBM_notm}} マーケットプレイス上の {{site.data.keyword.knowledgestudioshort}} に関する文書を参照するには、[このリンクをクリックしてください ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/services/knowledge-studio/build-groundtruth.html){: new_window}。
{: tip}

# グランド・トゥルースの作成
{: #build-groundtruth}

アノテーション・プロジェクトの目標は、{{site.data.keyword.watson}} を特定分野に適応させるために使用される入念に吟味されたデータの集合であるグランド・トゥルースを得ることです。{{site.data.keyword.knowledgestudioshort}} でグランド・トゥルースの決定において主要な役割を果たすのはヒューマン・アノテーターであり、通常はターゲット分野の専門家がヒューマン・アノテーターになります。
{: shortdesc}

標準的なワークフローには以下のステップが含まれます。

1. ヒューマン・アノテーターは、アノテーションを付けた文書をレビューのためにサブミットします。
1. プロジェクト管理者 (対象分野の上級専門家である可能性あり) は、ヒューマン・アノテーターによる作業の正確さを検討し、複数のアノテーション・セットにある重複する文書に彼らがどの程度一貫性のあるアノテーションを付けたかを比較します。
1. アノテーター間一致スコアが低すぎる場合、プロジェクト管理者はアノテーション・セットを拒否し、改善のためにヒューマン・アノテーターに返します。アノテーション・セットが拒否されると、そのセット内のすべての文書が編集可能モードに戻ります。
1. プロジェクト管理者がアノテーション・セットを承認した場合、複数のアノテーション・セットで重複していない文書はグランド・トゥルースにプロモートされ、アノテーションがモデルのトレーニングに使用できるようになります。
1. プロジェクト管理者は、重複する文書を検討し、アノテーション競合を解決します。裁定と呼ばれるこの段階では、異なるヒューマン・アノテーターによるテキストのアノテーション付けが正しくなかったり一貫性がなかったりした原因となった解釈の違いを解消できるように、チームでアノテーション・ガイドラインを検討して改訂することがあります。

    場合によっては、プロジェクト管理者は、差異を裁定するための重複パーセンテージよりも高い重複パーセンテージを、アノテーター間一致を評価するために使用したいことがあります。例えば、プロジェクト管理者は、アノテーター間一致が良好だと思ったら、どちらのアノテーションをグランド・トゥルースにプロモートしてもよいと判断することがあります。

1. プロジェクト管理者がアノテーション競合を解決すると、承認されたアノテーションがグランド・トゥルースにプロモートされます。

ヒューマン・アノテーションには常に主観的な判断が必要になることに留意してください。アノテーション・ガイドラインは、テキストのアノテーション付けを正しく一貫したものにするために多大な役割を果たすことが可能ですが、最良のガイドラインでさえ、個人の解釈にゆだねられています。グランド・トゥルースを得るために、ヒューマン・アノテーターが分野コンテンツを分析する際に最適な判断を行えるように、彼らの訓練と教育に時間をかけたほうがいい場合があります。

## アノテーター間一致
{: #wks_haiaa}

ヒューマン・アノテーターによって文書にアノテーションが付けられた後、どの文書をグランド・トゥルースにプロモートするのかを決定する必要があります。アノテーター間一致スコアを検討することから始めます。スコアの低い文書は、拒否されてヒューマン・アノテーターに改善のために返される候補となります。

アノテーター間一致スコアの計算では、アノテーション・セットの状況に関係なく、タスク内のすべてのアノテーション・セット内の重複する文書がすべて調べられます。アノテーション・セットの受け入れまたは拒否は、セットの状況が「サブミット済み (Submitted)」になってからでないと行えないため、すべてのアノテーション・セットがサブミットされるまではアノテーター間一致を評価しないようにしたり、完了したアノテーション・セットをサブミットしたヒューマン・アノテーターのみに限定して検討したりできます。

アノテーター間一致スコアは、メンション、関係、および照応チェーンのアノテーション付けがアノテーターによってどのくらい違うのかを示します。ヒューマン・アノテーターのペアを比較することによって、スコアを確認できます (例えば、人物 A によるメンションのアノテーションのすべてと、人物 B によるメンションのアノテーションのすべてを比較します)。特定の文書を比較することでもスコアを確認できます (例えば、ある文書での人物 A による関係アノテーションを、同じ文書での人物 B による関係アノテーションと比較します)。

調査が必要な領域を特定するのに役立つよう、アノテーター間一致しきい値に指定した値を下回るスコアは、赤で強調表示されます。アノテーション・プロジェクトの初期段階では、関係のスコアがメンションのスコアよりも悪いことがよくあります。これは、完全な関係のアノテーションは、その関係を定義するメンションがまず一致していることを必要とするためです。

**「すべて (All)」**列のスコアは、*フライス・カッパ・スコア* です。これは、タスク内のすべての重複文書において複数のヒューマン・アノテーターによって同じアノテーションがどの程度一貫して適用されたかを表します。値は 1 までの範囲で、負であることも可能であり、アノテーション・ガイドラインまたは特定のヒューマン・アノテーターの弱点を識別するのに役立ちます。以下のガイドライン (*Landis and Koch、1977)*) は、全体的なパフォーマンスを査定するための開始点となります。

<table cellpadding="4" cellspacing="0" summary="" id="wks_haiaa__table_p5s_dx1_f5" class="table" rules="rows" frame="void" border="0"><thead class="thead" align="left"><tr class="row"><th class="entry ncol thleft" align="left" valign="top" id="d12741e148">スコア</th>
<th class="entry ncol thleft" align="left" valign="top" id="d12741e150">一致レベル</th>
</tr>
</thead>
<tbody class="tbody"><tr class="row"><td class="entry ncol tdleft" align="left" valign="top" headers="d12741e148 "><p class="p wrapper">&lt; 0</p></td>
<td class="entry ncol tdleft" align="left" valign="top" headers="d12741e150 "><p class="p wrapper">不調</p></td>
</tr>
<tr class="row"><td class="entry ncol tdleft" align="left" valign="top" headers="d12741e148 "><p class="p wrapper">.01 - .20</p></td>
<td class="entry ncol tdleft" align="left" valign="top" headers="d12741e150 "><p class="p wrapper">低度</p></td>
</tr>
<tr class="row"><td class="entry ncol tdleft" align="left" valign="top" headers="d12741e148 "><p class="p wrapper">.21 - .40</p></td>
<td class="entry ncol tdleft" align="left" valign="top" headers="d12741e150 "><p class="p wrapper">可</p></td>
</tr>
<tr class="row"><td class="entry ncol tdleft" align="left" valign="top" headers="d12741e148 "><p class="p wrapper">.41 - .60</p></td>
<td class="entry ncol tdleft" align="left" valign="top" headers="d12741e150 "><p class="p wrapper">中度</p></td>
</tr>
<tr class="row"><td class="entry ncol tdleft" align="left" valign="top" headers="d12741e148 "><p class="p wrapper">.61 - .80</p></td>
<td class="entry ncol tdleft" align="left" valign="top" headers="d12741e150 "><p class="p wrapper">重度</p></td>
</tr>
<tr class="row"><td class="entry ncol tdleft" align="left" valign="top" headers="d12741e148 "><p class="p wrapper">.81 - 1.0</p></td>
<td class="entry ncol tdleft" align="left" valign="top" headers="d12741e150 "><p class="p wrapper">完璧</p></td>
</tr>
</tbody>
</table>

他の列のスコアは、*F1 尺度* です。これは、ヒューマン・アノテーターのペア間のアノテーション整合性のレベルを表します。値は 0 から 1 までの範囲であり、完璧な一致はスコア 1 で表されます。どのくらいのレベルの一致であれば受け入れ可能なのかを決める要因は、対象分野のデータおよびタイプ・システムによって異なります。例として、以下に F1 しきい値を示します。これらの値は、KLUE タイプ・システムに基づくプロジェクトで、それ以上になることをプロジェクト管理者が期待する値です。

- エンティティー・タイプを持つメンション: 0.85
- 関係: 0.8
- 照応チェーン: 0.9

スコアの解釈は、使用しているタイプ・システムの複雑さ、アノテーションが付けられたコンテンツの量と複雑さ、ヒューマン・アノテーターの経験の豊富さ、およびその他の要因によって異なります。例えば、アノテーション・タスクが、品詞のラベル付けに重点を置いている場合、品詞は明確に定義されているため、高スコアを期待できるかもしれません。しかし、人間による解釈が必要な、テキストを深く分析する必要があるタスクの場合は、あいまいさの原因を解消するステップを実行するまでは低いスコアになると考えられます。

一般に、多くのエンティティー・タイプおよび関係タイプを含むタイプ・システムは多様な解釈の余地があり、そのため、モデル開発の初期段階ではアノテーター間一致が低くなる可能性があります。スコアを見ると、例えば、どのエンティティー・タイプのスコアが低いのかが分かります。低いスコアは、アノテーション・ガイドラインの改善が必要であることを示しています。ヒューマン・アノテーターのペア間のスコアを見ることによって、特定のアノテーターが常に他のアノテーターより低いスコアを示しているかどうかを識別できます。このアノテーターは、ガイドラインの理解またはアノテーション・ツールの使用に問題を抱えている可能性があり、したがって、追加訓練の候補となります。

## アノテーター間一致スコアの検討
{: #wks_haaccuracy}

どの文書をグランド・トゥルースにプロモートするのかを決定するときには、アノテーター間一致スコアを検討する必要があります。スコアの低い文書は、拒否されてヒューマン・アノテーターに改善のために返される候補となります。

### この作業について

アノテーター間一致を調べるときには、複数のヒューマン・アノテーターによってアノテーションが付けられた文書を検査します。文書が複数のアノテーション・セットおよび複数のヒューマン・アノテーターで共有されていない場合は、計算するアノテーター間一致はありません。タスクにアノテーション・セットを追加するときに、比較したいセットに同じ重複文書が含まれていることを確認してください。アノテーション・セット内にある文書を表示するには、**「アセット & ツール (Assets & Tools)」** > **「文書 (Documents)」**ページを開き、**「アノテーション・セット (Annotation Sets)」**タブをクリックし、セットの名前をクリックします。

重複文書が見つからない状態になることがあります。例えば、アノテーション・セットの作成を 2 回に分けて行い、それらを同じタスクに追加した場合などに、この状態になる可能性があります。それらのアノテーション・セットは、ほぼ同時に作成されたものの、共通する文書は含まれていません。別の例として、重複する文書が含まれるアノテーション・セットを作成するが、それらのアノテーション・セットのすべてを単一のタスクに追加するのではなく、タスクごとに 1 つのアノテーション・セットを追加する場合、重複する文書は検出されず、アノテーター間一致を計算することはできません。

### 手順

ヒューマン・アノテーター間のアノテーション一致を査定するには、次のようにします。

1. {{site.data.keyword.knowledgestudioshort}} 管理者またはプロジェクト管理者としてログインし、ワークスペースを選択します。
1. **「アセット & ツール (Assets & Tools)」** > **「文書 (Documents)」** > **「タスク (Tasks)」**タブを選択し、評価したいタスクを開きます。
1. **「アノテーター間一致の計算 (Calculate Inter-Annotator Agreement)」**をクリックします。デフォルト・ビューには、ヒューマン・アノテーターのペアがメンションへのアノテーション付けでどのくらい一貫性があったのかを示す一致スコアが表示されます。先頭行は、アノテーターの各ペア間の全体的な一貫性を示し、その下の表は、アノテーターのペアがテキスト中の特定のメンションへのラベル付けでどの程度一貫性があったのかを示します。
1. ヒューマン・アノテーターのペアが関係および照応にどの程度一貫してアノテーションを付けたのかを調べるには、先頭メニューから**「関係 (Relation)」**または**「照応 (Coreference)」**を選択します。
1. ヒューマン・アノテーターのペアが特定の重複文書中のエンティティー、関係、または照応にどの程度一貫してアノテーションを付けたのかを調べるには、2 番目のメニューで**「文書 (Document)」**を選択し、評価したいアノテーターのペアを選択します。
1. スコアを検討した後、状況が「サブミット済み (Submitted)」のアノテーション・セットを承認するか拒否するかを決定できます。アノテーション・セットがサブミットされると、その名前の横にチェック・ボックスが表示されます。以下のアクションのいずれかを実行します。

    - アノテーター間一致スコアが受け入れ可能なアノテーション・セットに対して、チェック・ボックスを選択し、**「受け入れ (Accept)」**をクリックします。他のアノテーション・セットと重複していない文書はグランド・トゥルースにプロモートされます。重複する文書は、まず、競合を解決できるように裁定を通して検討される必要があります。
    - アノテーター間一致スコアが受け入れ可能ではないアノテーション・セットに対して、チェック・ボックスを選択し、**「拒否 (Reject)」**をクリックします。このアノテーション・セットは、ヒューマン・アノテーターによって、アノテーションの改善のために再処理される必要があります。

## 裁定
{: #wks_haperform}

複数のヒューマン・アノテーターが同じ文書で作業を行う場合、アノテーションをグランド・トゥルースにプロモートする前に、アノテーション間の不整合を解決したいことがよくあります。この競合解決プロセスは裁定と呼ばれます。

ヒューマン・アノテーターによってサブミットされたアノテーション・セットを承認すると、それらのアノテーション・セット間で重複していない文書はグランド・トゥルースにプロモートされます。重複文書をプロモートする前に、競合がないかアノテーションを調べる必要があります。一致しないインスタンスが見つかった場合、その競合の解決方法を決定する必要があります。そうするには、ヒューマン・アノテーターによって適用されたアノテーションの中から正しいものを選択するか、あるいは、まったく違うアノテーションを適用するように選択します。

文書を裁定の対象にできるのは、以下の条件の少なくとも 1 つが当てはまる場合です。

- プロジェクト管理者が 1 つのタスク内の複数のアノテーション・セットを同時に承認し、それらのアノテーション・セットのうちの 2 つ以上に同じ文書が存在する (重複文書)。
- プロジェクト管理者が、前に承認されたアノテーション・セット内の文書が裁定される前に別のアノテーション・セットを承認する。アノテーション・セット A とアノテーション・セット B で重複している文書を裁定し、アノテーションをグランド・トゥルースにプロモートし、その後で、同じ文書が含まれている別のアノテーション・セット C を承認すると、もう競合は存在しないため、新しく承認された文書内のアノテーションは自動的にグランド・トゥルースにプロモートされます。アノテーション・セット C 内のプロモートされたアノテーションは、アノテーション・セット A および B 内の重複文書が裁定されたときに確立されたグランド・トゥルースをオーバーライドすることに注意してください。アノテーション・セット A および B 内のアノテーションをプロモートする前に、アノテーション・セット C を承認する場合は、セット C 内の重複文書を調べて競合がないかチェックし、裁定することができます。

アノテーション・ガイドラインの改善に時間をかけると、裁定に費やす時間が次第に減少する可能性があります。例を用意し、混乱の原因となった領域をもっと明確にすることによって、ヒューマン・アノテーターが自分たちのミスから学ぶのを支援でき、将来の競合を防ぐことができます。

以下に、ヒューマン・アノテーター間での不一致が生じる例をいくつか示します。

- **メンション**

    - アノテーター 1 は、ある幅のテキストにメンションを配置しますが、アノテーター 2 はこれを行いません。
    - アノテーター 1 のインデックスが、アノテーター 2 のものよりも前または後ろで始まります (テキストの一部的な重なりまたは部分範囲がある)。
    - アノテーター 1 とアノテーター 2 が、異なるエンティティー・タイプを割り当てます。

- **関係**

    - アノテーター 1 は 2 つのメンション間に関係を作成しますが、アノテーター 2 はこれを行いません。
    - アノテーター 1 とアノテーター 2 は、同じメンション間に関係を作成しますが、異なる関係タイプで作成します。
    - アノテーター 1 とアノテーター 2 は、同じメンション間に関係を作成しますが、順序を逆にして作成します (1 番目のメンションと 2 番目のメンションの間の関係はタイプ・システムによって制約されるため、これはまれにしか起こりません)。

- **照応チェーン**

    - アノテーター 1 版の照応チェーンに包含 (または除外) されているメンションが、アノテーター 2 の照応チェーンでは除外 (または包含) されています。アノテーター 1 とアノテーター 2 の間でのエンティティーの調整は、スコアリングの問題になります。

## アノテーション競合の解決
{: #wks_haadjudicate}

裁定は、重複文書内のアノテーションをグランド・トゥルースにプロモートする前にアノテーション競合を検討することのできるステップです。ヒューマン・アノテーターのペアによって追加されたアノテーションを比較するか、ヒューマン・アノテーションを現行グランド・トゥルースと比較することができます。

### 始めに

[このリンク ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.youtube.com/watch?v=EbexfsuXxoQ&amp;feature=youtu.be){: new_window} をクリックして、文書を裁定する方法を説明する 3 分間のビデオをご覧ください。

### この作業について

ヒューマン・アノテーターは、アノテーション・タスクを完了した後、完了したアノテーション・セットをレビュー用にサブミットする必要があります。アノテーター間一致スコアを評価すると、アノテーターのペアが同じ文書にどのくらい異なるアノテーションの付け方をしたのかを知ることができます。アノテーター間一致スコアが受け入れ可能であれば、アノテーション・セットを承認します。タスク内の複数のアノテーション・セットで重複していない文書の場合、承認された文書中のアノテーションはグランド・トゥルースにプロモートされます。複数のアノテーション・セットで重複している文書の場合、アノテーションをグランド・トゥルースにプロモートする前に、文書を裁定し、アノテーション競合があればすべて解決する必要があります。

例として、文書を裁定しているときに、あるアノテーターがメンション `Barack Obama` をエンティティー・タイプ `PeoplePerson` を使用してアノテーション付けしたのが見つかったとします。また、別のアノテーターは、同じ文字列を 2 つのメンションとしてアノテーション付けし、エンティティー・タイプ `Person` を `Barack` に、エンティティー・タイプ `Person` を `Obama` に割り当てたとします。機械学習モデルのトレーニングが適切に行われることを確実にするため、このような不整合を解決する必要があります。

{{site.data.keyword.knowledgestudioshort}} でサポートされているのは、同時に 2 つのアノテーション・セット間で裁定を行うか、または、1 つのアノテーション・セットと現行グランド・トゥルースとの間で裁定を行うことです。3 つ以上のアノテーション・セットで重複している文書がある場合、最も信頼する (例えば、当該ヒューマン・アノテーターの信用性が高いなどの理由で) 2 つのアノテーション・セットを裁定して、その文書のグランド・トゥルースを決定します。その後、この最初の裁定の結果に基づいて、残りのアノテーション・セットを裁定します。

### 手順

重複文書を表示し、競合を解決するには、次のようにします。

1. {{site.data.keyword.knowledgestudioshort}} 管理者またはプロジェクト管理者としてログインし、ワークスペースを選択します。
1. **「アセット & ツール (Assets & Tools)」** > **「文書 (Documents)」** > **「タスク (Tasks)」**タブを選択し、評価したいタスクを開きます。
1. 少なくとも 2 つのアノテーション・セットが**「競合あり (In conflict)」**状況であることを確認します。
1. **「重複文書での競合のチェック (Check Overlapping Documents for Conflicts)」**をクリックします。競合がある文書がリストされます。
1. 重複文書内の競合を無視して、裁定を行わずにグランド・トゥルースにアノテーションをプロモートしたい場合、**「受け入れ (Accept)」**をクリックします。
1. 重複文書内の競合の解決を開始するには、**「競合のチェック (Check for Conflicts)」**をクリックします。
1. 裁定の候補が、ヒューマン・アノテーターによってアノテーションが付けられたアノテーション・セットおよび現行グランド・トゥルースを含めて 3 つ以上ある場合は、裁定の対象として 2 つの候補を選択し、**「競合のチェック (Check for Conflicts)」**をクリックします。候補が 2 つしかない場合、裁定ツールが自動的に開始されます。

    メンション、関係、および照応チェーンの競合がいくつ存在するのかが裁定ツールによって表示されます。メンションの競合を解決した後で、関係と照応チェーンの間の競合に進む必要があります。

1. 競合が含まれているセンテンスをクリックして強調表示します。未解決の競合に集中しやすくするため、**「解決済み (Resolved)」**チェック・ボックスをクリアして、**「未解決 (Unresolved)」**チェック・ボックスが選択されている状態にすることもできます。
1. 個々のアノテーションをクリックし、次に、**「受け入れ (Accept)」**または**「拒否 (Reject)」**をクリックします。直前の操作を取り消すには、`Ctrl+Z` を押します。

    一度に複数のアノテーションをクリックし、次に、受け入れるか拒否するかをクリックすることもできます。そうすると、選択したすべてのアノテーションにそれが適用されます。選択したアノテーションを選択解除したい場合は、センテンスの間の空白スペースをクリックするか、**Esc** キーを押すことによって、選択をクリアできます。

    以前にプロジェクトに接続されたアノテーション・ガイドラインがあり、適用する正しいアノテーションを選択できるよう支援が必要な場合は、**「ガイドラインの表示 (View Guidelines)」**をクリックします。ガイドラインがホストされているサイトでセットアップされたアクセス権によっては、ガイドラインを開いた後、説明や例を追加するといった更新を行うことができる場合があります。
    {: tip}

1. メンションに異なるエンティティー・タイプを適用するには、現行のアノテーションを拒否し、メンション (例えば `Barack Obama`) を選択し、正しいエンティティー・タイプ (例えば `Person`) を選択します。
1. センテンス中の他の競合について、受け入れ、拒否、および修正を続けます。センテンス内のすべての競合を解決した後、**「すべてのアノテーションを選択 (Select all annotations)」**リンクをクリックし、**「受け入れ (Accept)」**をクリックします。
1. 矢印アイコンをクリックして次のセンテンスに進みます。文書内のすべてのメンション競合が解決されるまで作業を続けます。

    処理中の作業を保存したり、現行の裁定セッションを一時的に中断したりするには、任意の時点で**「保存 (Save)」**をクリックします。行ったすべての変更を破棄するには、**「破棄 (Discard)」**をクリックします。前の裁定セッションが保存されていて、裁定を再開する準備ができた場合は、**「再開 (Resume)」**をクリックして、前に停止した場所から競合の裁定を開始します。前の裁定セッションを破棄した場合は、新しい裁定セッションを開始する必要があります。
    {: tip}

1. メンションの競合を解決した後、関係アノテーションおよび照応チェーン・アノテーションの間に生じる競合を解決するための裁定モードに切り替えます。

    - 関係の競合を解決するモードは、メンションの競合を解決する方法と似ています。センテンス単位で競合の解決を行います。
    - 照応チェーンは、複数のセンテンスにまたがって存在することが可能です。照応モードに進むと、右側のペインに、各ヒューマン・アノテーターによって作成された照応チェーンのリストが表示されます。裁定するチェーンを選択し、**「チェーンの拒否 (Reject Chain)」**または**「チェーンの受け入れ (Accept Chain)」**をクリックして、チェーン内のアノテーションを拒否するか受け入れます。あるいは、**「チェーンのマージ (Merge Chains)」**をクリックして、2 つのチェーンをマージします。照応チェーンからメンションを削除したい場合、文書領域でメンションの上にあるラベル内の削除アイコン (-) をクリックします。

1. 文書内のすべての競合が解決されたら、**「グランド・トゥルースへのプロモート (Promote to Ground Truth)」**をクリックします。
