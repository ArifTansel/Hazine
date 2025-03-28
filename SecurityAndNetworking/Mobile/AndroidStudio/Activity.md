farklı aktiviteler falan vardır bir nevi pageler gibi işliyormuş

oluşturmak için ilk olarak tanımlamalıyız o aktiviteyi 
`AndroidManifest.xml` dosyasını aç ve oraya bir `<activity>` oluştur 

```xml 
<manifest ... >
  <application ... >
      <activity android:name=".ExampleActivity" />
      ...
  </application ... >
  ...
</manifest >
```
Tek gerekli agüman android:name argümanıdır ve oluşturulacak activity'nin sınıf adını(class name) ini belirtir.

#### Declare intent filters 

bir activitynin sadece explicit olmasını değil hem de implict olmasını sağlar.
explicit request : Start the Send e-mail activity in the Gmail app
implicit request : Start a Send Email screen in any activity that can do the job

> [!NOTE]
>Uygulamanızın kendi kendine yeten bir uygulama olmasını ve diğer uygulamaların aktivitelerini etkinleştirmesine izin vermemesini istiyorsanız, başka bir `intent-filter` ihtiyacınız yoktur

bu avantajı kullanmak için `<intent-filter>` kullanabilirsin içindekiler  : 
- `<action>` bu aktivite data göndereceği 
-  `<category>` bu activite launch request alabileceği
-  `<data>` bu activitenin göndereceği verinin tipini belirtir.
```kotlin 
<activity android:name=".ExampleActivity" android:icon="@drawable/app_icon">
    <intent-filter>
        <action android:name="android.intent.action.SEND" />
        <category android:name="android.intent.category.DEFAULT" />
        <data android:mimeType="text/plain" />
    </intent-filter>
</activity>
```

burada main activity olarak belirtebiliriz istediğimiz bir actionu 
```kotlin
<action android:name="android.intent.action.MAIN" />
```
#### Declare Permissions 

