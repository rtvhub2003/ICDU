[At the very beginning]
* Using USB2TTL debugger, connect from G2L board, and proceed with step1.

[Step1]
cmd: sudo minicom

Note: If unable to enter in minicom terminal, plug-out, plug-in USB2TTL or check your connections

[Step2]
* Power the ICDU, and note the boot logs in minicom terminal
* If not getting boot logs, go back to step1

[Step3]
* Once ICDU is completely started, it will ask to log in minicom terminal
* user: root
* no password

[Step4]
* Connect with LAN cable, and check ip address
cmd: ifconfig

[Step5]
* Set temporary ip address
cmd: ifconfig eth0 192.168.3.x netmask 255.255.248.0
e.g, ifconfig eth0 192.168.3.25 netmask 255.255.248.0

* Then check, if ip is assigned to your device
cmd: ifconfig

[Step6]
* ping from your laptop
* open terminal and execute below command
cmd: ping 192.168.3.25

[Step7]
* Programming ICDU:
* Visit inside root folder in your laptop and execute below command

cmd: chmod a+x program_icdu.sh
cmd: ./program_icdu.sh 192.168.3.25

* Wait until ICDU is programmed! It'll take a few minutes [5 minutes]
* After restart, follow step8.

[Step8]
* Set temporary ip address
cmd: ifconfig eth0 192.168.3.x netmask 255.255.248.0
e.g, ifconfig eth0 192.168.3.25 netmask 255.255.248.0


* Transfer Kernels and DTB files to ICDU
cmd: mount /dev/mmcblk0p1 /media/
cmd: cd /media/
cmd: ls

Output: Image-r9a07g044l2-smarc.dtb	 Image-smarc-rzg2l.bin

* Rename these files
cmd: mv Image-r9a07g044l2-smarc.dtb Image-r9a07g044l2-smarc.dtb.old
cmd: mv Image-smarc-rzg2l.bin Image-smarc-rzg2l.bin.old
cmd: ls

Output: Image-r9a07g044l2-smarc.dtb.old  Image-smarc-rzg2l.bin.old

* Transfer files
* visit inside 'icduos_dtb' folder in your laptop and perform below commands
cmd: scp -r Image-* root@192.168.3.25:/media/

* Once done, execute below command in your laptop
cmd: cd /media/
cmd: ls

Output: 
Image-r9a07g044l2-smarc.dtb	 Image-smarc-rzg2l.bin
Image-r9a07g044l2-smarc.dtb.old  Image-smarc-rzg2l.bin.old

cmd: umount /dev/mmcblk0p1
cmd: ls
Output: <nothing>

[Step9]
* Start your system
cmd: reboot

* Wait for a few seconds to start ICDU and launch "Indian Railways Welcomes You" slogan on the screen.
* Once got, proceed with step10

