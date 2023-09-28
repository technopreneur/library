---
{"dg-publish":true,"permalink":"/altelyqat-alemryt-literature-notes/sywtyna-allh-mn-fdlh/macd-leader/"}
---

//
// @author LazyBear 
// List of all my indicators: 
// https://docs.google.com/document/d/15AGCufJZ8CIUvwFJ9W-IKns88gkWOKBCvByMEvm5MLo/edit?usp=sharing
//
study("MACD Leader [LazyBear]", shorttitle="MACDL_LB")
src=close
shortLength = input(12, title="Fast Length")
longLength = input(26, title="Slow Length")
sigLength = input(9, title="Signal Length")
showMACD=input(false)
showMACDSignal=input(false)
ma(s,l) => ema(s,l)
sema = ma( src, shortLength )
lema = ma( src, longLength )
i1 = sema + ma( src - sema, shortLength )
i2 = lema + ma( src - lema, longLength )
macdl = i1 - i2
macd=sema-lema

hline(0)
plot( macdl, title="MACDLeader", color=maroon, linewidth=2)
plot(showMACD?macd:na, title="MACD", color=green)
plot(showMACDSignal?sma(macd, sigLength):na, title="Signal", color=red)
