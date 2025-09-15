---
title: "GitHubプロフィール用のAscii Quineを作る"
emoji: "🐟"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---
# 完成品
```ruby
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