---
title: "GitHubプロフィール用のアスキーアートQuineを作った"
emoji: "🐟"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["ruby","quine","アスキーアート"]
published: true
---
# 作ったもの
```ruby:quine.rb
eval$s=%w(s=%(eval$s=%w(#{$s})*"");f=->n{s.slice!(0,n)};fish="#70@#23H
23#24@#18A34#18@#14R12#                       8A22#14@#11D12#11A25#11@
#9H12#12A28#9@#7R1                                  2#8A36#7@#5D13#6A4
1#5@#4H13#9A40            #4@#3R14                      #11A39#3@#2D14
#15A37#2@#2            H15#18A33#2                         @#R16#22A30
#@#D17#24            A27#@#H19#26                            A23#@#2R2
0#27A19            #2@#2D22                                    #27A17#
2@#3H             24#25A                                         15#3@
#4R2             9#20A13#4                                        @#5D
33#              14A13#5@#6H                                       57#
7@              #8A54#8@#11R48#                                     11
@#               13A44#13@#17D36#17                                 @#
                22A26#22@#70";output="                              
                 ";i=0;len=fish.size;i=0;                           
                   len.times{c=fish[i];if(c!=                       
'@                    '&&c!='#');j=i+1;len="";(fi                   sh
.s                      ize-j).times{|k|if(!(fish[j                 ]=
~/[                        0-9]/));break;end;len<<fi               sh[
j];j                             +=1;};count=len.to_i             ;pri
nt(32                                 .chr*count);i=             j;els
if(c==                                                         "@");pr
int("\n"                                                      );i+=1;e
lse;j=i+1;l                                                ="";(fish.s
ize-j).times{                                            |k|if(!(fish[
j]=~/[0-9]/));bre                                    ak;end;l<<fish[j]
;j+=1;};len=l.to_i;pri                          nt(f[len]);i=j;end;};p
uts();#This_program_is_a_Ruby_quine.___##arad166##Kento_Harada####)*""
```

![](/images/profile-quine/profile.png =300x)
*私のアイコン*

縦に伸びているように見えますが、[GitHub](https://github.com/arad166)では正しく表示されています。

# アスキーアートQuineとは

まずQuineとは、自身のソースコードと同じ文字列を出力するプログラムです。アスキーアートQuineとは、Quineをアスキーアートにしたものです。詳しくは以下の参考文献をご覧ください。

**参考文献**
遠藤 侑介, 『あなたの知らない超絶技巧プログラミングの世界』, 技術評論社, 2015年, [Amazon](https://www.amazon.co.jp/o/ASIN/4774176435/gihyojp-22)

自分のGitHubのプロフィールにこれがあったら格好良いと思い、作ってみました。言語はrubyです。

# 作成過程

まずはアイコンの画像をアスキーアートにしやすいように加工します。
パワーポイントで頑張りました。

![](/images/profile-quine/kakou.png)
*加工前/加工後*

最終的に正しい縦横比になるようにするため、この段階では少し横に伸ばしています^[一度正しい縦横比で画像を加工したら、アスキーアートの縦横比がおかしくなりました]。

これを[こちらのサイト](https://tool-taro.com/image_to_ascii/)でアスキーアートにします。

```
(mmmmmmmmmmmmmmmmmmmmmmmmmkkV7777????7777OXQmmmmmmmmmmmmmmmmmmmmmmmmm[
J@H@H@H@H@H@H@H@H@HMY"=`                      -?"WMH@H@H@H@H@H@H@H@H@]
JH@H@@@H@@@H@@H#"^                                  ?TM@H@@@H@@@H@@H@]
J@@H@HH@HH@HY=            ..kMMHa,                      ?WH@H@HH@H@@H]
J@H@H@@H@#"            .dHHHHHHHHF                         7MH@@H@H@H]
JH@H@HH#^            .MHHHHHHMW"^                            (HH@H@H@]
J@@H@M^            .HHHHMY"`         `                         ?M@H@@]
J@H@P             gHHHH|                `       `  `             4H@H]
JH@t             .HHHHHHN,                 `                      7H@]
J@t           `  dHHHHHHHHm,       `   `      `       `            OH]
JF      `  `    .HHH@HH@HHHHMa,                          `          W]
J!               OHHHHHHHHHHHHHHmJ.              `          `       ,]
J    `           .MHHHHHHHHHHHHHHHHHN,.  `  `       `          `     ]
(            `    .WHH@HH@HHHHHHHHHHHHHN&.             `             [
(       `           (MHHHHH@HHHHHHHHHHHHHHHMm, `          `      `   ]
J.         `   `      7HHHHHH@HH@HHHHHHHHHHHHHNa, `          `      .]
J]   `                  .YMHHHHHHH@HHHHHHHHHHHHHHN,  `              J]
J@,                        ?YHHHHHHH@HHHHHHHHHHHHHHL    `       `  .H]
JHN,    `   `  `    `            ?"HHHH@HHHHHHHHHHHH-      `      .H@]
J@HM,             `                   ?""WMMHH@HHHMY`         `  .H@H]
J@@HHh    `   `                                                .JH@@@]
JH@H@@M,         `    `  `  `                             `   .H@@HH@]
J@H@HH@HMx.  `     `            `                          ..H@@H@@HH]
J@@H@@H@H@Hh,                          `                 .dH@@H@HH@@@]
JH@H@H@H@H@H@HN..           `                        ..dH@@H@H@H@@HH@]
J@H@H@H@@H@@H@@HHHH+..         `             `  ..JdHH@H@H@@H@H@@H@@H]
J@H@H@HH@HH@H@H@@H@HHHHHHaJ................(gHH@H@H@H@H@H@HH@H@HH@HH@L
```

