# Yakha iseva yakho yokuthumela imeyili ye-SMTP

## isandulelo

I-SMTP ingathenga ngokuqondile izinsiza kubathengisi bamafu, njenge:

* [I-Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [I-Ali cloud imeyili push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Ungakwazi futhi ukwakha iseva yakho yemeyili - ukuthumela okungenamkhawulo, izindleko eziphansi.

Ngezansi, sibonisa isinyathelo ngesinyathelo ukuthi singazakha kanjani iseva yethu yemeyili.

## Ukukhetha iseva

Iseva ye-SMTP esingethwe yona idinga i-IP yomphakathi enezimbobo ezingu-25, 456, nezingu-587 ezivuliwe.

Amafu omphakathi asetshenziswa ngokujwayelekile avimbe lawa machweba ngokuzenzakalelayo, futhi kungenzeka ukuwavula ngokukhipha i-oda lomsebenzi, kodwa kuyinkinga kakhulu phela.

Ngincoma ukuthenga kumsingathi onalezi zimbobo ezivuliwe futhi osekela ukusetha amagama esizinda ahlehlayo.

Lapha, ngincoma [i-Contabo](https://contabo.com) .

U-Contabo ungumnikezeli wokubamba ozinze eMunich, eJalimane, owasungulwa ngo-2003 ngamanani ancintisana kakhulu.

Uma ukhetha i-Euro njengohlobo lwemali lokuthenga, intengo izoba eshibhile (iseva enenkumbulo engu-8GB kanye nama-CPU angu-4 abiza cishe ama-yuan angu-529 ngonyaka, futhi imali yokuqala yokufaka imahhala unyaka owodwa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Lapho ufaka i-oda, phawula `prefer AMD` , futhi iseva ene-AMD CPU izosebenza kangcono.

Ngokulandelayo, ngizothatha i-VPS kaContabo njengesibonelo ukuze ngibonise indlela yokwakha iseva yakho yemeyili.

## Ukucushwa kwesistimu ye-Ubuntu

Uhlelo lokusebenza lapha Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Uma iseva ku-ssh ibonisa `Welcome to TinyCore 13!` (njengoba kukhonjisiwe esithombeni esingezansi), kusho ukuthi uhlelo alukafakwa. Sicela unqamule i-ssh bese ulinda imizuzu embalwa ukuze ungene futhi.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Uma `Welcome to Ubuntu 22.04.1 LTS` kuvela, ukuqalisa sekuphelile, futhi ungaqhubeka nezinyathelo ezilandelayo.

### [Ongakukhetha] Qalisa indawo yokuthuthukisa

Lesi sinyathelo singokuzithandela.

Ukuze kube lula, ngifake ukufakwa nokucushwa kwesistimu yesofthiwe yobuntu [ku-github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Qalisa umyalo olandelayo ukuze uwufake ngokuchofoza okukodwa.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Abasebenzisi baseShayina, sicela nisebenzise umyalo olandelayo esikhundleni salokho, futhi ulimi, indawo yesikhathi, njll. kuzosethwa ngokuzenzakalelayo.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### I-Contabo inika amandla i-IPV6

Nika amandla i-IPV6 ukuze i-SMTP ikwazi nokuthumela ama-imeyili anamakheli e-IPV6.

hlela `/etc/sysctl.conf`

Lungisa noma wengeze imigqa elandelayo

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Landela [ngesifundo se-contabo: Ukwengeza uxhumano lwe-IPv6 kuseva yakho](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Hlela `/etc/netplan/01-netcfg.yaml` , engeza imigqa embalwa njengoba kukhonjisiwe esithombeni esingezansi (Ifayela lokumisa elizenzakalelayo le-Contabo VPS selinayo le migqa, vele uyeke ukuphawula).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Bese `netplan apply` ukwenza ukucushwa okushintshiwe kusebenze.

Ngemuva kokuthi ukumisa kube yimpumelelo, ungasebenzisa `curl 6.ipw.cn` ukuze ubuke ikheli le-ipv6 lenethiwekhi yakho yangaphandle.

## Vala ama-ops enqolobane yokucushwa

```
git clone https://github.com/wactax/ops.soft.git
```

## Khiqiza isitifiketi samahhala se-SSL segama lakho lesizinda

Ukuthumela imeyili kudinga isitifiketi se-SSL ukuze ibethelwe futhi isayinwe.

Sisebenzisa [i-acme.sh](https://github.com/acmesh-official/acme.sh) ukwenza izitifiketi.

I-acme.sh iyithuluzi lokusayina isitifiketi esizenzakalelayo somthombo ovulekile,

Faka i-warehouse ops.soft, sebenzisa `./ssl.sh` , futhi ifolda ye `conf` izokwakhiwa **ohlwini lwemibhalo olungaphezulu** .

Thola umhlinzeki wakho we-DNS kusuka [ku-acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , hlela `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Bese uqalisa `./ssl.sh 123.com` ukuze ukhiqize `123.com` kanye nezitifiketi ze `*.123.com` zegama lakho lesizinda.

Ukuqaliswa kokuqala kuzofaka ngokuzenzakalelayo [i-acme.sh](https://github.com/acmesh-official/acme.sh) futhi kwengeze umsebenzi ohleliwe wokuvuselela okuzenzakalelayo. Ungabona `crontab -l` , kunomugqa onjalo kanje.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Indlela yesitifiketi esikhiqiziwe ifana nokuthi `/mnt/www/.acme.sh/123.com_ecc。`

Ukuvuselelwa kwesitifiketi kuzobiza iskripthi `conf/reload/123.com.sh` , hlela lesi script, ungakwazi ukwengeza imiyalo efana `nginx -s reload` ukuze uvuselele inqolobane yesitifiketi yezinhlelo zokusebenza ezihlobene.

## Yakha iseva ye-SMTP nge-chasquid

[I-chasquid](https://github.com/albertito/chasquid) iwumthombo ovulekile weseva ye-SMTP ebhalwe ngolimi lwe-Go.

Njengengxenye yezinhlelo zeseva yemeyili yakudala njenge-Postfix ne-Sendmail, i-chasquid ilula futhi kulula ukuyisebenzisa, futhi kulula futhi ekuthuthukisweni kwesibili.

Run `./chasquid/init.sh 123.com` izofakwa ngokuzenzakalelayo ngokuchofoza okukodwa (shintshanisa okuthi 123.com ngegama lesizinda sakho esithumelayo).

## Lungiselela Isignesha ye-imeyili ye-DKIM

I-DKIM isetshenziselwa ukuthumela amasiginesha e-imeyili ukuze kuvinjelwe ukuthi izincwadi zingaphathwa njengogaxekile.

Ngemuva kokuthi umyalo usebenze ngempumelelo, uzocelwa ukuthi usethe irekhodi le-DKIM (njengoba kukhonjisiwe ngezansi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Vele wengeze irekhodi le-TXT ku-DNS yakho (njengoba kukhonjisiwe ngezansi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Buka isimo sesevisi namalogi

 `systemctl status chasquid` Buka isimo sesevisi.

Isimo sokusebenza okujwayelekile sikhonjiswe esithombeni esingezansi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` noma `journalctl -xeu chasquid` ingabuka ilogi yephutha.

## Hlehlisa ukucushwa kwegama lesizinda

Igama lesizinda eliphambene liwukuvumela ikheli le-IP ukuthi lixazululwe egameni lesizinda elihambisanayo.

Ukusetha igama lesizinda elihlehlayo kungavimbela ama-imeyili ukuthi abonakale njengogaxekile.

Lapho i-imeyili yamukelwe, iseva eyamukelayo izokwenza ukuhlaziywa kwegama lesizinda okuhlanekezelwe ekhelini le-IP leseva yokuthumela ukuze kuqinisekiswe ukuthi iseva ethumelayo inegama lesizinda elihlehla elivumelekile yini.

Uma iseva yokuthumela ingenalo igama lesizinda elihlehlayo noma uma igama lesizinda elihlehlayo lingafani nekheli le-IP leseva yokuthumela, iseva eyamukelayo ingase ibone i-imeyili njengogaxekile noma iyinqabe.

Vakashela [ku-https://my.contabo.com/rdns](https://my.contabo.com/rdns) futhi ulungiselele njengoba kukhonjisiwe ngezansi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Ngemuva kokusetha igama lesizinda elihlanekezelwe, khumbula ukulungisa ukulungiswa kwegama lesizinda ipv4 ne-ipv6 kuseva.

## Hlela igama lomethuleli we-chasquid.conf

Shintsha i- `conf/chasquid/chasquid.conf` ibe inani legama lesizinda elihlehlayo.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Bese usebenzisa `systemctl restart chasquid` ukuze uqale kabusha isevisi.

## Gcina i-conf ku-git repository

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Isibonelo, ngisekela ifolda ye-conf kunqubo yami ye-github kanje

Dala indawo yokugcina impahla yangasese kuqala

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Faka uhla lwemibhalo lwe-conf bese uluthumela ku-warehouse

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Engeza umthumeli

gijima

```
chasquid-util user-add i@wac.tax
```

Ingakwazi ukwengeza umthumeli

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Qinisekisa ukuthi iphasiwedi ihlelwe kahle

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Ngemva kokwengeza umsebenzisi, `chasquid/domains/wac.tax/users` izobuyekezwa, khumbula ukuyihambisa endaweni yokugcina impahla.

## I-DNS yengeza irekhodi le-SPF

I-SPF ( Uhlaka Lwenqubomgomo Yomthumeli) ubuchwepheshe bokuqinisekisa i-imeyili obusetshenziselwa ukuvimbela ukukhwabanisa kwe-imeyili.

Iqinisekisa ubunikazi bomthumeli wemeyili ngokubheka ukuthi ikheli lasesizindeni se-inthanethi lomthumeli lifana yini namarekhodi e-DNS egama lesizinda elizisho ukuthi liyilo, livimbela abakhwabanisi ukuthi bathumele ama-imeyili mbumbulu.

Ukwengeza amarekhodi e-SPF kungavimbela ama-imeyili ukuthi abonakale njengogaxekile ngangokunokwenzeka.

Uma iseva yegama lesizinda sakho ayisekeli uhlobo lwe-SPF, vele wengeze irekhodi lohlobo lwe-TXT.

Isibonelo, i-SPF `wac.tax` imi kanje

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

I-SPF `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Qaphela ukuthi ngifake `include:_spf.google.com` lapha, lokhu kungenxa yokuthi ngizomisa `i@wac.tax` njengekheli lokuthumela ebhokisini leposi le-Google kamuva.

## Ukucushwa kwe-DNS DMARC

I-DMARC isifinyezo se-(Ukuqinisekisa Umlayezo Osuselwe Esizinda, Ukubika Nokuhambisana).

Isetshenziselwa ukuthwebula ukubhampa kwe-SPF (mhlawumbe okubangelwa amaphutha okumisa, noma othile uzenza wena ukuze athumele ugaxekile).

Engeza irekhodi le-TXT `_dmarc` ,

Okuqukethwe kungokulandelayo

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Incazelo yepharamitha ngayinye imi kanje

### p (Inqubomgomo)

Ibonisa indlela yokusingatha ama-imeyili ahluleka ukuqinisekiswa kwe-SPF (Uhlaka Lwenqubomgomo Yomthumeli) noma i-DKIM (I-DomainKeys Identified Mail). Ipharamitha ye-p ingasethwa kwelinye lamanani amathathu:

* akukho: Asikho isenzo esithathwayo, umphumela wokuqinisekisa kuphela obuyiselwa kumthumeli ngohlelo lokubika lwe-imeyili.
* Ukuvalelwa: Faka imeyili engakadlulisi ukuqinisekiswa kufolda yogaxekile, kodwa ngeke yenqabe imeyili ngokuqondile.
* yenqaba: Wenqabe ngokuqondile ama-imeyili ahluleka ukuqinisekiswa.

### fo (Izinketho Zokwehluleka)

Icacisa inani lolwazi olubuyiswe indlela yokubika. Ingasethwa ibe yinye yamanani alandelayo:

* 0: Bika imiphumela yokuqinisekisa yayo yonke imilayezo
* 1: Bika kuphela imilayezo ehluleka ukuqinisekiswa
* d: Bika kuphela ukuhluleka kokuqinisekisa igama lesizinda
* s: bika kuphela ukuhluleka kokuqinisekisa kwe-SPF
* l: Bika kuphela ukuhluleka kokuqinisekisa kwe-DKIM

### ruf & ruf

* rua (I-URI yokubika yemibiko Ehlanganisiwe): Ikheli le-imeyili lokuthola imibiko ehlanganisiwe
* ruf (Ukubika i-URI yemibiko ye-Forensic): ikheli le-imeyili ukuze uthole imibiko enemininingwane

## Engeza amarekhodi e-MX ukuze uthumele ama-imeyili ku-Google Mail

Ngenxa yokuthi angikwazanga ukuthola ibhokisi leposi lamahhala lebhizinisi elisekela amakheli omhlaba wonke (Catch-All, ingathola noma yimaphi ama-imeyili athunyelwe kuleli gama lesizinda, ngaphandle kwemingcele yeziqalo), ngisebenzise i-chasquid ukudlulisela wonke ama-imeyili ebhokisini lami leposi le-Gmail.

**Uma unebhokisi lakho leposi lebhizinisi elikhokhelwayo, sicela ungayishintshi i-MX bese weqa lesi sinyathelo.**

Hlela i- `conf/chasquid/domains/wac.tax/aliases` , setha ibhokisi leposi lokudlulisela phambili

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` ikhombisa wonke ama-imeyili, `i` sekheli le-imeyili somsebenzisi othumelayo esidalwe ngenhla. Ukuze udlulisele imeyili, umsebenzisi ngamunye udinga ukwengeza umugqa.

Bese wengeza irekhodi le-MX (ngikhomba ngqo ekhelini legama lesizinda eliphambene lapha, njengoba kuboniswe emgqeni wokuqala emfanekisweni ongezansi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Ngemva kokuba ukulungiselelwa sekuqediwe, ungasebenzisa amanye amakheli e-imeyili ukuze uthumele ama-imeyili `i@wac.tax` `any123@wac.tax` ukuze ubone ukuthi ungawathola yini ama-imeyili ku-Gmail.

Uma kungenjalo, hlola i-chasquid log ( `grep chasquid /var/log/syslog` ).

## Thumela i-imeyili ku-i@wac.tax nge-Google Mail

Ngemuva kokuthi i-Google Mail ithole i-imeyili, ngiye ngathemba ukuphendula ngokuthi `i@wac.tax` esikhundleni sokuthi i.wac.tax@gmail.com.

Vakashela ku [-https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) bese uchofoza okuthi "Engeza elinye ikheli le-imeyili".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Bese, faka ikhodi yokuqinisekisa etholwe yi-imeyili ethunyelwe kuyo.

Ekugcineni, ingasethwa njengekheli lomthumeli elizenzakalelayo (kanye nenketho yokuphendula ngekheli elifanayo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Ngale ndlela, sesiqedile ukusungulwa kweseva yemeyili ye-SMTP futhi ngesikhathi esifanayo sisebenzisa i-Google Mail ukuthumela nokwamukela ama-imeyili.

## Thumela i-imeyili yokuhlola ukuze uhlole ukuthi ukucupha kuphumelele yini

Faka i- `ops/chasquid`

Run `direnv allow` ukufaka okuncikile (i-direnv ifakiwe kunqubo yokuqalisa yokhiye owodwa futhi ihhuku yengezwe kugobolondo)

bese ugijima

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Incazelo yamapharamitha imi kanje

* umsebenzisi: igama lomsebenzisi le-SMTP
* pass: SMTP iphasiwedi
* ku: umamukeli

Ungathumela i-imeyili yokuhlola.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Kunconywa ukusebenzisa i-Gmail ukuze uthole ama-imeyili okuhlola ukuze uhlole ukuthi ukulungiselelwa kuyaphumelela yini.

### Ukubethela okujwayelekile kwe-TLS

Njengoba kukhonjisiwe esithombeni esingezansi, kukhona lesi sikhiya esincane, okusho ukuthi isitifiketi se-SSL sinikwe amandla ngempumelelo.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Bese uchofoza okuthi "Bonisa I-imeyili Yangempela"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### I-DKIM

Njengoba kukhonjisiwe esithombeni esingezansi, ikhasi le-imeyili lokuqala le-Gmail libonisa i-DKIM, okusho ukuthi ukucushwa kwe-DKIM kuphumelele.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Hlola okuthi Thola kunhlokweni ye-imeyili yoqobo, futhi ungabona ukuthi ikheli lomthumeli lithi IPV6, okusho ukuthi i-IPV6 nayo ilungiselelwe ngempumelelo.
