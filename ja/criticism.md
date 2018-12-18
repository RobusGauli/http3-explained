# よくある疑問点

## UDP は多くの企業や組織で動くものではない

多くの企業、運用者、組織は、昨今においてほとんどが攻撃に悪用されるという理由のため、ポート53 (DNS に使われる) 以外の UDP トラフィックをブロックするか、あるいは利用制限をかけています。

特に、いくつかの既存 UDP プロトコルや UDP プロトコルを用いた一般的なサーバー上の実装はアンプ攻撃に対して脆弱であり続けていて、攻撃者は大量のトラフィックを無関係な第三者に送りつけることができます。

QUIC ではアンプ攻撃を軽減する方法が備わっています。サーバーから受け取る最初のパケットは最低でも1,200バイトを要求するとともに、クライアントからのレスポンスのパケットを受け取っていない場合では、応答としてサーバーは3つ以上のパケットを送ってはならない (MUST NOT)、とプロトコル上で明記されています。

## UDP はカーネル内で遅い

少なくとも2018年においては、 UDP がカーネル内で遅い点は正しいように思われます。

純粋に長年の間 UDP 転送のパフォーマンスは開発者の関心を集めてこなかったため、果たしてどの程度遅いのか、今後どのように発展していくのかは分かりません。

ほとんどのクライアントにとって、この「遅さ」が気になることはないはずです。

## QUIC は CPU 使用量が高すぎる

先述の「UDP は遅い」と同様ですが、これも TCP や TLS の世界的な普及がより成熟したり、ハードウェア支援ができるまでに必要な時間をかけているため、CPU 使用量が高すぎる点に関してもあまり当てはまりません。

もちろん、時間を経るごとに、こういった改善が見込めます。問題は利用者がどれだけ余剰な CPU 使用の増加を気にしなければならないかです。

## これは Google の規格でしょ？

いいえ、違います。 Google はインターネット規模で UDP を用いた QUIC 同様の規格が正しく動き、良いパフォーマンスであることを証明し、最初の仕様を IETF へ提案しました。

それ以来、多数の企業や組織から参加している個人が、ベンダーニュートラル な IETF でプロトコルの標準化に取り組んでいます。

もちろん Google の従業員は参加していますが、他にも Mozilla、Fastly、Cloudflare、Akamai、Microsoft、Facebook、Appleなど、インターネット上のトランスポートプロトコルの発展に興味を持つ多くの企業の従業員が参加しています。

## 改善にしては小さすぎる

それは批判ではなく、1つの意見です。おそらくその通りで、HTTP/2 が展開されてからの改善としては非常に小さいものかもしれません。

HTTP/3 はパケットロスの多いネットワーク上でより優れた性能を発揮し、より高速なハンドシェイクによって数字上でも体感でもレイテンシの改善が見込まれます。

しかしそれがサーバーやサービスへ HTTP/3 サポートを導入するほどのメリットであると言えるでしょうか？

時が経てば、そして将来のパフォーマンス測定結果が間違いなくそれを教えてくれるでしょう！