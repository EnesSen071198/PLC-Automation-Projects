# PNP_SENSOR_CONNECTION – TIA Portal (S7-1200 1212C DC/DC/DC) Notları

## 1) Varsayım / Kabul (ÖNEMLİ)
Bu ladder, **input’ların “aktif=1”** geldiği varsayımıyla çalışır.

- **E-Stop / Termik / Motor koruma** sahada çoğunlukla **NC** elemandır.  
  PNP bağlantıda NC seri hat **sağlıklı iken 1**, bastığında/attığında **0** üretir.  
  Bu durumda ladder’da bunları **NO kontak (| |)** gibi kullanmak doğrudur.

Eğer sende bu input’lar **sağlıklı iken 0** geliyorsa, ladder doğru görünse bile davranış ters olur.  
Çözüm: ya kontak tipini tersle (NC/NO), ya da `*_OK` gibi terslenmiş bir tag üret.

## 2) I/O Eşlemesi (Ekrandaki Adreslere Göre)
### Inputs
- `%I0.0` → `I_ESTOP`
- `%I0.1` → `I_START_BTN`   
- `%I0.2` → `I_STOP_BTN`   
- `%I0.3` → `I_THERMAL_RELAY`
- `%I0.4` → `I_MOTOR_PROTECTION`
- `%I0.5` → `I_LIMIT_SWITCH`
- `%I0.6` → `I_INDUCTIVE_SENSOR`
- `%I0.7` → `I_OPTICAL_SENSOR`

### Outputs
- `%Q0.0` → `Q_RELAY_1`
- `%Q0.1` → `Q_RELAY_2`
- `%Q0.2` → `Q_RELAY_3`
- `%Q0.3` → `Q_RELAY_4`
- `%Q0.4` → `Q_RELAY_5`
- `%Q0.5` → `Q_RELAY_6`


## 3) Network Mantığı  

### Network 1 – RÖLE 1 (Master Enable)
Koşul: `I_ESTOP` AND `I_THERMAL_RELAY` AND `I_MOTOR_PROTECTION`  
Çıkış: `Q_RELAY_1`

Amaç: Güvenlik zinciri sağlıklıysa **master röle** aktif olsun.

### Network 2 – RÖLE 2 (Start/Stop + Mühürleme)
Koşul: `Q_RELAY_1` AND `I_STOP_BTN` AND (`I_START_BTN` OR `Q_RELAY_2`)  
Çıkış: `Q_RELAY_2`

Amaç: Klasik start-stop mühürleme.
- Start basınca çalışır.
- Stop’a basınca düşer.
- `Q_RELAY_1` düşerse otomatik düşer.

> Kritik: `I_STOP_BTN` sinyali **bırakılmışken 1** olmalı (NC buton + PNP en yaygını).  
> Eğer stop NO ise (bırakılmışken 0), bu network sürekli kilitli kalır.

### Network 3 – RÖLE 3 (Limit Switch)
Koşul: `Q_RELAY_1` AND `I_LIMIT_SWITCH`  
Çıkış: `Q_RELAY_3`

### Network 4 – RÖLE 4 (İndüktif Sensör)
Koşul: `Q_RELAY_1` AND `I_INDUCTIVE_SENSOR`  
Çıkış: `Q_RELAY_4`

### Network 5 – RÖLE 5 ve RÖLE 6 (Optik Sensör)
Koşul: `Q_RELAY_1` AND `I_OPTICAL_SENSOR`  
Çıkışlar: `Q_RELAY_5` ve `Q_RELAY_6` (aynı şartta paralel)

Amaç: Optik sensör gelince iki röleyi aynı anda sürmek.
