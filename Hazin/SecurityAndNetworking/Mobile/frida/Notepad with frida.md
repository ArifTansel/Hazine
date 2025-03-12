
```python
import frida

def on_message(message, data):
    print("[on_message] message:", message, "data:", data)

session = frida.attach("notepad.exe")  
script = session.create_script("""
rpc.exports.enumerateModules = () => {
  return Process.enumerateModules();
};
""")

script.on("message", on_message)
script.load()
print([m["name"] for m in script.exports_sync.enumerate_modules()])
```

C:\Users\Arif\Desktop\SEC\for_frida>python example.py 
'notepad.exe', 'ntdll.dll', 'KERNEL32.DLL', 'KERNELBASE.dll', 'GDI32.dll', 'win32u.dll', 'gdi32full.dll', 'msvcp_win.dll', 'ucrtbase.dll', 'USER32.dll', 'combase.dll', 'RPCRT4.dll', 'shcore.dll', 'msvcrt.dll', 'COMCTL32.dll', 'IMM32.DLL', 'bcryptPrimitives.dll', 'ADVAPI32.dll', 'sechost.dll', 'bcrypt.dll', 'kernel.appcore.dll', 'uxtheme.dll', 'clbcatq.dll', 'MrmCoreR.dll', 'SHELL32.dll', 'windows.storage.dll', 'Wldp.dll', 'OLEAUT32.dll', 'shlwapi.dll', 'MSCTF.dll', 'TextShaping.dll', 'efswrt.dll', 'MPR.dll', 'wintypes.dll', 'twinapi.appcore.dll', 'oleacc.dll', 'textinputframework.dll', 'CoreUIComponents.dll', 'CoreMessaging.dll', 'WS2_32.dll', 'ntmarta.dll', 'CRYPT32.dll', 'PSAPI.DLL', 'DNSAPI.dll', 'IPHLPAPI.DLL', 'ole32.dll', 'WINMM.dll', 'NSI.dll'

`session = frida.attach("notepad.exe") ` ile `notepad.exe` ye bağlanır 
`script = session.create_script()` ile script oluşturulur `on load` 

`on` fonksiyonunda kullanılan `callback` fonksiyonunu çalıştırabilmek için oluşturulan JS kodunda bir `send()` fonksiyonu yazılmalıdır.

`script.exports_sync.enumerateModules` js içindeki `enumerateModules` fonksiyonunun dönderdiği değerleri bekler ve alır. 
