
The main advantages of having a configured Windows domain are:
- **Centralised identity management:** All users across the network can be configured from Active Directory with minimum effort.
- **Managing security policies:** You can configure security policies directly from Active Directory and apply them to users and computers across the network as needed.

The core of any Windows Domain is the **Active Directory Domain Service (AD DS)**. This service acts as a catalogue that holds the information of all of the "objects" that exist on your network. Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others. Let's look at some of them:

**Users** 
Users are one of the most common object types in Active Directory. Users are one of the objects known as **security principals**, meaning that they can be authenticated by the domain and can be assigned privileges over **resources** like files or printers.
two type of entities:
- **People:** users will generally represent persons in your organisation that need to access the network, like employees.
- **Services:** you can also define users to be used by services like IIS or MSSQL. Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service. 

**_Machines_**
Machines are another type of object within Active Directory; for every computer that joins the Active Directory domain, a machine object will be created.
The machine accounts themselves are local administrators on the assigned computer, they are generally not supposed to be accessed by anyone except the computer itself, but as with any other account, if you have the password, you can use it to log in.

### 🚫 3. **Neden başkası kullanmamalı?**

Çünkü:

- Makine hesapları genellikle **şifre rotasyonuna sahiptir** ve bu şifreler karmaşık, sistem tarafından belirlenir.
    
- **İzlenebilirlik** kaybolur: Eğer biri bu hesapla bir işlem yaparsa, "bu işlemi kim yaptı?" sorusunun cevabı "bilgisayar yaptı" olur. Halbuki bu durumda bir kullanıcı gizlenmiş olur.
    
- **Saldırı yüzeyi artar**: Eğer bu hesaplar dışarıya açık olursa (örneğin RDP ya da servis hesabı olarak kullanılırsa), saldırgan için bir kapı olur.


Groups can have both users and machines as members. If needed, groups can include other groups as well.

administrative responsibilities are separated into two types of administrators:

- **Service administrators**: Responsible for maintaining and delivering Active Directory Domain Services (AD DS), including managing domain controllers and configuring AD DS.
    
- **Data administrators**: Responsible for maintaining the data that's stored in AD DS and on domain member servers and workstations.

