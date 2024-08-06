# Magang-Infra-Team
# knowledge base
1. Apa yang anda ketahui tentang Bare Metal?
   - jawaban :
     Bare Metal adalah sebuah istilah yang mengacu pada sebutan “hard disk” OS (Operating System) sebuah komputer yang akan kita instal. Berbeda dengan hard disk pada umumnya yang komputer miliki, Bare Metal lebih mengacu pada layanan cloud computing sehingga muncul istlah Bare Metal Cloud atau environment yaitu sebuah Virtual Machine (VM) yang diinstal secara langsung pada hardware yaitu hard disk/bare metal bukan dalam host operating system.

     Kelebihan utama dari menggunakan bare metal adalah kontrol penuh atas perangkat keras dan potensi performa maksimal, karena tidak ada overhead dari lapisan tambahan seperti sistem operasi atau hypervisor. Namun, ini juga berarti lebih banyak tanggung jawab dalam hal manajemen perangkat keras, pembaruan, dan keamanan.

2. Apa yang anda ketahui tentang konsep jaringan VLAN?
   - jawaban :
     VLAN (Virtual Local Area Network) adalah teknologi jaringan komputer yang memungkinkan pemisahan jaringan fisik menjadi beberapa jaringan logis. Dimana hal ini memungkinkan seorang administrator jaringan membuat beberapa jaringan virtual untuk keperluan fleksibilitas dan skalabilitas. Hal ini memungkinkan kita untuk mengelola dan mengoptimalkan lalu lintas jaringan dengan lebih baik.
     
3. Apa yang anda ketahui tentang IPMI / Ip Management pada server?
   - jawaban :
      IPMI adalah singkatan dari Intelligent Platform Management Interface, untuk server tipe lama biasa tidak dilengkapi dengan fitur IPMI, sedangkan di server moderen secara default sudah build in IPMI.
     
      IPMI sendiri sangat berguna untuk melakukan remote pada server tersebut jika terjadi kendala dan mengetahui informasi-informasi apa saja yang ada didalam server tersebut dari sisi hardwarenya.

     Fitur pada IPMI yaitu menampilkan informasi-informasi penting server seperti suhu, voltage, vga, hdd/ssd storage beserta dengan log nya dan remote KVM yang dapat digunakan untuk melihat layar server secara remote melalui java console.

5. Pernahkah anda mendesign suatu jaringan pada suatu kantor/perusahaan/campus sebutkan dan jelaskan?
   - jawaban :
     Pernah, dengan skenario sebagai berikut:
     
     Sebuah perusahaan perfilman terdiri dari empat bagian yaitu Manajemen, Kreatif, HRD, dan Produksi. Perusahaan tersebut medirikan sebuah gedung dua lantai (Kantor A) dan satu kantor cabang (Kantor B).

     - Dengan kebutuhan jaringan :
       - Kantor A Lantai 1
         1. Ruang HRD - 3 komputer dan 1 printer - terhubung ke switch A -  terhubung ke router 0
         2. Ruang Manajemen - 6 Komputer dan 1 printer - terhubung ke switch A - terhubung ke router 0
       - Kantor A Lantai 2
         1. Ruang Kreatif - 7 komputer dan 1 printer - terhubung ke switch B -  terhubung ke router 1
       - Kantor B Lantai 1
         1. Ruang Produksi - 3 komputer dan 1 printer - terhubung ke switch C -  terhubung ke router 2
       - Kantor B Lantai 2
         1. Ruang Produksi - 5 komputer dan 1 printer - terhubung ke switch D -  terhubung ke router 3
      - Kantor A dan Kantor B merupakan autonomous system yang berbeda. Menghubungkan host to host dengan menggunakan Cisco Packet Tracer. Alamat IP end device yang terhubung ke jaringan menggunakan DHCP. Menggunakan protokol OSPF untuk routing dinamis dalam satu Kantor dan menghubungkan Kantor A dan Kantor B menggunakan protokol BGP(Border Gateway Protocol).



# Design Modules

Desain Jaringan dan Alokasi IP:

Lantai 3:

   - IT Networking (5 orang):
     - VLAN 10
     - IP Range: 192.168.10.1 - 192.168.10.5
       
  - Server Aplikasi (10 server):
    - VLAN 20
    - IP Range: 192.168.20.1 - 192.168.20.10
    
  - Server Database (5 server):
    - VLAN 30
    - IP Range: 192.168.30.1 - 192.168.30.5

Lantai 2:

   - Developer/Programmer (200 orang):
     - VLAN 40
     - IP Range: 192.168.40.1 - 192.168.40.200

   - Database Engineer (50 orang):
     - VLAN 50
     - IP Range: 192.168.50.1 - 192.168.50.50

   - QA/QC Engineer (50 orang):
     - VLAN 60
     - IP Range: 192.168.60.1 - 192.168.60.50

Lantai 1:

   - Manager (10 orang):
     - VLAN 70
     - IP Range: 192.168.70.1 - 192.168.70.10

   - Front Office (8 orang):
     - VLAN 80
     - IP Range: 192.168.80.1 - 192.168.80.8
- Diagram Jaringan:
-               +-------------------------------------+
                |               Lantai 3             |
                +-------------------------------------+
                | VLAN 10 (IT Networking)             |
                | VLAN 20 (Server Aplikasi)           |
                | VLAN 30 (Server Database)           |
                +-------------------------------------+
                                 |
                                 | Switch Layer 3
                                 |
                +-------------------------------------+
                |               Lantai 2             |
                +-------------------------------------+
                | VLAN 40 (Developer/Programmer)      |
                | VLAN 50 (Database Engineer)         |
                | VLAN 60 (QA/QC Engineer)            |
                +-------------------------------------+
                                 |
                                 | Switch Layer 3
                                 |
                +-------------------------------------+
                |               Lantai 1             |
                +-------------------------------------+
                | VLAN 70 (Manager)                   |
                | VLAN 80 (Front Office)              |
                +-------------------------------------+
- Pengaturan Routing dan ACL:
1. ACL (Access Control List) pada VLAN 20 (Server Aplikasi):
   - Izinkan akses dari VLAN 10, VLAN 40, VLAN 70, dan VLAN 80.
   - Deny akses dari VLAN lainnya.
     
2. ACL pada VLAN 30 (Server Database):
   - Izinkan akses dari VLAN 10, VLAN 40, dan VLAN 50.
   - Deny akses dari VLAN lainnya.
     
3. Manager & Front Office (VLAN 70 & VLAN 80):
   - Izinkan akses hanya ke VLAN 20.
     
4. IT Networking (VLAN 10):
   - Izinkan akses ke semua VLAN.
