GCC ile farkları : 

| **Özellik**           | **LLVM/Clang**                                                | **GCC**                                           |
| --------------------- | ------------------------------------------------------------- | ------------------------------------------------- |
| **Hızlı Derleme**     | Daha hızlıdır                                                 | Genellikle daha yavaştır                          |
| **Modülerlik**        | Evet, bağımsız bileşenlerden oluşur                           | Daha monolitik yapıdadır                          |
| **Hata Raporlama**    | Daha okunaklı hata mesajları üretir                           | Hata mesajları genellikle karmaşıktır             |
| **Kod Optimizasyonu** | Daha iyi optimizasyon yapabilir (özellikle `-O3` seviyesinde) | Çoğu durumda iyidir, ancak LLVM kadar esnek değil |

LLVM (**Low Level Virtual Machine**), esnek ve modüler bir derleyici altyapısıdır.

#### Bileşenleri :
1. LLVM Core :  
	- Derleyicilik yapan ana bileşen
	- LLVM IR denilen bir **ara kod** kullanır.
2. Clang(C/C++ derleyicisi) : 
	- C, C++ ve Objective-C için **LLVM tabanlı** bir ön uç (frontend) derleyicidir.
	-  GCC ye alternatiftir
3. LLDB (Hata Ayıklayıcı):
	- GDB'ye alternatif olarak kullanılabilir.
4. LLD (Bağlayıcı): 
5. libc++ (C++ Standart Kütüphanesi)

## **LLVM Nerelerde Kullanılır?**

- **Modern derleyiciler** (Clang, Rust, Swift gibi dillerin derleyicileri LLVM kullanır)
- **Just-in-Time (JIT) derleme** (Örn: WebAssembly, JavaScript motorları)
- **Performans analizleri ve optimizasyonlar**
- **Özel derleyiciler ve programlama dili geliştirme**