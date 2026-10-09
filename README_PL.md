# 🛡️ Wazuh SIEM i Zautomatyzowany Kanał Powiadomień

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

## 📌 Cel Projektu
Projekt polega na wdrożeniu systemu **Wazuh SIEM** do monitorowania środowiska Active Directory oraz konfiguracji bezpiecznych, automatycznych powiadomień e-mail przy użyciu lokalnego serwera **Postfix** i piaskownicy **Mailtrap**.

## ⚙️ Wykorzystane Technologie
* **SIEM:** Wazuh Manager & Wazuh Agent
* **Systemy:** Ubuntu Linux, Windows Server 2022
* **Sieć:** Wewnętrzna sieć VirtualBox, Statyczny Routing
* **Poczta:** Postfix (SMTP Relay), Uwierzytelnianie SASL, Mailtrap

## 🚀 Zrealizowane Zadania
* Uruchomienie Wazuh Managera na systemie Ubuntu i podłączenie Agenta na Kontrolerze Domeny (Windows Server).
* Monitorowanie dzienników zdarzeń Windows w czasie rzeczywistym (szczególnie audyt operacji na kontach AD - np. Event ID 4720).
* Skonfigurowanie serwera przekazującego Postfix z użyciem uwierzytelniania SASL do bezpiecznego przesyłania powiadomień.
* Modyfikacja pliku konfiguracyjnego `ossec.conf` w celu zautomatyzowania wysyłki e-maili po przekroczeniu progu bezpieczeństwa.

## 🛠️ Problemy i jak je rozwiązałem (Troubleshooting)
1. **Błąd uwierzytelniania SASL w Postfix:** 
   * *Problem:* Serwer Postfix nie mógł uwierzytelnić się w zewnętrznej usłudze Mailtrap.
   * *Rozwiązanie:* Utworzyłem i poprawnie zmapowałem poświadczenia w pliku `/etc/postfix/sasl_passwd`, skompilowałem bazę poleceniem `postmap`, a następnie zabezpieczyłem pliki odpowiednimi uprawnieniami (`chmod 600`), co przywróciło pełną komunikację SMTP.
2. **Brak łączności Agenta z Menedżerem:** 
   * *Problem:* Agent na systemie Windows Server miał status rozłączonego w panelu Wazuha.
   * *Rozwiązanie:* Zdiagnozowałem problem z ruchem wirtualnej sieci. Wymusiłem statyczne adresy IP na izolowanych kartach sieci wewnętrznej (`192.168.10.x`) i zrestartowałem usługę w PowerShell (`Restart-Service -Name wazuh`), co ustabilizowało połączenie.

## 📸 Zrzuty ekranu
<img width="1710" height="1387" alt="Stan Wazuh" src="https://github.com/user-attachments/assets/5617f49d-7a5e-4c13-b1ac-99658c61bcec" />
<img width="1024" height="830" alt="Logi Wazuh" src="https://github.com/user-attachments/assets/da1816a0-d30f-4441-a091-babfe62faff9" />
<img width="1715" height="1386" alt="Logi WS" src="https://github.com/user-attachments/assets/709e5606-8fcd-4204-8ffe-2b8c35992448" />
<img width="1024" height="389" alt="MailTrap" src="https://github.com/user-attachments/assets/63b64122-45d6-4fcc-9730-dbe0481333d4" />
