
# BUDT 758X
## Assignment#1
## Xukun LIU
## Feb 7, 2019

### Exercise #1 (3 points)

One of the earliest forms of cryptography was the Caesar cipher, a form of substitution cipher in which each letter in the alphabet is shifted by a fixed number of positions (with wrapping). Caesar himself used a left shift of three (-3), but any shift can be used. For example, a Caesar cipher with a right shift of two (+2) would replace the letter 'A' with the letter 'C', the letter 'B' with the letter 'D', and so on, with the letters 'Y' and 'Z' being replaced with the letters 'A' and 'B', respectively. In such a scheme, the word 'ANALYTICS' would be encrypted as 'CPCNAVKEU'. 

Define a function shift_alpha that takes in an alphabet string (A) and a shift constant (shift, default value of 0), prints the original and shifted alphabet (each as a single string), and returns a translation dictionary that contains each original letter as the key and the encrypted letter as the value. Demonstrate the performance of your function on the upper case alphabet with a shift of 0, +12, and -3.

Hint:

In the string module, there are built-in string constants ascii_lowercase and ascii_uppercase that contains lower case letters (a-z) and upper case letters (A-Z) that you can use in your solution.

### Exercise #1


```python
import string
print(string.ascii_lowercase)
print(string.ascii_uppercase)
```

    abcdefghijklmnopqrstuvwxyz
    ABCDEFGHIJKLMNOPQRSTUVWXYZ



```python
def shift_alpha(alphabet, shift = 0): # take alphabet, shift as input, default value for shift =0
    if alphabet.isalpha(): # check if the input is a alphabet
        trans_dict = {}
        for char in string.ascii_lowercase:
            loc = string.ascii_lowercase.index(char) # find the index of the alphabet in alphabet order
            loc_new = (loc+shift)%26
            trans_dict[char] = string.ascii_lowercase[loc_new]
            #print(string.ascii_lowercase[loc_new])
        for char in string.ascii_uppercase:
            #print(char)
            loc = string.ascii_uppercase.index(char) # find the index of the alphabet in alphabet order
            loc_new = (loc+shift)%26
            trans_dict[char] = string.ascii_uppercase[loc_new]
        
        alphabet_shifted = trans_dict[alphabet]
        # convert the lower case to upper case if applicable.
        print('The original letter is:',alphabet)
        print('The letter shifted by {} is: {}'.format(shift,alphabet_shifted))
    else:
        print('Please input a valid letter')
    return trans_dict
```


```python
# Test the function
shift_alpha('A',0)
print('\n')
shift_alpha('B',12)
print('\n')
shift_alpha('C',-3)
```

    The original letter is: A
    The letter shifted by 0 is: A
    
    
    The original letter is: B
    The letter shifted by 12 is: N
    
    
    The original letter is: C
    The letter shifted by -3 is: Z





    {'a': 'x',
     'b': 'y',
     'c': 'z',
     'd': 'a',
     'e': 'b',
     'f': 'c',
     'g': 'd',
     'h': 'e',
     'i': 'f',
     'j': 'g',
     'k': 'h',
     'l': 'i',
     'm': 'j',
     'n': 'k',
     'o': 'l',
     'p': 'm',
     'q': 'n',
     'r': 'o',
     's': 'p',
     't': 'q',
     'u': 'r',
     'v': 's',
     'w': 't',
     'x': 'u',
     'y': 'v',
     'z': 'w',
     'A': 'X',
     'B': 'Y',
     'C': 'Z',
     'D': 'A',
     'E': 'B',
     'F': 'C',
     'G': 'D',
     'H': 'E',
     'I': 'F',
     'J': 'G',
     'K': 'H',
     'L': 'I',
     'M': 'J',
     'N': 'K',
     'O': 'L',
     'P': 'M',
     'Q': 'N',
     'R': 'O',
     'S': 'P',
     'T': 'Q',
     'U': 'R',
     'V': 'S',
     'W': 'T',
     'X': 'U',
     'Y': 'V',
     'Z': 'W'}



### Exercise #2 (3 points)

Define a function encrypt that takes in a word and a shift (default value = 0), and returns a string containing the encrypted version of the word using a Caesar shift. The function should work properly on upper and lower case letters, and return any non-alphabetic characters as is. Demonstrate that your function works properly on the following list of (case-sensitive) words/phrases with a Caesar shift of +5:

apple, Maryland, Route 66, LaTeX, twenty-first century


