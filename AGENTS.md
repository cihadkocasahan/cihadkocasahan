# Personal Profile (cihadkocasahan) Agent Instructions

Bu klasör, Cihad Kocaşahan'ın birincil GitHub profil ve Özgeçmiş (CV) deposudur.
Tüm işlemler aşağıdaki katı kurallara (Düzey 1 Context) göre yürütülmelidir.

## 📌 1. CV Mimari ve Bütünlük Kuralları
- **1-to-1 Simetri (Zorunlu):** `CV_Cihad_Kocasahan_TR.md` ve `CV_Cihad_Kocasahan_EN.md` dosyaları birbirinin birebir simetriği olmalıdır. Birine eklenen bir özellik veya düzeltilen bir hata, mutlaka aynı satır sırasıyla diğerine de eklenmelidir.
- **Gerçeklik ("Ne ise o" İlkesi):** Abartılı unvanlardan (Örn: Super Senior) ve süslü kelimelerden kaçınılmalıdır. Yetkinlikler kanıtlanabilir, net ve doğrudan ifade edilmelidir.
- **İç İçe Link Yasağı:** CV dosyalarının (.md) içine "PDF İndir" linki KOYMAYIN. Aksi takdirde üretilen PDF'in içinde kendisine ait bir indirme linki (Inception) oluşur. İndirme linkleri sadece `README.md` içinde bulunur.
- **Markdown Disiplini:** Listelerin (Bullet points) bozulmaması ve düz bir paragrafa dönüşmemesi için madde imlerinden önce ve sonra uygun boşluklar (Enter) bırakıldığından emin olun. Kod blokları içine (` ``` `) madde imi koymayın.
- **Public Repo / Open Source Ekleme Kuralı:** Kullanıcı "yeni public repo ekle" dediğinde, bu proje MUTLAKA 3 yere birden eklenmelidir:
  1. `README.md` dosyasındaki "🛠️ Open Source & Personal Projects" altına.
  2. `CV_Cihad_Kocasahan_TR.md` dosyasındaki "🛠️ Açık Kaynak ve Kişisel Projeler" altına (Türkçe açıklamayla).
  3. `CV_Cihad_Kocasahan_EN.md` dosyasındaki "🛠️ Open Source & Personal Projects" altına (İngilizce açıklamayla).

## 🚀 2. CI/CD PDF Otomasyonu (Zero-Config Pipeline)
- **Motor:** PDF üretimi için 3. parti sorunlu Docker tabanlı action'lar YERİNE, doğrudan GitHub Runner üzerinde **Native Node.js (`npx md-to-pdf`)** kullanılır. Bu sistem `Profile-PDF-Automator` projemizin altın standardıdır.
- **İşletim Sistemi Sabitlemesi:** Ubuntu 24.04'te gelen katı AppArmor (Sandbox) kısıtlamalarını ve Puppeteer hatalarını baypas etmek için workflow (`.github/workflows/generate-pdf.yml`) her zaman **`ubuntu-22.04`** üzerinde çalıştırılmalıdır. `--no-sandbox` ayarlarıyla uğraşılmaz.
- **Tetiklenme:** Her `git push` işlemi otomasyonu tetikler. Yeni PDF'ler otomatik olarak derlenir ve "GitHub Releases" sekmesine son sürüm olarak (Latest) yüklenir.

## 🧹 3. "Tek Temiz Push" (Single Clean Push) Doktrini
- Bu depo, uzman bir yazılımcının vitrinidir. Geçmişi "deneme", "test", "hata düzeltme" gibi commit'lerle çöplüğe dönüştürülemez.
- Büyük çaplı düzenlemelerden sonra gerekirse **Orphan Branch** tekniğiyle geçmiş temizlenir ve tek bir profesyonel `[Official Release]` commit'i ile Force Push atılır.

---
> **Not:** Eğer PDF dönüştürme motorunda köklü bir iyileştirme yapılacaksa, bu değişiklik önce `Profile-PDF-Automator` açık kaynak projesinde test edilmeli, başarılı olursa bu depoya senkronize edilmelidir.
