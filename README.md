# One_Point_Decorder_from_General_Curve

20200921

しばらくパソコンのトラブルで集中できなかったけど、さぼっていたせいで研究が遅れてしまった。
SIKEにしようかとも思っていたんですが、楕円曲線だけに拘っているようで飽きるので、SIKEに対抗する形で、
つまりペアリング写像を「符号で打倒」するために符号を使ったカギ交換に取り組もうかと思っている。（大きな野望ｗ）

SIKEだったらマイクロソフトがバックについていて既に実装を公開しているから、
私があえて自分なりの実装を公開する意義は、勉強になるからという動機でしかない。

でもCAKEの場合、この目標は代数曲線の理論から符号理論を通って暗号理論に至る広範囲の知識を必要とする分野で、難しい分、魅力がある。
実は公開鍵暗号に幾何学的Goppa符号が使えるかどうかはいまだに意見が分かれていて、ペリカンなんかは５回も書き直して否定しているけど
他の研究者からはオリジナルのモレノ―ジャンワ構成は解かれていないなど反論も出ていて研究が進行中だ。

で、リスト復号はよく知らないのでとっつきにくい感じだけど、どちらにしてもグレブナー基底が出てきてしまうので躊躇するところではある。

一つはBM法を一般化した復号法。
もう一つはリスト復号。
BMはこんなの読んでもわからないよね、という書き方がされているので却下。（馬鹿に厳しい）

しかも手持ちの復号法は知りうる限り、リスト復号と関係していてLeeの絡んでいる方法は全部グレブナー基底が出てくる。
グレブナーが出てこないのはフェンラオだけで、BMだろうとリストだろうと出てくることには変わりがない。
つまりAG符号がやりたければ、どちらにしてもグレブナー基底をやらなければならないのだ。
どっちも好きじゃないんだけど、どっちでもないという方法は今のところないらしい。（工業数学らしく、わかりやすい方がいい）

BMとリストの違いは、エラーを特定する情報としてシンドロームを使うか、補間多項式を使うかの違いだ。
どちらも同じくらいの性能と処理能力がある。
BMがシンドローム復号という昔からある方法で一番よく知られているとすると、リストは１９９９年にMITのSudanが見つけるまで知られていなかった。

つまりシンドロームを使わないということは、今まで私が実装した方法の知識を全部投げ捨てることになる。
そしてリスト復号のために知識をリセットすることだ。
でも、一つの計算方法で多点生成AG符号が訂正できるとしたらどうすべきだろう。

ここでグレブナーを諦めてSIKEにするという迷いが出てくる。
同じだけの手間をかけるなら、SIKEを覚えるほうが楽かもしれない。
この迷いは、誤り訂正符号を復号するという問題に対して２つの異なる手段を覚えるという２度手間な努力を必要とするか、
あるいは既存のコードがあることを前提にSIKEという新しい知識を覚えるかを決めることだ。
前者の場合、２つの方法を理解することで何か新しい発見が出てくる可能性もある。

リスト復号に関してはMcElieceの丁寧な解説があるので、それを読めばいいだけだけど、まだどちらが楽かはわからない。
多分これMcElieceの解説読むのがどう見ても最短。

となると幾何学的Goppa符号を復号する前に、普通のRSのリスト復号を攻略する必要が出てくる。（２点生成RS符号なんかもある）
そしてリスト復号を公開している人はあまりいないようだ。

やらなきゃいけないことがはっきりしているSIKEのほうがCAKEより楽だと思うのだが、符号の伝道者である私が、符号より楕円曲線を優先するというのも変な気がする。
楕円曲線だったらサイボウズラボに詳しい人がいると思う。
２つの方式は読むまでもなく全然違うけど、コードの希少性から言ってリスト復号のほうが面白いかも。（Cの実装がない）
とりあえず今の目標は一般の代数曲線から作った一点生成幾何学的ゴッパ符号の復号だ。（楽なほうで）


20200806

リストでもシンドロームでもない補間多項式を使って、任意の幾何学的ゴッパ符号を復号する方法を実装する予定。
今の所暗号で手一杯なので、もう少し時間がかかりそう。
普通のフェンラオではたった1種類の曲線のある決められた符号の構成法の場合だけしか復号できなかったけど、この方法は遂にいろいろな曲線や多点生成符号まで1つのアルゴリズムで復号できるということだ。
まだ詳しくは読んでないけど、フルトンのalgebraic curveを読めば代数曲線の知識は得られると思うので、このまま論文を読み進めて途中でつまずいたら、それを先に勉強しようと思う。

http://www.math.lsa.umich.edu/~wfulton/CurveBook.pdf

20200731

Feng-Rao decoderからスピンアウト。
暗号作る合間に暇があったら、一般の曲線を使った幾何学的ゴッパ符号の復号をやる予定。
何時もの通り理論を無視して計算方法だけ学習するつもりｗ。
今をときめくMcElieceさんの、リスト復号のテキストをネットで入手。
1つの計算方法に60ページ以上の分量を割ける本はまずないから、私は随分ネット上のテキストや論文に助けられていることになる。
まだまだわからないことは沢山あるけど、1つずつ明らかにしていきたい。
面白いのは、二変数多項式で符号語を保管するということ。
補間法自体は大学の数値計算で出てくるけど、あんな古い知識に最近の研究が本に載っていることはまずない。
でもネットのテキストくらい丁寧に書かれてあれば私でも理解できるだろうと期待している。（外れるかも知れないがｗ）

これをやる上で一番肝心なのは、グレブナー基底を理解できるかどうかで、それとペアリング写像を理解するのとどちらが難しいかという天秤にかけなければならないこと。