```python
def shift_char(alphabet, shift = 0): # take alphabet, shift as input, default value for shift =0
    if alphabet.isalpha(): # check if the input is a alphabet
        trans_dict = {}
        for char in string.ascii_lowercase:
            loc = string.ascii_lowercase.index(char) # find the index of the alphabet in alphabet order
            loc_new = (loc+shift)%26
            trans_dict[char] = string.ascii_lowercase[loc_new]
            #print(string.ascii_lowercase[loc_new])
        for char in string.ascii_uppercase:
            #print(char)
            loc = string.ascii_uppercase.index(char) # find the index of the alphabet in alphabet order
            loc_new = (loc+shift)%26
            trans_dict[char] = string.ascii_uppercase[loc_new]
        
        alphabet_shifted = trans_dict[alphabet]
        # convert the lower case to upper case if applicable.
    else:
        return alphabet
    return alphabet_shifted
```


```python
# test the performance of the function
print(shift_char(" ",-3))
print(shift_char("A",-3))
print(shift_char("Z",10))
```

     
    X
    J



```python
def encrypt(word, shift_encrypt = 0):
    word_shifted = ''
    #use a for loop to go through all the chars in word
    for char in word:
        word_shifted += shift_char(char,shift_encrypt)
        #re-use shift_char() function to perform letter shift
    return word_shifted
```


```python
# test the performance of the function
print(encrypt('apple',5))
print(encrypt('Maryland',5))
print(encrypt('Route 66',5))
print(encrypt('LaTeX',5))
print(encrypt('twenty-first century',5))
```

    fuuqj
    Rfwdqfsi
    Wtzyj 66
    QfYjC
    ybjsyd-knwxy hjsyzwd


### Exercise #3 (4 points)

Now suppose you receive an encrypted message. Write a function decrypt that takes in a message, and produces all possible translations of the message using a Caesar cipher. Report the decrypted message and the shift (in the range of [-12, 13]) on the following encrypted quotes from Greek philosophers:

1. Aristotle: Swcnkva ku pqv cp cev, kv ku c jcdkv.

2. Demosthenes: Dxlww zaazcefytetpd lcp zqepy esp mprtyytyr zq rcple pyepcactdpd.

3. Hypatia: Fczy cm uh ohzifxgyhn, uhx nby zolnbyl qy nlupyf nby gily nlonb qy wuh wigjlybyhx. Ni ohxylmnuhx nby nbcham nbun uly un iol xiil cm nby vymn jlyjuluncih zil ohxylmnuhxcha nbimy nbun fcy vysihx.


```python
def decrypt(message):
    for i in range(-12,13):
        message_shifted = ''
        for char in message:
            message_shifted += shift_char(char,i)
        print(str(i)+" : "+message_shifted)
```


```python
sen1 = "Swcnkva ku pqv cp cev, kv ku c jcdkv."
sen2 = "Dxlww zaazcefytetpd lcp zqepy esp mprtyytyr zq rcple pyepcactdpd."
sen3 = "Fczy cm uh ohzifxgyhn, uhx nby zolnbyl qy nlupyf nby gily nlonb qy wuh wigjlybyhx. Ni ohxylmnuhx nby nbcham nbun uly un iol xiil cm nby vymn jlyjuluncih zil ohxylmnuhxcha nbimy nbun fcy vysihx."
```


```python
decrypt(sen1)
# decrypt shift index: -2
# -2 : Quality is not an act, it is a habit.
```

    -12 : Gkqbyjo yi dej qd qsj, yj yi q xqryj.
    -11 : Hlrczkp zj efk re rtk, zk zj r yrszk.
    -10 : Imsdalq ak fgl sf sul, al ak s zstal.
    -9 : Jntebmr bl ghm tg tvm, bm bl t atubm.
    -8 : Koufcns cm hin uh uwn, cn cm u buvcn.
    -7 : Lpvgdot dn ijo vi vxo, do dn v cvwdo.
    -6 : Mqwhepu eo jkp wj wyp, ep eo w dwxep.
    -5 : Nrxifqv fp klq xk xzq, fq fp x exyfq.
    -4 : Osyjgrw gq lmr yl yar, gr gq y fyzgr.
    -3 : Ptzkhsx hr mns zm zbs, hs hr z gzahs.
    -2 : Quality is not an act, it is a habit.
    -1 : Rvbmjuz jt opu bo bdu, ju jt b ibcju.
    0 : Swcnkva ku pqv cp cev, kv ku c jcdkv.
    1 : Txdolwb lv qrw dq dfw, lw lv d kdelw.
    2 : Uyepmxc mw rsx er egx, mx mw e lefmx.
    3 : Vzfqnyd nx sty fs fhy, ny nx f mfgny.
    4 : Wagroze oy tuz gt giz, oz oy g nghoz.
    5 : Xbhspaf pz uva hu hja, pa pz h ohipa.
    6 : Ycitqbg qa vwb iv ikb, qb qa i pijqb.
    7 : Zdjurch rb wxc jw jlc, rc rb j qjkrc.
    8 : Aekvsdi sc xyd kx kmd, sd sc k rklsd.
    9 : Bflwtej td yze ly lne, te td l slmte.
    10 : Cgmxufk ue zaf mz mof, uf ue m tmnuf.
    11 : Dhnyvgl vf abg na npg, vg vf n unovg.
    12 : Eiozwhm wg bch ob oqh, wh wg o vopwh.



