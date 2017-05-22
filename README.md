![](http://ww4.sinaimg.cn/large/006tNc79ly1fftwu9cvqfj30p00iyn1x.jpg)

## 正确的信息

captionWriter = 李琰 

keywords = 中国 

headline = （一带一路·高峰论坛）习近平会见波兰总理希德沃 

dateCreated = 20170512 

copyright = 新华通讯社 

category = 18 

caption = 新华社照片，北京，2017年5月12日 习近平会见波兰总理希德沃 5月12日，国家主席习近平在北京人民大会堂会见来华出席“一带一路”国际合作高峰论坛的波兰总理希德沃。 新华社记者 谢环驰 摄 

byline = 谢环驰

## 直接getUint8()

<<<<<<< HEAD
> getUint8()每8个比特提取为一个字，非汉字是正确的，但是直接将汉字分为两个Unicode，被编译成拉丁文
=======
>getUint8()每8个比特提取为一个字，非汉字是正确的，但是直接将汉字分为两个Unicode，被编译成拉丁文
>>>>>>> gh-pages

```
function getStringFromDB(buffer, start, length) {
        var outstr = "";
        for (n = start; n < start+length; n++) {
            outstr += String.fromCharCode(buffer.getUint8(n));            
        }
        return outstr;
    }
```



captionWriter = Àîçü 

keywords = ÖÐ¹ú 

headline = £¨Ò»´øÒ»Â·¡¤¸ß·åÂÛÌ³£©Ï°½üÆ½»á¼û²¨À¼×ÜÀíÏ£µÂÎÖ 

dateCreated = 20170512 

copyright = ÐÂ»ªÍ¨Ñ¶Éç 

category = 18 

caption = ÐÂ»ªÉçÕÕÆ¬£¬±±¾©£¬2017Äê5ÔÂ12ÈÕ Ï°½üÆ½»á¼û²¨À¼×ÜÀíÏ£µÂÎÖ 5ÔÂ12ÈÕ£¬¹ú¼ÒÖ÷Ï¯Ï°½üÆ½ÔÚ±±¾©ÈËÃñ´ó»áÌÃ»á¼ûÀ´»ª³öÏ¯¡°Ò»´øÒ»Â·¡±¹ú¼ÊºÏ×÷¸ß·åÂÛÌ³µÄ²¨À¼×ÜÀíÏ£µÂÎÖ¡£ ÐÂ»ªÉç¼ÇÕß Ð»»·³Û Éã 

byline = Ð»»·³Û

## 直接getUint16()

> getUint16()每16个比特提取为一个字，能提取出汉字，但是对应关系错误

```
function getFinalStringFromDB(buffer, start, length) {        
        var outstr = "";
        length = length/2;
        for (n = start; n < start+length; ) {
            var buffer10 = buffer.getUint16(n);
            var buffer16 = buffer10.toString(16).toUpperCase();
            var unicode10 = gbk2unicode(buffer16);
            outstr += String.fromCharCode(unicode10);
        }
        return outstr
    }
```



captionWriter = 李铉 

keywords = 中泄 

headline = 一淮带一宦路贰高叻峰迓论厶坛常习 

dateCreated = 

copyright = 新禄华通 

category = 

caption = 新禄华社缯照掌片北本京年月日习敖近平交会峒见波兰甲总芾理硐希德挛沃月日眨国家抑主飨席习敖近平皆在诒北本京 

byline = 谢换环

## 修改n和length

> 因为n的位置应该向后移动两个比特，所以作出修改，此时汉字部分正确，但是非汉字部分解码错误

```
function getFinalStringFromDB(buffer, start, length) {        
        var outstr = "";
        for (n = start; n < start+length; ) {
            var buffer10 = buffer.getUint16(n);
            var buffer16 = buffer10.toString(16).toUpperCase();
            var unicode10 = gbk2unicode(buffer16);
            outstr += String.fromCharCode(unicode10);
            n += 2;
        }
        return outstr
    }
```

captionWriter = 李琰 

keywords = 中国 

headline = 一带一路高峰论坛习近平会见波兰总理希德沃 

dateCreated = 

copyright = 新华通讯社 

category = 

caption = 新华社照片北京年习近平会见波兰总理希德沃月日国家主席习近平在北京人民大会堂会见来华出席一带一路国际合作高峰论坛的波兰总理希德沃禄缂钦谢环驰 

byline = 谢环驰

## 修改if判断

> 对应关系是两个拉丁文字符对应一个汉字，一个汉字占16比特，一个非汉字只占8比特，所以要进行判断。

```
    function getFinalStringFromDB(buffer, start, length) {        
        var outstr = "";
        for (n = start; n < start+length; ) {
            if(buffer.getUint8(n)<127){
                outstr += String.fromCharCode(buffer.getUint8(n));
                n++;
            }else{
                var buffer10 = buffer.getUint16(n);
                var buffer16 = buffer10.toString(16).toUpperCase();
                var unicode10 = gbk2unicode(buffer16);
                var str = String.fromCharCode(unicode10);
                outstr += str;           
                n += 2;
            }          
        }
        return outstr
    }
```

captionWriter = 李琰
keywords = 中国
headline = 一带一路高峰论坛习近平会见波兰总理希德沃
dateCreated = 20170512
copyright = 新华通讯社
category = 18
caption = 新华社照片北京2017年5月12日 习近平会见波兰总理希德沃 5月12日国家主席习近平在北京人民大会堂会见来华出席一带一路国际合作高峰论坛的波兰总理希德沃 新华社记者 谢环驰 摄 
byline = 谢环驰



