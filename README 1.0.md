# คำอธิบายโปรแกรม mmdpaimaya

## ความสามารถ
โค้ดถูกเขียนขึ้นเพื่อใช้นำเข้าโมเดล MMD จากไฟล์ .pmd และ .pmx เข้ามาใส่ในโปรแกรม Autodesk Maya



## ส่วนประกอบของโปรแกรม
ไฟล์ที่แจกประกอบด้วย ๕ โฟลเดอร์

ในจำนวนนั้น ๔ โฟลเดอร์คือมอดูลเสริมที่จำเป็นต้องใช้ซึ่งยืมมาใช้เพื่อเป็นส่วนประกอบในโปรแกรม ไม่ได้เป็นส่วนที่เขียนขึ้นเองแต่อย่างใด ได้แก่
- pymeshio สำหรับเปิดอ่านข้อมูลจากไฟล์ .pmd และ .pmx
- pykakasi สำหรับแปลงภาษาญี่ปุ่นเป็นโรมาจิ ([รายละเอียด](http://phyblas.blog.jp/20170124.html))
- jctconv สำหรับแปลงอักษรคาตาคานะครึ่งตัวเป็นเต็มตัว ([รายละเอียด](http://phyblas.blog.jp/20170202.html))
- pkg_resources ถูกเรียกใช้โดย pykakasi

ส่วนโฟลเดอร์ mmdpaimaya คือส่วนของโค้ดที่เขียนขึ้นมาเอง



## เวอร์ชันของมายาที่ใช้
โค้ดนี้ถูกทดสอบแล้วว่าใช้งานได้ในมายา 2015,2016,2017 ภายใน windows และ mac



## การเตรียมการก่อนใช้งาน
ให้นำโฟลเดอร์ทั้ง ๕ ไปไว้ในโฟลเดอร์สำหรับใส่สคริปต์ไพธอนในมายา

โฟลเดอร์ที่ว่านั้นมีชื่อว่า scripts ซึ่งตำแหน่งที่อยู่จะต่างกันไปตามเวอร์ชันและระบบปฏิบัติการ รายละเอียดได้อธิบายไว้ในนี้ http://phyblas.blog.jp/maso05.html

ไฟล์หรือโฟลเดอร์ที่ถูกนำไปวางไว้ในนั้นจะสามารถถูกเรียกใช้จากโปรแกรมมายาในฐานะเป็นมอดูลได้



## การใช้งาน
เมื่อจะใช้งานให้นำเอาโค้ดที่อยู่ในไฟล์ roem.py มารันในสคริปต์อีดิเตอร์ในมายา

หรือก็คือแค่พิมพ์ตามนี้ในสคริปต์อีดิเตอร์แล้วกดรัน

```python
import natang
natang_sang = natang.roem()
```

หรือหากต้องการให้ใช้งานสะดวกขึ้นอีกก็ให้นำโค้ดไปเซฟใส่เชลฟ์ไว้เลย ทุกครั้งที่ต้องการใช้ก็แค่กดปุ่ม

วิธีการตามที่เขียนไว้ใน http://phyblas.blog.jp/maso29.html



หากโค้ดใช้งานได้ไม่มีปัญหาอะไรก็จะมีหน้าต่างขึ้นมาดังนี้

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d01.jpg)

เมื่อเริ่มหน้าต่างโปรแกรมขึ้นมาจะเห็นว่ามีช่องให้เลือกไฟล์อยู่ด้านบนสุด และมีอะไรให้เลือกปรับแต่งหลายอย่าง

ค่าต่างๆเหล่านี้ค่าตั้งต้นจะดึงมาจากไฟล์ khatangton.txt ในโฟลเดอร์เดียวกับกับโค้ด ทุกครั้งที่กดสร้างโมเดลไปค่าจะถูกบันทึกเอาไว้ทำให้ค่าเหมือนกับที่ใช้ล่าสุดทุกครั้ง

แต่หากทำไฟล์ khatangton.txt หายไป หรือมีข้อผิดพลาดทำให้อ่านไม่ได้ขึ้นมา ไฟล์จะถูกสร้างขึ้นมาใหม่เอง

ชื่อของโหนดต่างๆจะถูกตั้งโดยดึงชื่อจากในโมเดลเดิม โดยหากชื่อไหนที่เป็นภาษาญี่ปุ่นจะถูกแปลงเป็นโรมาจิโดย pykakasi อาจมีได้ชื่อแปลกๆไม่ถูกต้องอยู่บ้าง แต่ไม่มีวิธีอื่นเพราะชื่อโหนดในมายาถูกบังคับให้ใช้อักษรโรมัน ๒๖ ตัวและ _ เท่านั้น

เมื่อสร้างเสร็จโดยไม่มีข้อผิดพลาดอะไรหน้าต่างก็จะถูกปิด แล้วโมเดลก็จะมาปรากฏตัวในฉาก



## ปรับขนาดโมเดล
ช่องปรับแต่งอันแรกสุดและเป็นอันเดียวที่ให้พิมพ์ค่าก็คือส่วนของขนาด หน่วยของขนาดจะเป็นจำนวนเท่าของขนาดเดิม

โดยทั่วไปแล้วขนาดมาตรฐานของโมเดลใน MMD จะเป็นขนาดที่ให้มิกุมีความสูง ๒๐ หน่วย แต่ส่วนสูงจริงๆของมิกุคือ ๑๕๘ ซม. หรือก็คือประมาณ ๑๖๐ ซม.

นั่นหมายความว่าหากในมายาเราจะใช้สัดส่วนเป็น ซม. ก็ควรจะใส่ขนาดเป็น 8 และหากจะใช้เป็นเมตรก็ควรใส่เป็น 0.08 เป็นต้น

เทียบขนาด 8x|1x|0.08x

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d02.jpg)

([Tda式初音ミク デフォ服ver](https://bowlroll.net/file/16344))

โมเดลที่มีการสร้างกระดูกไว้จะปรับขนาดในภายหลังได้ลำบาก ดังนั้นควรเลือกขนาดให้ถูกต้องตั้งแต่แรก



## แยกโพลิกอนตามวัสดุ
ส่วนช่องที่ให้ติ๊กว่าจะแยกโพลิกอนตามวัสดุหรือไม่นั้นมีไว้สำหรับโมเดลที่เป็นพวกเครื่องประดับหรือฉาก เพราะพวกฉากต่างๆเช่นพวกเมืองหรือห้องมักจะประกอบไปด้วยสิ่งของต่างๆมารวมอยู่ด้วยกัน บางทีเราอาจต้องการแยกแต่ละอย่างออกจากกัน หรืออยากลบบางส่วนออก

แต่ว่าโมเดลใน MMD มักใส่โพลิกอนทั้งหมดในโมเดลรวมกันหมดไม่ได้แยก ทำให้การจะแยกสิ่งของแต่ละอย่างออกจากกันนั้นค่อนข้างลำบาก

วิธีที่ดูจะง่ายที่สุดในการแยกก็คือแยกตามวัสดุ เพราะสิ่งของคนละส่วนมักใช้วัสดุคนละอย่างกันอยู่แล้ว เพียงแต่ว่าก็เป็นแค่การแบ่งคร่าวๆเท่านั้น ยังไงก็ต้องมาปรับดูอีกที ถึงอย่างนั้นการแยกเอาไว้ก่อนก็ช่วยให้คัดกรองส่วนประกอบง่ายขึ้นมาก

หากติ๊กว่าจะแยกโพลิกอนแล้วจะไม่สามารถสร้าง blend shape และกระดูกได้ เพราะมันไม่สามารถทำได้อยู่แล้ว ดังนั้นการแยกโพลิกอนจึงใช้กับเฉพาะฉากหรือเครื่องประดับที่อยู่นิ่ง ไม่ใช้กับตัวละครที่ต้องการเคลื่อนไหว

โพลิกอนที่แยกออกมาจะเป็นคนละโหนดกันแต่จะถูกรวมเป็นกลุ่มเดียว

ตัวอย่าง ดาบในภาพนี้สามารถแยกโพลิกอนส่วนที่เป็นตัวดาบกับปลอกดาบออกมาจากกันได้อย่างง่ายดาย

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d08.jpg)

([法の剣](http://seiga.nicovideo.jp/seiga/im3129714))



## สร้าง blend shape
เบลนด์เชปคือส่วนที่ทำให้เกิดการขยับเปลี่ยนแปลงเล็กๆน้อยๆบนผิวโมเดล ส่วนใหญ่จะใช้กับการแสดงใบหน้า แต่ก็มีใช้กับอย่างอื่นด้วย

สำหรับใน MMD จะเรียกว่ามอร์ฟ (morph) ซึ่งที่จริงแล้วมอร์ฟยังครอบคลุมความสามารถหลายอย่างเช่นการเปลี่ยนแปลงสีหรือความโปร่งใสในวัสดุของผิวด้วย

แต่ว่าเบลนด์เชปในมายาไม่ได้รองรับการเปลี่ยนแปลงของวัสดุ ดังนั้นจึงสามารถแปลงเฉพาะมอร์ฟที่เป็นการขยับจุดเท่านั้น

กรณีโมเดลมีมอร์ฟที่ไม่สามารถแปลงได้จะมีข้อความเตือนขึ้นมาเพื่อให้รู้

สามารถดูและควบคุมเบลนด์เชปได้ใน

\> Windows (ウィンドウ)
\> Animation Editor (アニメーション エディタ)
\> Blend Shape (ブレンド シェイプ)

ตัวอย่าง ปรับปากและตากับคิ้วให้มิกุยิ้มได้

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d03.jpg)

([ゆきはね式ミク　イージスβ2](https://bowlroll.net/file/12207))



## สร้างกระดูกและ IK
สำหรับโมเดลที่เป็นตัวละครจำเป็นจะต้องมีกระดูกเพื่อใช้ในการเคลื่อนไหวร่างกาย

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d04.jpg)

([Racing Miku 2015](http://digitrevx.deviantart.com/art/Princess-Knight-Racing-Miku-2015-MMD-530215264))

กระดูกทั้งหมดจะถูกสร้างตามข้อมูลของกระดูกทั้งหมดที่มีในโมเดล แม้แต่กระดูกที่ไม่สามารถควบคุมได้โดยตรงตอนอยู่ในโปรแกรม MMD ด้วย เช่นพวกเส้นผมและกระโปรง

ใน MMD นั้นเส้นผมและกระโปรงถูกควบคุมด้วยฟิสิกส์เพื่อให้เคลื่อนที่พริ้วไหวไปเอง แต่ความสามารถในส่วนนั้นไม่ได้ถูกดึงมาใช้ในนี้ ดังนั้นหากต้องการให้ขยับก็ต้องมาควบคุมกระดูกตรงนี้เอง

ช่องที่ติ๊กให้สร้าง IK นั้นยังไม่สมบูรณ์และไม่แนะนำให้ใช้เท่าไหร่ เพียงแต่ว่าได้พยายามสร้างเอาไว้แล้วก็เลยเสียดายที่จะลบทิ้งเท่านั้น ใครจะลองใช้ดูก็ได้

ที่จริงการดึง IK จากข้อมูลโมเดล MMD เดิมนั้นอาจไม่ค่อยจำเป็นสักเท่าไหร่นัก เพราะในมายามีคำสั่งที่ใช้การได้ดีมากอย่างหนึ่ง นั่นคือ HumanIK เป็นคำสั่งที่เอาไว้ควบคุมตัวละครที่มีลักษณะเป็นมนุษย์โดยสร้าง IK ที่จำเป็นขึ้นมาโดยอัตโนมัติ

ในที่นี้จะไม่อธิบายรายละเอียดเกี่ยวกับ HumanIK เพราะมีรายละเอียดค่อนข้างมาก อาจลองไปศึกษาดูเองได้ แต่ในตัวโปรแกรมได้แนบไฟล์แม่แบบ mmdhik.xml ที่ใส่ชื่อของข้อต่อต่างๆที่ถูกแปลงเป็นโรมาจิในโปรแกรมนี้เอาไว้ สามารถใช้ได้



## ใส่สีผิว
ตัวเลือกใส่สีผิวถ้าเลือกว่าใส่ก็จะดึงข้อมูลวัสดุของโมเดลมาใช้ โดยสร้างโหนดของวัสดุและเท็กซ์เจอร์ขึ้นมา

กรณีที่เลือกไม่ใส่สีผิวก็จะได้โมเดลที่ใส่สีมาตรฐานให้ทั้งตัว ดูแล้วอาจคล้ายรูปปั้นหิน

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d05.jpg)

([Animasa X Pikadude 初音ミク](http://seiga.nicovideo.jp/seiga/im4222520))

อนึ่ง หากเลือกว่าจะแยกโพลิกอนตามวัสดุ สีผิวจะถูกบังคับใส่โดยอัตโนมัติ เพราะถ้าไม่ใส่วัสดุก็ไม่มีทางแยกโพลิกอนตามวัสดุได้อยู่แล้ว

วัสดุที่นำมาใช้จะไม่ได้ดึงเอาความสามารถของสเฟียร์แม็ป (sphere map) มาใส่ด้วย

สเฟียร์แม็ป คือไฟล์เท็กซ์เจอร์ชนิด .spd .spa ซึ่งใช้คูณหรือบวกเข้ากับเท็กซ์เจอร์พื้นฐาน มักใช้เพื่อทำให้วัสดุเกิดความมันวาว

เนื่องจากยังไม่พบวิธีที่จะนำมาใช้ในมายาได้ จึงทำให้วัสดุที่ใช้เท็กซ์เหล่านี้อาจแสดงผลสีแปลกออกไปดูไม่สมบูรณ์แบบ



## การปรับ alpha map
ค่าอัลฟาคือค่าความโปร่งใสของแต่ละจุดในภาพ โดยทั่วไปไฟล์บางชนิดเช่น bmp หรือ png จะมีค่าอัลฟาอยู่ด้วยนอกเหนือไปจากค่าสี

หากเลือกว่าจะทำอัลฟาแม็ป โปรแกรมจะหาดูว่ามีวัสดุที่อาจต้องทำอัลฟาแม็ปอยู่หรือไม่ หากทำได้ก็จะทำ

ตัวอย่าง เช่นโมเดลอันนี้ เทียบภาพระหว่างทำอัลฟาแม็ปกับไม่ได้ทำ

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d06.jpg)

([初音オミク２回目修正版](https://bowlroll.net/file/18038))

แต่ก็มีโมเดลบางตัวที่ทำอัลฟาแม็ปเฉพาะวัสดุบางอัน หากทำอัลฟาแม็ปให้กับวัสดุที่ไม่ครวรจะต้องทำก็จะทำให้เกิดการแสดงผลแปลกๆ

ตอนนี้ยังหาวิธีเขียนโปรแกรมให้ช่วยแยกแยะว่าอันไหนควรหรือไม่ควรทำไม่ได้ ทำให้ต้องมาดูแล้วคัดเอาเองว่าวัสดุไหนควรทำ

ในเบื้องต้นโปรแกรมจะทำการเชื่อมอัลฟาแม็ปให้กับทุกวัสดุที่ทำได้ จากนั้นก็ค่อยมาคัดกรองดูว่าอันไหนควรทำ

โปรแกรมนี้ได้ทำระบบเพื่อให้สะดวกในการคัดกรองว่าวัสดุไหนควรจะใส่อัลฟาแม็ป โดยเมื่อนำเข้าโมเดลขึ้นมาเสร็จจะมีขึ้นหน้าต่างให้ติ๊กเลือก

![](http://i271.photobucket.com/albums/jj153/phyblas/yami/2017/d07.jpg)

([มิกุ TDA ในชุดจีนโดย kooooi](http://kooooi.deviantart.com/gallery/))

เมื่อติ๊กเครื่องหมายถูกออกอัลฟาแม็ปก็จะถูกเอาออกทันที สามารถสังเกตเห็นความเปลี่ยนแปลงได้ทันที ถ้ารู้สึกว่าเอาออกแล้วแปลกก็ติ๊กใหม่ อัลฟาแม็ปจะกลับมา

ลองไล่ดูไปให้ครบทุกอันแล้วก็กดเสร็จสิ้นหรือกดปิด หน้าต่างก็จะหายไป เป็นอันเสร็จ

เพื่อความสะดวกเพื่อจะได้ไม่ต้องมาคอยทำแบบนี้ทุกครั้งที่นำเข้าโมเดลอันเดิม จึงได้ทำโปรแกรมให้มีการบันทึกค่าการเลือกเอาไว้ด้วย

โดยที่หากกดปุ่ม "เสร็จสิ้น" ข้อมูลการเลือกอัลฟาแม็ปของโมเดลนั้นก็จะถูกบันทึกไว้ พอใช้โปรแกรมนี้นำเข้าโมเดลเดิมอีกครั้งก็จะถูกเลือกให้โดยอัตโนมัติ

ข้อมูลการเลือกอัลฟาแม็ปจะถูกเก็บอยู่ในไฟล์ชื่อ model_alpha.txt ซึ่งจะถูกสร้างขึ้นอัตโนมัติหลังการใช้งานครั้งแรก และยิ่งใช้ไปก็จะยิ่งบันทึกข้อมูลการเลือกอัลฟาแม็ปของโมเดลต่างๆไว้มากขึ้น หากอยากจะลบทิ้งก็เปิดไฟล์นี้มาดูได้

แต่หากแก้แล้วมีข้อผิดพลาดอะไรจนทำให้การอ่านไฟล์เกิดขัดข้องขึ้นมามันจะทำลายตัวเองแล้วสร้างขึ้นใหม่ ข้อมูลการเลือกที่เคยบันทึกไว้ก็หายหมด

ในอนาคตหากมีเวลาปรับปรุงโปรแกรมเพิ่มเติมและคิดวิธีที่ดีกว่าได้ก็คงจะตัดส่วนนี้ทิ้งไป



## ส่วนที่ไม่สมบูรณ์
ดังที่ได้กล่าวไปบ้างแล้วข้างต้น ความสามารถบางส่วนจาก MMD ยังไม่สามารถดึงเข้ามาใช้ในมายาได้ทั้งหมด หากมีเวลาอาจพยายามปรับปรุงต่อไป

ตัวอย่างข้อบกพร่องที่ยังควรปรับปรุง เช่น
- ไม่สามารถใส่ฟิสิกส์ การขยับของเส้นผมและกระโปรงยังต้องปรับเอง
- ไม่สามารถใส่สเฟียร์แม็ป ส่วนที่ทำให้วัสดุดูมันวาว
- เบลนด์เชปไม่ได้ทำมอร์ฟอื่นๆที่ไม่ใช่มอร์ฟขยับจุด
- กระดูกบางส่วนขยับแล้วยังมีอาการแปลกๆ
- ไฟล์เท็กซ์เจอร์บางชนิดที่ใช้ใน MMD ไม่สามารถใช้ในมายา หรือใช้แล้วไม่สมบูรณ์ ทำให้สีอาจดูผิดเพี้ยนไปได้
- รองรับเฉพาะไฟล์ .pmd และ .pmx หากต้องการนำเข้าไฟล์ .x ให้ใช้โปรแกรมเช่น pmxeditor แปลงเป็น pmx ก่อน
- ฯลฯ



## ขอขอบคุณ
โค้ดโปรแกรมนี้ถูกเขียนโดยได้แรงบันดาลใจและแนวคิดมาจาก
- [PmxIO ของคุณ Yomogi](http://mayatech.blog.jp/archives/3009881.html)
- [mmd-transporter ของคุณ GRGSIBERIA](http://www.nicovideo.jp/watch/sm23644737)



## ตัวอย่างงานที่ใช้โมเดล MMD ในมายา
- https://www.youtube.com/watch?v=7iixZmr8rAo
- http://phyblas.blog.jp/20170217.html
- https://www.facebook.com/1081618448523592



## ติดต่อสอบถาม
หากมีปัญหาสงสัยถามได้ในเพจที่ facebook https://www.facebook.com/ikamiso