```python
decrypt(sen2)
# decrypt shift index: -11
# -11 : Small opportunities are often the beginning of great enterprises.
```

    -12 : Rlzkk noonqstmhshdr zqd nesdm sgd adfhmmhmf ne fqdzs dmsdqoqhrdr.
    -11 : Small opportunities are often the beginning of great enterprises.
    -10 : Tnbmm pqqpsuvojujft bsf pgufo uif cfhjoojoh pg hsfbu foufsqsjtft.
    -9 : Uocnn qrrqtvwpkvkgu ctg qhvgp vjg dgikppkpi qh itgcv gpvgtrtkugu.
    -8 : Vpdoo rssruwxqlwlhv duh riwhq wkh ehjlqqlqj ri juhdw hqwhusulvhv.
    -7 : Wqepp sttsvxyrmxmiw evi sjxir xli fikmrrmrk sj kviex irxivtvmwiw.
    -6 : Xrfqq tuutwyzsnynjx fwj tkyjs ymj gjlnssnsl tk lwjfy jsyjwuwnxjx.
    -5 : Ysgrr uvvuxzatozoky gxk ulzkt znk hkmottotm ul mxkgz ktzkxvxoyky.
    -4 : Zthss vwwvyabupaplz hyl vmalu aol ilnpuupun vm nylha lualywypzlz.
    -3 : Auitt wxxwzbcvqbqma izm wnbmv bpm jmoqvvqvo wn ozmib mvbmzxzqama.
    -2 : Bvjuu xyyxacdwrcrnb jan xocnw cqn knprwwrwp xo panjc nwcnayarbnb.
    -1 : Cwkvv yzzybdexsdsoc kbo ypdox dro loqsxxsxq yp qbokd oxdobzbscoc.
    0 : Dxlww zaazcefytetpd lcp zqepy esp mprtyytyr zq rcple pyepcactdpd.
    1 : Eymxx abbadfgzufuqe mdq arfqz ftq nqsuzzuzs ar sdqmf qzfqdbdueqe.
    2 : Fznyy bccbeghavgvrf ner bsgra gur ortvaavat bs terng ragrecevfrf.
    3 : Gaozz cddcfhibwhwsg ofs cthsb hvs psuwbbwbu ct ufsoh sbhsfdfwgsg.
    4 : Hbpaa deedgijcxixth pgt duitc iwt qtvxccxcv du vgtpi tcitgegxhth.
    5 : Icqbb effehjkdyjyui qhu evjud jxu ruwyddydw ev whuqj udjuhfhyiui.
    6 : Jdrcc fggfiklezkzvj riv fwkve kyv svxzeezex fw xivrk vekvigizjvj.
    7 : Kesdd ghhgjlmfalawk sjw gxlwf lzw twyaffafy gx yjwsl wflwjhjakwk.
    8 : Lftee hiihkmngbmbxl tkx hymxg max uxzbggbgz hy zkxtm xgmxkikblxl.
    9 : Mguff ijjilnohcncym uly iznyh nby vyachhcha iz alyun yhnyljlcmym.
    10 : Nhvgg jkkjmopidodzn vmz jaozi ocz wzbdiidib ja bmzvo ziozmkmdnzn.
    11 : Oiwhh kllknpqjepeao wna kbpaj pda xacejjejc kb cnawp ajpanlneoao.
    12 : Pjxii lmmloqrkfqfbp xob lcqbk qeb ybdfkkfkd lc dobxq bkqbomofpbp.



