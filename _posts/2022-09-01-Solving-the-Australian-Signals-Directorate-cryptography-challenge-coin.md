---
layout: post
author: Sen
title: "Solving the Australian Signals Directorate cryptography challenge coin"
tags: []
categories: hacktheplanet
twitter: https://twitter.com/senwerks/status/1416976612470394882
github: 
image: 2021-07-20-DMG01-LiPo-07.jpg
---

Today the Australian Signals Directorate announced their [75th Anniversary Commemorative Coin](https://www.asd.gov.au/75th-anniversary/events/2022-09-01-75th-anniversary-commemorative-coin), which is a standard Australian 50 cent coin with various cryptographic puzzles embedded in it. I'm not a cryptography expert, but I've always loved this stuff from the sidelines of physical pentesting and teen-years script-kiddying, so I thought I'd give it a go. Along with a mate in our local Hackerspace's slack channel, we started bouncing ideas back and forth, and below is a write-up of the eventual path to solving all the puzzles on the coin (though as you'll see, not necessarily in the order they intended).

The coin itself looks like this:

![ASD 50c Coin - Front](/images/2022-09-01-ASD-50c-Coin-1.png)

![ASD 50c Coin - Back](/images/2022-09-01-ASD-50c-Coin-2.png)

The first thing we did is transcribe the text from the coin to a note file, so we had it copy-pastable:

> Heads Side
> 
> B    T    H    A    S    A 
> ''   :    :'   '    '.   .:
> 
> Tails Side
> 
> Outer Ring: 
> dvzivzfwzxrlfhrmxlmxvkgzmwnvgrxfolfhrmvcvxfgrlm
> urmwxozirgbrm7drwgsc5wvkgs
> 
> Inner Ring:
> bgoamvoeiatsirlngttneogrergxnteaifcecaieoalekfnr5lwefchdeeaeee7nmdrxx5
> 
> Central Block:
> e3b8287d4290f7233814d7a47a291dc0f71b2806d1a53b311cc4b97a0e1cc2b93b31068593332f10c6a3352f14d1b27a3514d6f7382f1ad0b0322955d1b83d3801cdb2287d05c0b82a311085a033291d85a3323855d6bc333119d6fb7a3c11c4a72e3c17ccbb33290c85b6343955ccba3b3a1ccbb62e341acbf72e3255caa73f2f14d1b27a341b85a3323855d6bb333055c4a53f3c55c7b22e2a10c0b97a291dc0f73e3413c3be392819d1f73b331185a3323855ccba2a3206d6be3831108b

The press release made lots of mention of WWII code breakers, and had the word "enigma" mentioned in it, as well as hinting that you would need Wikipedia to solve it all... so I thought the old Enigma machine must have had something to do with all this? The "BTHASA" and dots underneath lined up with the Enigma machine having 3 rotors each with a position/ring pair. This led me down an hour+ one-way trip to nowhere, as I just couldn't figure out how to make it fit into the Enigma criteria. While doing this, I was plugging the strings into [Cyberchef](https://gchq.github.io/CyberChef/) and trying random recipes just to see if I fluked on something that'd help (never underestimate aspergers-level bruteforcing while watching shows on your other monitor). It did. 

Throwing the first string in the "Outer Ring" part of our notes and choosing Atbash Cipher in Cyberchef gave me readable text:

![ASD 50c Coin - weareaudaciousinconceptandmeticulousinexecution](/images/2022-09-01-ASD-50c-Coin-3.png)

The result reads: weareaudaciousinconceptandmeticulousinexecution

Throwing in the 2nd string from the same part gives:

![ASD 50c Coin - findclarityin7widthx5depth](/images/2022-09-01-ASD-50c-Coin-4.png)

The result reads: findclarityin7widthx5depth

The first part is a reference to the ASD "Values", as seen [on their website](https://www.asd.gov.au/about/values). The second part is obviously a clue for the next puzzle.

At this point I figured out the dots on the Heads side of the coin could be some form of grid pattern, and looked up the [Wikipedia entry on Braille](https://en.wikipedia.org/wiki/Braille). In there, was this section showing that a 4-dot version of Braille is used to show both the start of the alphabet and also numbers 0-9. 

![ASD 50c Coin - findclarityin7widthx5depth](/images/2022-09-01-ASD-50c-Coin-5.png)

I translated it in our notes to show that the symbols could now either mean "C B F A E D" or "3 2 6 1 5 4". My mate noted that the letters above each Braille symbol, when re-ordered into numerical order based on those Braille numbers before, spells out ATBASH... oh wait, we already figured that puzzle out (thanks Cyberchef, I love you).

Next we spent a while trying to figure out what "find clarity in 7 width x 5 depth" means. Obviously referring to some kind of matrix/grid, and there were multiple rabbit holes there to do with mathetmatical matrix puzzles and grid based ciphers. My mate and I here both managed to solve this one at the same time using 2 very different methods, which I thought was pretty cool... he was coding up a python script that organised the letters and I was sitting in VS Code manually copy/pasting chunks of the string into rows/columns. We both came up with this though:

> bgoamvo
> eiatsir
> lngttne
> ogrergx
> nteaifc
> 
> ecaieoa
> lekfnr5
> lwefchd
> eeaeee7
> nmdrxx5

... which if read as columns, reads: "belongingtoagreatteamstrivingforexcellencewemakeadifferencexorhexa5d75" or "Belonging to a great team striving for excellence we make a difference XOR HEX a5d75".

Clearly the "XOR HEX a5d75" part is the clue, and I know what a XOR gate is... but I didn't realise there was also a "XOR Cipher" until doing some more web searching (again, not an expert). My search came up with the Wikipedia page about XOR Ciphers, and an example, but more helpfully came up with this ["XOR of two hexadecimal strings" tool](https://tomeko.net/online_tools/xor.php?lang=en) right on the first page. In VS Code I repeated the "a5d75" key until it was the same length as the source text (as per the Wikipedia example) and plugged them into the tool:

![ASD 50c Coin - findclarityin7widthx5depth](/images/2022-09-01-ASD-50c-Coin-6.png)

That gives us the output:

'''
0x46, 0x6F, 0x72, 0x20, 0x37, 0x35, 0x20, 0x79, 0x6E, 0x61, 0x72, 0x73, 0x20, 0x74, 0x68, 0x65, 
0x20, 0x41, 0x75, 0x73, 0x74, 0x72, 0x61, 0x6C, 0x69, 0x61, 0x6E, 0x20, 0x53, 0x69, 0x67, 0x6E, 
0x61, 0x6C, 0x73, 0x20, 0x44, 0x69, 0x72, 0x65, 0x63, 0x74, 0x6F, 0x72, 0x61, 0x74, 0x65, 0x20, 
0x68, 0x61, 0x73, 0x20, 0x62, 0x72, 0x6F, 0x75, 0x67, 0x68, 0x74, 0x20, 0x74, 0x6F, 0x67, 0x65, 
0x74, 0x68, 0x65, 0x72, 0x20, 0x70, 0x65, 0x6F, 0x70, 0x6C, 0x65, 0x20, 0x77, 0x69, 0x74, 0x68, 
0x20, 0x74, 0x68, 0x65, 0x20, 0x73, 0x6B, 0x69, 0x6C, 0x6C, 0x73, 0x2C, 0x20, 0x61, 0x64, 0x61, 
0x70, 0x74, 0x61, 0x62, 0x69, 0x6C, 0x69, 0x74, 0x79, 0x20, 0x61, 0x6E, 0x64, 0x20, 0x69, 0x6D, 
0x61, 0x67, 0x69, 0x6E, 0x61, 0x74, 0x69, 0x6F, 0x6E, 0x20, 0x74, 0x6F, 0x20, 0x6F, 0x70, 0x65, 
0x72, 0x61, 0x74, 0x65, 0x20, 0x69, 0x6E, 0x20, 0x74, 0x68, 0x65, 0x20, 0x73, 0x6C, 0x69, 0x6D, 
0x20, 0x61, 0x72, 0x65, 0x61, 0x20, 0x62, 0x65, 0x74, 0x77, 0x65, 0x65, 0x6E, 0x20, 0x74, 0x68, 
0x65, 0x20, 0x64, 0x69, 0x66, 0x66, 0x69, 0x63, 0x75, 0x6C, 0x74, 0x20, 0x61, 0x6E, 0x64, 0x20, 
0x74, 0x68, 0x65, 0x20, 0x69, 0x6D, 0x70, 0x6F, 0x73, 0x73, 0x69, 0x69, 0x6C, 0x65, 0x2E, 
'''

Throw that back into Cyberchef again, and we get the final answer to all the puzzles:

![ASD 50c Coin - findclarityin7widthx5depth](/images/2022-09-01-ASD-50c-Coin-7.png)

Output reads:

> "For 75 ynars the Australian Signals Directorate has brought together people with the skills, adaptability and imagination to operate in the slim area between the difficult and the impossiile."

Yes, there's a typo there... I assume that comes from a typo earlier in our processes, but I left it here to show exactly how it all came out.

It was a fun series of puzzles, but nowhere near the complexity of a lot of those shared via DEFCON/etc (most of which I can get a few steps into then my brain explodes and I go drink a bottle of sake). I can't imagine this was difficult for anyone actually in the industry, so I assume all the media hype about "solve this and you could get a job as a spy!" is just the usual media bullshit... or Cyberchef and basic web searches has made puzzles like this as obsolete as me :) 

Still, I enjoyed it, and while doing all of the above I managed to get through the 2 hour queue on the Australian Mint web store and snag myself a physical copy of the coin itself, so that's cool too.