[Step10]
* From your laptop, execute below command
cmd: echo "CMD|INIT|END" | nc -u -w1 -q1 192.168.3.25 45454
cmd: echo 'CMD|ROUTE|{"data":{"st_list":[{"dist_km":0,"rl1":"PUNJABI","rl2":"HINDI","st_code":"SHC","st_name_en":"SAHARSA JUNCTION","st_name_hi":"सहरसा जंक्शन","st_name_rl1":"ਸਹਰਸਾ ਜੰਕਸ਼ਨ","st_name_rl2":"सहरसा जंक्शन","st_no":1},{"dist_km":16,"rl1":"PUNJABI","rl2":"HINDI","st_code":"SBV","st_name_en":"SIMRI BAKHTIYARPUR","st_name_hi":"सिमरी बख्तियारपुर","st_name_rl1":"ਸਿਮਰੀ ਬਖਤਿਆਰਪੁਰ","st_name_rl2":"सिमरी बख्तियारपुर","st_no":2},{"dist_km":51,"rl1":"PUNJABI","rl2":"HINDI","st_code":"KGG","st_name_en":"KHAGARIA JUNCTION","st_name_hi":"खगड़िया जंक्शन","st_name_rl1":"ਖਗੜੀਆ ਜੰਕਸ਼ਨ","st_name_rl2":"खगड़िया जंक्शन","st_no":3},{"dist_km":91,"rl1":"PUNJABI","rl2":"HINDI","st_code":"BGS","st_name_en":"BEGUSARAI JUNCTION","st_name_hi":"बेगूसराय जंक्शन","st_name_rl1":"ਬੇਗੂਸਰਾਏ ਜੰਕਸ਼ਨ","st_name_rl2":"बेगूसराय जंक्शन","st_no":4},{"dist_km":106,"rl1":"PUNJABI","rl2":"HINDI","st_code":"BJU","st_name_en":"BARAUNI JUNCTION","st_name_hi":"बरौनी जंक्शन","st_name_rl1":"ਬਰੌਨੀ ਜੰਕਸ਼ਨ","st_name_rl2":"बरौनी जंक्शन","st_no":5},{"dist_km":134,"rl1":"PUNJABI","rl2":"HINDI","st_code":"DSS","st_name_en":"DALSINGH SARAI","st_name_hi":"दलसिंह सराय","st_name_rl1":"ਦਲਸਿੰਘ ਸਰਾਏ","st_name_rl2":"दलसिंह सराय","st_no":6},{"dist_km":157,"rl1":"PUNJABI","rl2":"HINDI","st_code":"SPJ","st_name_en":"SAMASTIPUR JUNCTION","st_name_hi":"समस्तीपुर जंक्शन","st_name_rl1":"ਸਮਸਤੀਪੁਰ ਜੰਕਸ਼ਨ","st_name_rl2":"समस्तीपुर जंक्शन","st_no":7},{"dist_km":209,"rl1":"PUNJABI","rl2":"HINDI","st_code":"MFP","st_name_en":"MUZAFFARPUR JUNCTION","st_name_hi":"मुजफ्फरपुर जंक्शन","st_name_rl1":"ਮੁਜ਼ੱਫਰਪੁਰ ਜੰਕਸ਼ਨ","st_name_rl2":"मुजफ्फरपुर जंक्शन","st_no":8},{"dist_km":263,"rl1":"PUNJABI","rl2":"HINDI","st_code":"MFP","st_name_en":"HAJIPUR JUNCTION","st_name_hi":"हाजीपुर जंक्शन","st_name_rl1":"ਹਾਜੀਪੁਰ ਜੰਕਸ਼ਨ","st_name_rl2":"हाजीपुर जंक्शन","st_no":9},{"dist_km":322,"rl1":"PUNJABI","rl2":"HINDI","st_code":"CPR","st_name_en":"CHHAPRA JUNCTION","st_name_hi":"छपरा जंक्शन","st_name_rl1":"ਛਪਰਾ ਜੰਕਸ਼ਨ","st_name_rl2":"छपरा जंक्शन","st_no":10},{"dist_km":383,"rl1":"PUNJABI","rl2":"HINDI","st_code":"SV","st_name_en":"SIWAN JUNCTION","st_name_hi":"सिवान जंक्शन","st_name_rl1":"ਸੀਵਾਨ ਜੰਕਸ਼ਨ","st_name_rl2":"सिवान जंक्शन","st_no":11},{"dist_km":453,"rl1":"PUNJABI","rl2":"HINDI","st_code":"DEOS","st_name_en":"DEORIA SADAR","st_name_hi":"देवरिया सदर","st_name_rl1":"ਦੇਵਰੀਆ ਸਦਰ","st_name_rl2":"देवरिया सदर","st_no":12},{"dist_km":502,"rl1":"PUNJABI","rl2":"HINDI","st_code":"GKP","st_name_en":"GORAKHPUR JUNCTION","st_name_hi":"गोरखपुर जंक्शन","st_name_rl1":"ਗੋਰਖਪੁਰ ਜੰਕਸ਼ਨ","st_name_rl2":"गोरखपुर जंक्शन","st_no":13},{"dist_km":772,"rl1":"PUNJABI","rl2":"HINDI","st_code":"LKO","st_name_en":"LUCKNOW CHARBAGH NR","st_name_hi":"लखनऊ चारबाग एनआर","st_name_rl1":"ਲਖਨਊ ਚਾਰਬਾਗ ਐਨ.ਆਰ","st_name_rl2":"लखनऊ चारबाग एनआर","st_no":14},{"dist_km":873,"rl1":"PUNJABI","rl2":"HINDI","st_code":"HRI","st_name_en":"HARDOI","st_name_hi":"हरदोई","st_name_rl1":"ਹਰਦੋਈ","st_name_rl2":"हरदोई","st_no":15},{"dist_km":1006,"rl1":"PUNJABI","rl2":"HINDI","st_code":"BE","st_name_en":"BEREILLY JUNCTION","st_name_hi":"बरेली जंक्शन","st_name_rl1":"ਬਰੇਲੀ ਜੰਕਸ਼ਨ","st_name_rl2":"बरेली जंक्शन","st_no":16},{"dist_km":1097,"rl1":"PUNJABI","rl2":"HINDI","st_code":"MB","st_name_en":"MORADABAD JUNCTION","st_name_hi":"मुरादाबाद जंक्शन","st_name_rl1":"ਮੁਰਾਦਾਬਾਦ ਜੰਕਸ਼ਨ","st_name_rl2":"मुरादाबाद जंक्शन","st_no":17},{"dist_km":1201,"rl1":"PUNJABI","rl2":"HINDI","st_code":"HPU","st_name_en":"HAPUR JUNCTION","st_name_hi":"हापुड़ जंक्शन","st_name_rl1":"ਹਾਪੁੜ ਜੰਕਸ਼ਨ","st_name_rl2":"हापुड़ जंक्शन","st_no":18},{"dist_km":1262,"rl1":"PUNJABI","rl2":"HINDI","st_code":"NDLS","st_name_en":"NEW DELHI","st_name_hi":"नई दिल्ली","st_name_rl1":"ਨਵੀਂ ਦਿੱਲੀ","st_name_rl2":"नई दिल्ली","st_no":19},{"dist_km":1461,"rl1":"PUNJABI","rl2":"HINDI","st_code":"UMB","st_name_en":"AMBALA CANTT JUNCTION","st_name_hi":"अंबाला कैंट जंक्शन","st_name_rl1":"ਅੰਬਾਲਾ ਕੈਂਟ ਜੰਕਸ਼ਨ","st_name_rl2":"अंबाला कैंट जंक्शन","st_no":20},{"dist_km":1575,"rl1":"PUNJABI","rl2":"HINDI","st_code":"LDH","st_name_en":"LUDHIANA JUNCTION","st_name_hi":"लुधियाना जंक्शन","st_name_rl1":"ਲੁਧਿਆਣਾ ਜੰਕਸ਼ਨ","st_name_rl2":"लुधियाना जंक्शन","st_no":21},{"dist_km":1611,"rl1":"PUNJABI","rl2":"HINDI","st_code":"PGW","st_name_en":"PHAGWARA JUNCTION","st_name_hi":"फगवाड़ा जंक्शन","st_name_rl1":"ਫਗਵਾੜਾ ਜੰਕਸ਼ਨ","st_name_rl2":"फगवाड़ा जंक्शन","st_no":22},{"dist_km":1632,"rl1":"PUNJABI","rl2":"HINDI","st_code":"JUC","st_name_en":"JALANDHAR CITY JUNCTION","st_name_hi":"जालंधर सिटी जंक्शन","st_name_rl1":"ਜਲੰਧਰ ਸਿਟੀ ਜੰਕਸ਼ਨ","st_name_rl2":"जालंधर सिटी जंक्शन","st_no":23},{"dist_km":1668,"rl1":"PUNJABI","rl2":"HINDI","st_code":"BEAS","st_name_en":"BEAS JUNCTION","st_name_hi":"ब्यास जंक्शन","st_name_rl1":"ਬਿਆਸ ਜੰਕਸ਼ਨ","st_name_rl2":"ब्यास जंक्शन","st_no":24},{"dist_km":1711,"rl1":"PUNJABI","rl2":"HINDI","st_code":"ASR","st_name_en":"AMRITSAR JUNCTION","st_name_hi":"अमृतसर जंक्शन","st_name_rl1":"ਅੰਮ੍ਰਿਤਸਰ ਜੰਕਸ਼ਨ","st_name_rl2":"अमृतसर जंक्शन","st_no":25}]},"info":{"route":{"tr_nm_en":"AMRITSAR GARIB RATH EXPRESS अमृतसर गरीब रथ एक्सप्रेस ਅੰਮ੍ਰਿਤਸਰ ਗਰੀਬ ਰਥ ਐਕਸਪ੍ਰੈਸ अमृतसर गरीब रथ एक्सप्रेस","tr_no_en":"12203","tr_route_en":"SAHARSA TO AMRITSAR JUNCTION","tr_via_en":"VIA GORAKHPUR JUNCTION"}}}|END' | nc -u -w1 -q1 192.168.3.25 45454
Output: Station names and train moving animation (DRM) will be displayed on the screen. If not, there is something wrong. Ask for help!
* If DRM is visible, proceed with the next commands

cmd: echo "CMD|SLG|THIS IS A LONG SLOGAN FOR TESTING MARQUEE,HINDI,#FFFF00|END" | nc -u -w1 -q1 192.168.3.25 45454
Output: A long slogan will start scrolling from right2left. If not, seek help or debug.

cmd: echo "CMD|VIDEO|ad_video1.mp4|END" | nc -u -w1 192.168.3.25 45454
Output: A video will get played on the right of the screen along with DRM and slogans

[Step11]
* Perform step10, 2-3 times, to verify that ICDU is completely programmed and working fine.
* If feels uneasy or stuck somewhere, ask for support!

Thanks!