```python
decrypt(sen3)
# decrypt shift index: -11
#6 : Life is an unfoldment, and the further we travel the more truth we can comprehend.
# To understand the things that are at our door is the best preparation for understanding those that lie beyond.
```

    -12 : Tqnm qa iv cvnwtlumvb, ivl bpm nczbpmz em bzidmt bpm uwzm bzcbp em kiv kwuxzmpmvl. Bw cvlmzabivl bpm bpqvoa bpib izm ib wcz lwwz qa bpm jmab xzmxizibqwv nwz cvlmzabivlqvo bpwam bpib tqm jmgwvl.
    -11 : Uron rb jw dwoxumvnwc, jwm cqn odacqna fn cajenu cqn vxan cadcq fn ljw lxvyanqnwm. Cx dwmnabcjwm cqn cqrwpb cqjc jan jc xda mxxa rb cqn knbc yanyjajcrxw oxa dwmnabcjwmrwp cqxbn cqjc urn knhxwm.
    -10 : Vspo sc kx expyvnwoxd, kxn dro pebdrob go dbkfov dro wybo dbedr go mkx mywzboroxn. Dy exnobcdkxn dro drsxqc drkd kbo kd yeb nyyb sc dro locd zbozkbkdsyx pyb exnobcdkxnsxq dryco drkd vso loiyxn.
    -9 : Wtqp td ly fyqzwoxpye, lyo esp qfcespc hp eclgpw esp xzcp ecfes hp nly nzxacpspyo. Ez fyopcdelyo esp estyrd esle lcp le zfc ozzc td esp mpde acpalcletzy qzc fyopcdelyotyr eszdp esle wtp mpjzyo.
    -8 : Xurq ue mz gzraxpyqzf, mzp ftq rgdftqd iq fdmhqx ftq yadq fdgft iq omz oaybdqtqzp. Fa gzpqdefmzp ftq ftuzse ftmf mdq mf agd paad ue ftq nqef bdqbmdmfuaz rad gzpqdefmzpuzs ftaeq ftmf xuq nqkazp.
    -7 : Yvsr vf na hasbyqzrag, naq gur shegure jr geniry gur zber gehgu jr pna pbzceruraq. Gb haqrefgnaq gur guvatf gung ner ng bhe qbbe vf gur orfg cercnengvba sbe haqrefgnaqvat gubfr gung yvr orlbaq.
    -6 : Zwts wg ob ibtczrasbh, obr hvs tifhvsf ks hfojsz hvs acfs hfihv ks qob qcadfsvsbr. Hc ibrsfghobr hvs hvwbug hvoh ofs oh cif rccf wg hvs psgh dfsdofohwcb tcf ibrsfghobrwbu hvcgs hvoh zws psmcbr.
    -5 : Axut xh pc jcudasbtci, pcs iwt ujgiwtg lt igpkta iwt bdgt igjiw lt rpc rdbegtwtcs. Id jcstghipcs iwt iwxcvh iwpi pgt pi djg sddg xh iwt qthi egtepgpixdc udg jcstghipcsxcv iwdht iwpi axt qtndcs.
    -4 : Byvu yi qd kdvebtcudj, qdt jxu vkhjxuh mu jhqlub jxu cehu jhkjx mu sqd secfhuxudt. Je kdtuhijqdt jxu jxydwi jxqj qhu qj ekh teeh yi jxu ruij fhufqhqjyed veh kdtuhijqdtydw jxeiu jxqj byu ruoedt.
    -3 : Czwv zj re lewfcudvek, reu kyv wlikyvi nv kirmvc kyv dfiv kilky nv tre tfdgivyveu. Kf leuvijkreu kyv kyzexj kyrk riv rk fli uffi zj kyv svjk givgrirkzfe wfi leuvijkreuzex kyfjv kyrk czv svpfeu.
    -2 : Daxw ak sf mfxgdvewfl, sfv lzw xmjlzwj ow ljsnwd lzw egjw ljmlz ow usf ugehjwzwfv. Lg mfvwjklsfv lzw lzafyk lzsl sjw sl gmj vggj ak lzw twkl hjwhsjslagf xgj mfvwjklsfvafy lzgkw lzsl daw twqgfv.
    -1 : Ebyx bl tg ngyhewfxgm, tgw max ynkmaxk px mktoxe max fhkx mknma px vtg vhfikxaxgw. Mh ngwxklmtgw max mabgzl matm tkx tm hnk whhk bl max uxlm ikxitktmbhg yhk ngwxklmtgwbgz mahlx matm ebx uxrhgw.
    0 : Fczy cm uh ohzifxgyhn, uhx nby zolnbyl qy nlupyf nby gily nlonb qy wuh wigjlybyhx. Ni ohxylmnuhx nby nbcham nbun uly un iol xiil cm nby vymn jlyjuluncih zil ohxylmnuhxcha nbimy nbun fcy vysihx.
    1 : Gdaz dn vi piajgyhzio, viy ocz apmoczm rz omvqzg ocz hjmz ompoc rz xvi xjhkmzcziy. Oj piyzmnoviy ocz ocdibn ocvo vmz vo jpm yjjm dn ocz wzno kmzkvmvodji ajm piyzmnoviydib ocjnz ocvo gdz wztjiy.
    2 : Heba eo wj qjbkhziajp, wjz pda bqnpdan sa pnwrah pda ikna pnqpd sa ywj ykilnadajz. Pk qjzanopwjz pda pdejco pdwp wna wp kqn zkkn eo pda xaop lnalwnwpekj bkn qjzanopwjzejc pdkoa pdwp hea xaukjz.
    3 : Ifcb fp xk rkcliajbkq, xka qeb croqebo tb qoxsbi qeb jlob qorqe tb zxk zljmobebka. Ql rkabopqxka qeb qefkdp qexq xob xq lro allo fp qeb ybpq mobmxoxqflk clo rkabopqxkafkd qelpb qexq ifb ybvlka.
    4 : Jgdc gq yl sldmjbkclr, ylb rfc dsprfcp uc rpytcj rfc kmpc rpsrf uc ayl amknpcfclb. Rm slbcpqrylb rfc rfgleq rfyr ypc yr msp bmmp gq rfc zcqr npcnypyrgml dmp slbcpqrylbgle rfmqc rfyr jgc zcwmlb.
    5 : Khed hr zm tmenkcldms, zmc sgd etqsgdq vd sqzudk sgd lnqd sqtsg vd bzm bnloqdgdmc. Sn tmcdqrszmc sgd sghmfr sgzs zqd zs ntq cnnq hr sgd adrs oqdozqzshnm enq tmcdqrszmchmf sgnrd sgzs khd adxnmc.
    6 : Life is an unfoldment, and the further we travel the more truth we can comprehend. To understand the things that are at our door is the best preparation for understanding those that lie beyond.
    7 : Mjgf jt bo vogpmenfou, boe uif gvsuifs xf usbwfm uif npsf usvui xf dbo dpnqsfifoe. Up voefstuboe uif uijoht uibu bsf bu pvs epps jt uif cftu qsfqbsbujpo gps voefstuboejoh uiptf uibu mjf cfzpoe.
    8 : Nkhg ku cp wphqnfogpv, cpf vjg hwtvjgt yg vtcxgn vjg oqtg vtwvj yg ecp eqortgjgpf. Vq wpfgtuvcpf vjg vjkpiu vjcv ctg cv qwt fqqt ku vjg dguv rtgrctcvkqp hqt wpfgtuvcpfkpi vjqug vjcv nkg dgaqpf.
    9 : Olih lv dq xqirogphqw, dqg wkh ixuwkhu zh wudyho wkh pruh wuxwk zh fdq frpsuhkhqg. Wr xqghuvwdqg wkh wklqjv wkdw duh dw rxu grru lv wkh ehvw suhsdudwlrq iru xqghuvwdqglqj wkrvh wkdw olh ehbrqg.
    10 : Pmji mw er yrjsphqirx, erh xli jyvxliv ai xvezip xli qsvi xvyxl ai ger gsqtvilirh. Xs yrhivwxerh xli xlmrkw xlex evi ex syv hssv mw xli fiwx tvitevexmsr jsv yrhivwxerhmrk xlswi xlex pmi ficsrh.
    11 : Qnkj nx fs zsktqirjsy, fsi ymj kzwymjw bj ywfajq ymj rtwj ywzym bj hfs htruwjmjsi. Yt zsijwxyfsi ymj ymnslx ymfy fwj fy tzw ittw nx ymj gjxy uwjufwfynts ktw zsijwxyfsinsl ymtxj ymfy qnj gjdtsi.
    12 : Rolk oy gt atlurjsktz, gtj znk laxznkx ck zxgbkr znk suxk zxazn ck igt iusvxknktj. Zu atjkxyzgtj znk znotmy zngz gxk gz uax juux oy znk hkyz vxkvgxgzout lux atjkxyzgtjotm znuyk zngz rok hkeutj.

