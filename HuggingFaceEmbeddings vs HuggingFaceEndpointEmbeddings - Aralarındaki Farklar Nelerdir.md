Bu dosya, LangChain altyapısında Hugging Face modelleriyle embedding (vektörleştirme) süreçlerinin iki farklı yöntemle (`HuggingFaceEmbeddings` ve `HuggingFaceEndpointEmbeddings`) nasıl gerçekleştirildiğini, mimari farklarını, maliyet/performans dengelerini ve örnek kod yapılarını inceler.

| **Karşılaştırma Kriteri** | **HuggingFaceEmbeddings** | **HuggingFaceEndpointEmbeddings** |
|----|----|----|
| **Çalışma Ortamı (Execution)** | Yerel sunucu veya makine üzerinde süreç içi (in-process) olarak çalışır. | Hugging Face bulut altyapısı (sunucusuz veya özel uç noktalar) üzerinden uzaktan çalışır. |
| **Temel Bağımlılık** | `sentence-transformers` kütüphanesini baz alır ve model ağırlıklarını yerel diske indirir. | `huggingface_hub` kütüphanesini kullanır ve model ile API üzerinden iletişim kurar. |
| **Donanım / Kimlik Doğrulama** | Yerel CPU, GPU (CUDA) veya Apple Silicon (MPS) kaynaklarını kullanır; API anahtarı zorunlu değildir. | Yerel donanım yükü yoktur; `HUGGINGFACEHUB_API_TOKEN` çevre değişkeni veya parametre ile kimlik doğrulama zorunludur. |
| **Maliyet ve Veri Gizliliği** | Ek API maliyeti yoktur; veri yerel ortam dışına çıkmadığı için veri güvenliği üst düzeydedir. | Uç nokta katmanına göre maliyet üretir; veriler ağ üzerinden Hugging Face sunucularına iletilir. |
| **Optimum Kullanım Senaryosu** | Çevrimdışı (offline) sistemler, yüksek gizlilik gerektiren veriler ve yerel donanım gücüyle yapılan yüksek throughput işlemleri. | Sınırlı yerel kaynak/RAM bulunan ortamlar, sunucusuz mimariler (AWS Lambda vb.) ve büyük modelleri yerelde çalıştırmama gereksinimi. |
