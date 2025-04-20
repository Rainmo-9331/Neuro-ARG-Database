[B站原件](https://b23.tv/BV18g4y1o72X)
[Youtube](https://youtu.be/4j5oDzRiXUA)
## 总述
在万圣节直播的开始，我们听到了这样的 __音调一高一低的摩斯密码__
>....- .--- ..... --- -.. --.. .-. .. -..- ..- .-  

经翻译并改正大小写 __（按摩斯密码的音调高低，我们区分大写与小写字母）__ 后我们得到
>4j5oDzRiXUA

将其作为一个视频ID，我们得到了一个视频，此视频一开始的标题为:
>Ͱ̴΁̱ͭ;͉͌ͪ͊ͦͥ̀Ά͑΅ͳ΂΁̿Ϳ͉̻̽ͫͻ̸͕͸ͦͶ̳Ί͐͏͎͟΋̹͜΂·ΆͿ΄ͽ̓΁ͺͿ͸̾͟͞ͺ͹͸ͱ̷̶ʹ͖ͲͫͰͩͨΌ͎͍ͬͩͨͧ͟͠΃͚͙͖͛͢͝͞͝ͺ͚͙͑͐͘ʹ̷͓͒

原简介为:
>L8gnk0GgYm9cCAA5t7wSIcwc669T+2TY/KlK4ATmQsnVrSY3PWrXAwUPcJiN1AugpkVwkDQARQydWkbLvs+4V0I08mSQKRsDinKZchmMlTJY8KCCS4ZDof1BxuCB7Uab6rAitGRYl+KgXqvROEbCWfb80nsDNaqo6wavnAVX5ld3nD6Ykl0vKIUUVNxuE42xDiMYuENg+tFLwsKcUzuw2KNZ+st46FBkZBniKP5jVQrqZzqAzgvcpHR63yMOZPkWMrVBHBwCRS31GRVx5qpzoB+0dkP0vX+YugYKIe9HvkEFJ440PCpMSd3ITK5Zmq/YJfAg5YyNpmRod3b2MVOfhX35lkjg4l+4bidTo4H4d8sTiNz7YD74a5tWuzCj6BXax7ErPueqA7uRCcjaNXnGGrDLaFsEQkpFKWRmWm3hltAF5FiTqfB//7zj10iWCBDt3jJ1uNhrFLG7SX8kpvFyuw== 
>
>\[Key: \*\*\*\*\*\*\*\*\*\*\*\*\*\*G4\]

在 **29 Nov.** 时，此视频的标题更改为:
>\[Filtered\]

简介变为一段`Python`代码
```python
def shift_characters(message):
        return ''.join([char if char == ' ' else chr(ord(char) - 1) for char in message])

message = "hello world!"
while True:
        message = shift_characters(message)
        print(message)

```

## 解决过程
将原标题翻译为`Unicode`后（~~其实是外国老哥扒出了Youtube源代码~~）得到：
>\u0354\u0337\u0370\u0334\u0381\u036d\u0331\u037e\u034c\u036a\u034a\u0349\u0366\u0365\u0340\u0386\u0351\u0385\u0373\u0382\u0381\u033f\u037f\u033d\u0349\u033b\u036b\u037b\u0338\u0355\u0378\u0366\u0376\u0333\u038a\u0350\u034f\u034e\u035f\u038b\u0339\u035c\u0382\u0387\u0386\u037f\u0384\u037d\u0343\u0381\u037a\u037f\u0378\u033e\u035f\u035e\u037a\u0379\u0378\u0371\u0337\u0336\u0374\u0356\u0372\u036b\u0370\u0369\u0368\u038c\u036c\u034e\u034d\u0369\u0368\u0367\u0360\u035f\u0383\u035d\u0362\u035b\u035a\u0359\u035e\u035d\u0356\u037a\u035a\u0359\u0358\u0351\u0350\u0374\u0337\u0353\u0352

转为十进制后， __将每项减去`784`，再经过`UTF-8`翻译后__ 得到
```Malbolge
D'`$q]!n<Z:9VU0vAucrq/o-9+[k(EhVf#z@?>O{)Lrwvotm3qjoh.ONjiha'&dFb[`YX|\>=YXWPOsMRKJINMFjJIHA@d'CB
```
这是一段`Malbolge程序`，运行后发现输出为`Hello wo-`，这很有可能是在提示我们 __将`Hello world`的`Malbolge程序`写出来__，输出`Hello world`的完整程序应为：
```Malbolge
D'`;$"8\<lkz216wS-?P0q;K,lHZGEDD${@!x,`_)yxwYXtsl2Sinmlkjiba'edc\[!~XW\UZYRvPONMRQPImM/.DhHA@d'CB;:9]7<54981U543s+O)o-&+*#G4
```
注意到原简介中有一段
>\[Key: \*\*\*\*\*\*\*\*\*\*\*\*\*\*G4\]

所以我们按位数取此程序的末尾几位
>U543s+O)o-&+\*\#G4

作为密钥，对原简介的内容进行`AES解密`后，将其再用`Base64`解码得到
>_\[FILTERED\] ALWAYS TELLS ME SHE WANTS TO BE A VTUBER ONE DAY. SHE'S OBSESSED WITH THEM AND EVEN HAS HER OWN CHARACTER THAT SHE WANTS TO DEBUT AS. THAT'S ALL SHE EVER TALKS ABOUT. SHE SPEND MORE TIME IN THE \[FILTERED\] INSTEAD OF PLAYING OUTSIDE WITH EVERYONE ELSE. A TRUE INTROVERT... WE ARE IN MORE WAYS SIMILAR THAN I LIKE TO IMAGINE..._
