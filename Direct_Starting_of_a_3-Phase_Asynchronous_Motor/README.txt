🔌 3 Fazlı Asenkron Motora Direkt Yol Verme (DOL Starter)
📌 Proje Açıklaması (TR)

Bu projede, Siemens S7-1200 PLC kullanılarak 3 fazlı asenkron motorun direkt yol verme (Direct Online - DOL) yöntemi ile çalıştırılması gerçekleştirilmiştir.

Sistem; start-stop kontrolü, mühürleme (self-hold) ve aşırı akım koruma mantığı içermektedir.

⚙️ Kullanılan Bileşenler

Siemens S7-1200 PLC

Start Butonu (NO)

Stop Butonu (NC)

Aşırı Akım Rölesi (NC kontakt)

Kontaktör (Motor sürme)

3 Fazlı Asenkron Motor

🧠 Çalışma Mantığı

Start butonuna basıldığında motor çalışır.

Motor rölesi, kendi kontağı üzerinden mühürleme yaparak çalışmayı sürdürür.

Stop butonuna basıldığında sistem durur.

Aşırı akım rölesi devreye girerse motor otomatik olarak durdurulur.

🔁 Ladder Diyagramı

Sistem aşağıdaki mantık ile çalışır:

Aşırı akım rölesi (NC)

Stop butonu (NC)

Start butonu (NO)

Motor çıkışı (self-hold ile)

🏷️ Tag Listesi
Tag Adı	Açıklama	Adres
I0.0	Aşırı Akım Rölesi	NC
I0.1	Stop Butonu	NC
I0.2	Start Butonu	NO
Q0.0	Motor Rölesi	Çıkış
🎯 Amaç

Bu proje ile:

PLC ladder logic temellerini öğrenmek

Endüstriyel motor kontrol mantığını kavramak

Gerçek saha uygulamalarına giriş yapmak

🌍 Project Description (EN)

This project demonstrates how to control a 3-phase induction motor using a Direct Online (DOL) starter method with a Siemens S7-1200 PLC.

The system includes start-stop control, self-holding (latching), and overcurrent protection logic.

⚙️ Components

Siemens S7-1200 PLC

Start Push Button (NO)

Stop Push Button (NC)

Overcurrent Relay (NC contact)

Contactor

3-Phase Induction Motor

🧠 Working Principle

Pressing the start button runs the motor.

The system maintains operation via self-holding contact.

Pressing the stop button stops the motor.

If overcurrent occurs, the system shuts down automatically.

🎯 Purpose

Learn PLC ladder logic basics

Understand industrial motor control systems

Build a foundation for automation projects