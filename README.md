# firebase-services-checker

## Как проверить доступность сервисов Firebase?

1. Достаём из декомпилированного приложения (целевого) следующие данные:
```
<string name="google_app_id">1:421150332737:…</string>
<string name="google_api_key">AIzaSyDANl17-T_…</string>
<string name="gcm_defaultSenderId">421150332…</string>
<string name="project_id">notes-…</string>
<string name="google_storage_bucket">notes-…</string>
```
2. Дизассемблируем приложение, которое будет проверять доступность сервисов с помощью команды:
```
apktool d app-release.apk
```

3. Переходим в сгенерированную командой выше папку и меняем наши ресурсы в файле strings.xml на полученные в 1 пункте:
```
cd app-release/res/values
```

4. Обратно собираем приложение с помощью команды (возможно придется немного пострадать с ресурсами из-за apktool):
```
apktool b app-release (это наша папка)
```

5. Находим новый apk:
```
cd app-release/dist/app-release.apk
```

6. Скачиваем [uber-apk-signer.jar](https://github.com/patrickfav/uber-apk-signer/) 

7. Подписываем сборку:
```
java -jar uber-apk-signer.jar -a /app-release/dist/app-release.apk --allowResign
```
