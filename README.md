# 🌐 Routing średniozaawansowany i podstawy przełączania

**Projekt akademicki** zrealizowany w ramach studiów inżynierskich  
**Vladyslav Fedun, Artsemi Reviakin**  
Uniwersytet WSB Merito Wrocław, 2026

---

## 📋 Opis projektu

Projekt obejmuje zaprojektowanie i wdrożenie sieci komputerowej dla **4 budynków**,  
połączonych ze sobą przez **8 routerów Cisco** z dostępem do Internetu przez dwóch dostawców ISP.

### Zrealizowane cele:
- Projektowanie adresacji IP z techniką **VLSM** (Variable Length Subnet Masking)
- Wdrożenie routingu dynamicznego **OSPF** (Area 0) na wszystkich routerach
- Segmentacja sieci przy użyciu **VLAN** (4 sieci VLAN, po jednej na budynek)
- Konfiguracja protokołu **STP** (Spanning Tree Protocol) dla stabilności warstwy 2
- Zapewnienie redundancji połączeń i wyjścia do Internetu przez **2 dostawców ISP**

---

## 🏗️ Topologia sieci

```
          ISP                ISP2
           |                  |
          R12 ------------- R13
         /    \            /    \
       R10    R11----------      |
      /    \  /    \             |
    R1     R2      R3     R4-----+
    |       |       |      |
  Bud.1  Bud.2   Bud.3  Bud.4
(VLAN10)(VLAN20)(VLAN30)(VLAN40)
```

### Urządzenia:
| Router | Rola |
|--------|------|
| R1–R4 | Routery dostępowe budynków |
| R10, R11 | Routery szkieletowe (core) |
| R12 | Router graniczny – wyjście do ISP |
| R13 | Router graniczny – wyjście do ISP2 (redundancja) |

---

## 🗺️ Adresacja IP (VLSM)

### Sieci LAN (budynki)
| VLAN | Sieć | Budynek |
|------|------|---------|
| VLAN 10 | 192.168.10.0/24 | Budynek 1 – R1 |
| VLAN 20 | 192.168.30.0/24 | Budynek 2 – R2 |
| VLAN 30 | 192.168.20.0/24 | Budynek 3 – R3 |
| VLAN 40 | 192.168.40.0/24 | Budynek 4 – R4 |

### Połączenia punkt–punkt (/30)
| Łącze | Sieć |
|-------|------|
| R1 ↔ R10 | 10.1.1.0/30 |
| R2 ↔ R10 | 10.2.2.0/30 |
| R3 ↔ R11 | 10.3.3.0/30 |
| R4 ↔ R11 | 10.4.4.0/30 |
| R10 ↔ R12 | 10.5.5.0/30 |

### Wyjście do Internetu
| Łącze | Sieć |
|-------|------|
| R12 ↔ ISP | 209.165.200.224/27 |
| R13 ↔ ISP2 | 10.10.10.0/30 |

---

## ⚙️ Technologie i protokoły

| Technologia | Zastosowanie |
|-------------|--------------|
| **OSPF** (Area 0) | Routing dynamiczny między wszystkimi routerami |
| **VLSM** | Optymalne zarządzanie przestrzenią adresową IP |
| **VLAN 10/20/30/40** | Segmentacja ruchu per budynek |
| **STP (PVST)** | Ochrona przed pętlami w warstwie 2 |
| **PPP** | Enkapsulacja na łączach szeregowych R1↔R10, R2↔R10 |
| **Dual ISP** | Redundancja wyjścia do Internetu (R12 + R13) |
| **Cisco IOS 15.1** | System operacyjny routerów Cisco 1941/2911 |

---

## 🚀 Jak otworzyć projekt

1. Pobierz i zainstaluj [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)
2. Sklonuj repozytorium:
   ```bash
   git clone https://github.com/TWOJ_NICK/cisco-ospf-vlan-project.git
   ```
3. Otwórz plik `Projekt_sieci.pkt` w Cisco Packet Tracer

---

## 📁 Struktura repozytorium

```
cisco-ospf-vlan-project/
├── README.md
├── Projekt_sieci.pkt          ← topologia Packet Tracer
└── config/
    ├── R1.txt
    ├── R2.txt
    ├── R3.txt
    ├── R4.txt
    ├── R10.txt
    ├── R11.txt
    ├── R12.txt
    └── R13.txt
```

---

## 👥 Autorzy

**Vladyslav Fedun** · **Artsemi Reviakin**  
Inżynierowie Informatyki – WSB Merito Wrocław, 2026  
📧 risev44@gmail.com
