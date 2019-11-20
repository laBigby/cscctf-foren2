Forensic - DUARRR!!<br>
Indonesia telah memasuki tahun 2027, ASEAN telah membentuk kesepakatan untuk melakukan pengawasan ketat terhadap peredaran memes karena diduga merusak kejiwaan pemuda pemudi negara asia<br>
Kamu diberikan arahan untuk menginvestigasi printer dari seorang warga negara Indonesia yang diduga telah mencetak memes secara illegal, coba cari tahu apa yang sebenarnya dicetak<br>

Diberikan sebuah printerlog
<br><br>
<p align="center">
<img src="https://github.com/laBigby/cscctf-foren2/blob/master/201.JPG">
</p>
<br><br>
Terdapat 262144 entry di dalam log tersebut, dan di setiap entry terdapat 3 value yang yang dipisahkan oleh koma<br>
Ketiga value tersebut merupakan RGB value, kita harus merangkai gambar yang dimaksud pixel by pixel sesuai dengan RGB value di setiap entry<br>
Terdapat 262144 entry yang berarti 262144 pixel, yang berarti gambar berukuran 512x512 pixel<br><br>
Soal bisa diselesaikan dengan scripting<br><br>
from PIL import Image<br>
import re<br>
f=open("printerlog", 'r')<br>
x = []<br>
for line in f.readlines():<br>
	try:<br>
		(front,r,g,b,back) = map(int, re.findall(r'\d+', line))<br>
	except:<br>
		continue<br>
	x.append((front,r,g,b,back))<br>
gbr = Image.new("RGB", (512,512))<br>
pixel = gbr.load()<br>
k=0<br>
for i in range(0,512):<br>
	for j in range(0,512):<br>
		pixel[j,i] = (x[k][1], x[k][2], x[k][3])<br>
		k+=1<br>
gbr.save("new.jpg")<br><br>
<p align="center">
<img src="https://github.com/laBigby/cscctf-foren2/blob/master/new.jpg">
</p>
<br><br>
Dapat di scan QR code nya dan didapatkan flag di google drive
<br>
Flag : CCC{1_r4n_0ut_of_1d3as_t0_wr1t3_as_fl4g}
