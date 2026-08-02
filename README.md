# DeathNote
 Перша команда яку ми використовуємо    sudo netdiscover -r 10.0.2.0/24
 та    nmap -Pn -V 10.0.2.X
<img width="675" height="164" alt="image" src="https://github.com/user-attachments/assets/3d6324c3-a88a-485e-ad5d-b818000c0bdb" />

Перевіримо айпі на якій з двох відкриватиметься потрібна сторінка.
Вводимо у термінал команду sudo nano /etc/hosts та вводимо айпі
<img width="477" height="180" alt="image" src="https://github.com/user-attachments/assets/d7e4ca05-3cfa-4af9-9875-ad3bd2723c5c" />

Оновлюємо сторінку та отримуємо доступ до сайту:
<img width="1917" height="895" alt="image" src="https://github.com/user-attachments/assets/5ddf0f03-1018-43b4-a03f-5a50f61a02b4" />

Натискаємо F12 та у пошуковому рядку вводимо kira. Шукаємо та копіюємо це посилання:
http://deathnote.vuln/wordpress/wp-content/uploads/2021/07/
<img width="1197" height="723" alt="image" src="https://github.com/user-attachments/assets/dcf2136a-763e-4e6b-ae89-af1fc62771e5" />

Переходимо за посиланням:
<img width="1055" height="898" alt="image" src="https://github.com/user-attachments/assets/565403b5-a30d-4a07-b098-9b3165f22629" />

Для сканування директорій використаємо команду: 
dirsearch -u http://deathnote.vuln/
<img width="1478" height="730" alt="image" src="https://github.com/user-attachments/assets/4a2fefc8-98f8-429d-8801-e064c204e18f" />

У просканованих файлах знаходимо robots.txt, перейдемо за посиланням http://deathnote.vuln/robots.txt
<img width="778" height="418" alt="image" src="https://github.com/user-attachments/assets/eff4b193-901e-41e7-bbbe-33b1b4a774b7" />

Заходимо на сторінку з /important.jpg:
<img width="1445" height="412" alt="image" src="https://github.com/user-attachments/assets/5769643f-13f9-4db8-b573-e733afc6fea4" />

Але не знайшовши там нічого, використовуємо команду:
curl http://deathnote.vuln/important.jpg
<img width="607" height="256" alt="image" src="https://github.com/user-attachments/assets/df8eeec9-e38c-4cc2-9c39-44ae70c4b1ce" />

Отримуємо відповідь, у якій згадуються user.txt — може бути ідентифікатор, а також notes.txt — може бути список паролів.
<img width="522" height="72" alt="image" src="https://github.com/user-attachments/assets/ef2ea556-377f-4243-bf2a-4e1dcc85f9c9" />

Вміст notes.txt:
<img width="942" height="760" alt="image" src="https://github.com/user-attachments/assets/d318191a-85b6-421b-9065-ff8037d53169" />

Вміст user.txt:
<img width="937" height="451" alt="image" src="https://github.com/user-attachments/assets/19158f67-dd99-4e9a-b94b-2ec0521cc366" />

Скористаємось інструментом для брут-форсу логінів і паролів hydra:
hydra -L user.txt -P notes.txt 10.0.2.3 ssh
<img width="1347" height="281" alt="image" src="https://github.com/user-attachments/assets/e99c0db0-ac37-4122-86ee-84282405e844" />

Заходимо через ssh порт з отриманими логіном і паролем (l:death4me):
ssh l@10.0.2.X
Після логінування через ssh в домашньому каталозі cеред файлів знаходимо user.txt.
Використовуємо команду ls -la
<img width="482" height="43" alt="image" src="https://github.com/user-attachments/assets/5266e27f-9878-46d2-bf23-f8235190b8ec" />

Переглядаємо файл, використовуючи cat user.txt:
<img width="1919" height="106" alt="image" src="https://github.com/user-attachments/assets/4307da39-52ee-4044-beda-e3463202f2e3" />


i think u got the shell , but you wont be able to kill me -kira

<img width="707" height="140" alt="image" src="https://github.com/user-attachments/assets/96add347-9711-4592-9f7b-7007e1c44549" />

Переміщуючись по директорія командами cd.. cd kira cd /opt cd kira-case, знайдемо файл case.wav, де бачимо код:
<img width="713" height="347" alt="image" src="https://github.com/user-attachments/assets/da4356a1-b8ad-4a8f-acc5-f21af2f0827b" />

63 47 46 7a 63 33 64 6b 49 44 6f 67 61 32 6c 79 59 57 6c 7a 5a 58 5a 70 62 43 41 3d

Отримали підказку використовувати cyberchef:
<img width="419" height="84" alt="image" src="https://github.com/user-attachments/assets/3ae0a447-e7e9-4adc-9f55-902c03f204b7" />

При розшифровці отримаємо: passwd: kiraisevil
<img width="798" height="560" alt="image" src="https://github.com/user-attachments/assets/5ace31dd-1592-4ab7-a246-b4e03be50cd0" />
<img width="402" height="497" alt="image" src="https://github.com/user-attachments/assets/7138b8f5-91d4-440f-bf13-1b2e78d95675" />

Змінюємо користувача поточної сесії на kira, використовуючи знайдений пароль:
<img width="411" height="102" alt="image" src="https://github.com/user-attachments/assets/af71df2b-7745-477e-9a8f-76f4d3ea1fb6" />

Спробуємо використати той самий пароль для отримання суперкористувача: вводимо команду sudo -i, змінюємо директорію (cd /root), та переглядаємо файли (ls).Знаходимо файл root.txt та виводимо:
<img width="1033" height="358" alt="image" src="https://github.com/user-attachments/assets/55bf0a0a-648b-4fc1-828d-0c50569a04f9" />