これをさらに加工します。まず、バッククオートをスペースで置換します。
```bash
cat ascii.csv | sed 's/`/ /g' > ascii2.csv
```
さらにスペース以外の部分を`#`で置換します。
```bash
cat ascii2.csv | sed 's/[^ ]/#/g' > ascii-sharp.csv
```
```
######################################################################
#######################                       ########################
##################                                  ##################
##############            ########                      ##############
###########            ###########                         ###########
#########            ############                            #########
#######            ########                                    #######
#####             ######                                         #####
####             #########                                        ####
###              ###########                                       ###
##              ###############                                     ##
##               ##################                                 ##
#                ######################                              #
#                 ########################                           #
#                   ##########################                       #
##                    ###########################                   ##
##                      ###########################                 ##
###                        #########################               ###
####                             ####################             ####
#####                                 ##############             #####
######                                                         #######
########                                                      ########
###########                                                ###########
#############                                            #############
#################                                    #################
######################                          ######################
######################################################################
```
出来たものをランレングス圧縮します。

:::details 圧縮アルゴリズム

```ruby
prev = nil
count = 0
result = ""
harada = %w(H A R A D A)
harada_idx = 0

ARGF.each_char do |c|
  if c == "\n"
    c = "@"
  end
  if c == prev
    count += 1
  else
    if prev
      if prev == " "
        result << harada[harada_idx]
        harada_idx = (harada_idx + 1) % harada.size
        result << (count > 1 ? count.to_s : "")
      else
        result << (count > 1 ? "#{prev}#{count}" : prev)
      end
    end
    prev = c
    count = 1
  end
end
if prev
  if prev == " "
    result << harada[harada_idx]
    harada_idx = (harada_idx + 1) % harada.size
    result << (count > 1 ? count.to_s : "")
  else
    result << (count > 1 ? "#{prev}#{count}" : prev)
  end
end
puts result
```
:::


``` text:圧縮後
#70@#23H23#24@#18A34#18@#14R12#8A22#14@#11D12#11A25#11@#9H12#12A28#9@#7R12#8A36#7@#5D13#6A41#5@#4H13#9A40#4@#3R14#11A39#3@#2D14#15A37#2@#2H15#18A33#2@#R16#22A30#@#D17#24A27#@#H19#26A23#@#2R20#27A19#2@#2D22#27A17#2@#3H24#25A15#3@#4R29#20A13#4@#5D33#14A13#5@#6H57#7@#8A54#8@#11R48#11@#13A44#13@#17D36#17@#22A26#22@#70
```

改行は`@`、スペースはアルファベットで表しています^[実はアルファベットはHARADAが順番に出てくるようになっています]。
また、これの復元アルゴリズムも作っておきます。

アスキーアートの準備はここまでです。

```ruby:quine.gen.rb
eval$s=%w(
s=%(eval$s=%w(#{$s})*"");
#ここに成形用のプログラムを書く
)*""
```
アスキーアートQuineを作るには、上のプログラムの適切な部分に成形用のコードを入れれば良いです。ここに圧縮後の文字列と復元アルゴリズムを書いて実行すると、冒頭で示したアスキーアートQuineが得られます^[変数名を変えながら文字数を調整しました]。

:::details Quine.gen.rb(完全版)
```ruby:quine.gen.rb
eval$s=%w(
s=%(eval$s=%w(#{$s})*"");
f=->n{s.slice!(0,n)};
fish="#70@#23H23#24@#18A34#18@#14R12#8A22#14@#11D12#11A25#11@#9H12#12A28#9@#7R12#8A36#7@#5D13#6A41#5@#4H13#9A40#4@#3R14#11A39#3@#2D14#15A37#2@#2H15#18A33#2@#R16#22A30#@#D17#24A27#@#H19#26A23#@#2R20#27A19#2@#2D22#27A17#2@#3H24#25A15#3@#4R29#20A13#4@#5D33#14A13#5@#6H57#7@#8A54#8@#11R48#11@#13A44#13@#17D36#17@#22A26#22@#70";
output = "";
i = 0;
len=fish.size;
i=0;
len.times{
  c = fish[i];
  if(c!='@'&&c!='#');
    j = i + 1;
    len = "";
    (fish.size - j).times{|k|
      if(!(fish[j] =~ /[0-9]/));
        break;
      end;
      len << fish[j];
      j += 1;
    };
    count = len.to_i;
    print(32.chr * count);
    i = j;
    elsif(c == "@");
    print("\n");
    i += 1;
  else;
    j = i + 1;
    l = "";
    (fish.size - j).times{|k|
      if(!(fish[j] =~ /[0-9]/));
        break;
      end;
      l << fish[j];
      j += 1;
    };
    len = l.to_i;
    print(f[len]);
    i = j;
  end;
};
puts();#This_program_is_a_Ruby_quine.___##arad166##Kento_Harada####
)*""
```
:::


```shell-session
harada@pc:~/projects/quine/prof-quine$ ruby quine.gen.rb > quine.rb
harada@pc:~/projects/quine/prof-quine$ ruby quine.rb > output.rb
harada@pc:~/projects/quine/prof-quine$ diff -s quine.rb output.rb
Files quine.rb and output.rb are identical
```
Quineになっているようです。

# 感想
アスキーアートQuineは敷居が高いイメージがありましたが、この程度であれば思ったより簡単に作ることができました。より芸術点の高いQuineが作れるよう、精進を続けたいと思います。