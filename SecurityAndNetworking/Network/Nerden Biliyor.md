
bir sunucuya istek atarken routerda NAT ile ip değişimi oluyor peki sunucu response dönerken localdeki beni nasıl biliyor yada router bana geldiğini nereden biliyor

- **NAT (Network Address Translation)** kullanarak:
    
    - Local IP'ini kendi public IP'si (mesela `85.105.200.30`) ile değiştiriyor.
        
    - Aynı zamanda local IP + local port bilgisini, kendi içindeki bir tabloya yazıyor. (NAT tablosu)
        
    
    Örneğin:
    
    `192.168.1.5:52314 → 85.105.200.30:40215`
    (Senin bilgisayarında port 52314'ten çıkan istek, router'da port 40215'e eşleniyor.)
    
- Sunucu, router'ın public IP'sine ve 40215 portuna cevap dönüyor.
    
- Router cevabı alınca NAT tablosuna bakıyor:
    
    - "Hmm 40215 portu, 192.168.1.5:52314 ile eşleştirilmiş."
        
    - Bu yüzden cevabı doğru şekilde senin bilgisayarına yönlendiriyor.


![[NatPort.png]]