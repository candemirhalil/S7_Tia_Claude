HCD Agent — Özellikler ve Çalışma Şekli / Features and How It Works candemirhalil@gmail.com
19 Kas 2026 · @Halil Can Demir
Türkçe — Genel bakış
HCD Agent, TIA Portal V15 projelerini Claude ile ve kendi masaüstü penceresiyle okuyup değiştiren bir otomasyon aracıdır. Geliştiren: Halil Can Demir (candemirhalil@gmail.com), Sanem Plastik.
Amaç: PLC ve HMI değişikliklerini sohbetten tarif edip, yedekli ve kayıtlı şekilde projeye uygulamak; projeden otomatik rapor ve bağlantı şeması çıkarmak. Siemens'in TIA Portal Openness arayüzünü kullanır, ek program veya paket gerektirmez.
Özellikler
Alan
Ne yapar
Bağlantı
Açık TIA Portal'ları PID ve proje adıyla bulur; tek proje açıksa kendiliğinden bağlanır. PLC, HMI ve sürücülerin IP / PROFINET / DP adreslerini gösterir.
Tam okuma
Bağlanınca 2-3 sn sonra arka planda tüm blokları, PLC taglarını, HMI ekran / şablon / tag tablolarını ve HMI taglarını okur; pencere donmaz.
PLC blokları
Listeleme, XML (SimaticML) dışa aktarma, düzenleme, içe aktarma + derleme, tek blok silme (tam isimle).
PLC tagları
Listeleme, arama, yeni tag ekleme (ekledikten sonra geri okuyup derler).
HMI
Ekran, ekran şablonu ve HMI tag tablosu dışa / içe aktarma, HMI derleme.
PLC'ye yükleme
Manuel veya Otomatik mod; sadece yazılım yükler. STOP veya DB yeniden ilklendirme gerekirse yüklemez.
Yedek ve Geri Al
Her değişiklikten önce XML yedeği; tek tıkla geri dönüş (dönüşten önce mevcut hal de yedeklenir).
Rapor
Excel rapor + EPLAN tarzı PDF bağlantı şeması: ağ topolojisi, istasyon yerleşimi, modül / kanal / klemens sayfaları, I/O listesi.
İşlem kaydı
Claude'un ve pencerenin yaptığı her işlem islem_kaydi.csv dosyasına yazılır.
Claude bağlantısı
20'yi aşkın araç (MCP); Claude aynı bağlantıyı ve aynı kuralları kullanır.
Görünüm
Açık / Koyu / Lacivert tema; başlıkta ve alt çubukta geliştirici adı ve e-postası.
Güvenlik kuralları ve sınırlar
• Yedek: İçe aktarma, silme, tag ekleme ve geri almadan önce eski hal Yedekler klasörüne XML olarak alınır.
• Online kilidi: TIA online iken hiçbir değişiklik yapılmaz; önce Go offline gerekir.
• Silme: Sadece tek blok, tam isimle, joker (*) yok; onay için blok adı tekrar yazılır.
• PLC'ye yükleme: Varsayılan Manuel. Otomatik modda da PLC'nin STOP'a alınması veya DB'lerin sıfırlanması gerekiyorsa yükleme yapılmaz, sebebi gösterilir.
• Onay: Claude, projeyi değiştiren araçları kullanıcının açık onayı olmadan çağırmaz.
• Tek işlem: Claude ve pencere aynı anda TIA'ya işlem gönderemez; sırayla çalışırlar.
Sınırlar: sadece TIA Portal V15; HMI panele yükleme TIA'dan elle yapılır (V15 Openness desteklemiyor); Step 7 Classic projeleri okunamaz; donanım ekleme ve teknoloji nesneleri henüz yok.
Kurulum ve günlük kullanım
Gerekenler: Windows 10/11, TIA Portal V15 (Openness dahil), Windows kullanıcısı "Siemens TIA Openness" grubunda, Python 3, PDF için Microsoft Edge.
1.  HCD_Agent klasörünü masaüstüne koy; Claude bağlantısı için claude_desktop_config.json içine hcd-agent satırını ekleyip Claude'u yeniden başlat.
2.  TIA'da projeyi aç, START.bat ile HCD Agent'ı başlat. İlk bağlantıda TIA erişim sorarsa "Yes to all".
3.  Bağlantı sekmesinde proje, PLC ve IP görünür; 2-3 sn sonra tüm veri okunur.
4.  Değişiklik: Claude'a tarif et ya da XML'i pencerede düzenle → içe aktar → derleme sonucunu kontrol et → TIA'da Save project.
5.  PLC'ye yükleme: Manuel modda TIA'dan veya Ayarlar → "Şimdi PLC'ye yükle"; HMI'a yükleme TIA'dan.
6.  Sorun olursa: Yedekler · Geri Al sekmesinden önceki hale dön; ne olduysa İşlem Kaydı sekmesinde görünür.
7.  Rapor: Bağlantı sekmesi → "Rapor + bağlantı şeması" → Raporlar klasöründe Excel ve PDF.
English — Overview
HCD Agent is an automation tool that reads and changes TIA Portal V15 projects, both through Claude and through its own desktop window. Developed by Halil Can Demir (candemirhalil@gmail.com), Sanem Plastik.
Purpose: describe PLC and HMI changes in a chat and apply them to the project with a backup and a log, and generate reports and wiring diagrams from the project automatically. It uses Siemens TIA Portal Openness and needs no extra programs or packages.
Features
Area
What it does
Connection
Finds open TIA Portal instances by PID and project name; connects automatically when one project is open. Shows IP / PROFINET / DP addresses of PLCs, HMIs and drives.
Full read
2-3 s after connecting, reads all blocks, PLC tags, HMI screens / templates / tag tables and HMI tags in the background; the window stays responsive.
PLC blocks
List, export as XML (SimaticML), edit, import + compile, delete a single block (exact name).
PLC tags
List, search, add a tag (read back and compiled after adding).
HMI
Export / import screens, screen templates and HMI tag tables; compile the HMI.
Download to PLC
Manual or Automatic mode; software only. Nothing is downloaded if STOP or DB reinitialization would be required.
Backup and Undo
XML backup before every change; one-click restore (the current state is backed up before restoring).
Report
Excel report + EPLAN-style PDF wiring diagram: network topology, station layout, module / channel / terminal pages, I/O list.
Activity log
Every action by Claude or the window is written to islem_kaydi.csv.
Claude connection
20+ tools (MCP); Claude uses the same connection and the same rules.
Look
Light / Dark / Navy theme; developer name and e-mail in the title and status bar.
Safety rules and limits
• Backup: Before import, delete, tag add or undo, the previous state is saved as XML in the Yedekler (Backups) folder.
• Online lock: No change is made while TIA is online; go offline first.
• Delete: One block only, by exact name, no wildcards (*); the block name must be typed again to confirm.
• Download to PLC: Manual by default. Even in Automatic mode, nothing is downloaded if the PLC would have to go to STOP or DBs would be reset; the reason is shown.
• Approval: Claude does not call tools that change the project without the user's explicit approval.
• One at a time: Claude and the window cannot send operations to TIA at the same time; they run in turn.
Limits: TIA Portal V15 only; downloading to the HMI panel is done manually from TIA (V15 Openness does not support it); Step 7 Classic projects cannot be read; adding hardware and technology objects are not available yet.
Setup and daily use
Requirements: Windows 10/11, TIA Portal V15 (with Openness), the Windows user in the "Siemens TIA Openness" group, Python 3, Microsoft Edge for PDF output.
1.  Put the HCD_Agent folder on the desktop; for the Claude connection add the hcd-agent entry to claude_desktop_config.json and restart Claude.
2.  Open the project in TIA and start HCD Agent with START.bat. If TIA asks for access on the first connection, choose "Yes to all".
3.  The Connection tab shows the project, PLC and IP; 2-3 s later all data is read.
4.  To change something: describe it to Claude or edit the XML in the window → import → check the compile result → Save project in TIA.
5.  Download to PLC: in Manual mode from TIA or Settings → "Download to PLC now"; HMI download from TIA.
6.  If something goes wrong: go back with the Backups · Undo tab; every action is in the Activity Log tab.
7.  Report: Connection tab → "Report + wiring diagram" → Excel and PDF in the Raporlar folder.
