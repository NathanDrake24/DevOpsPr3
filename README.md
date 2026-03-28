# DevOpsPr3
## Вариант №3

1. Создаем рабочую папку
<img width="321" height="21" alt="image" src="https://github.com/user-attachments/assets/b70bb8c8-0cac-4194-b1b0-1e1876a739e0" />

2. Переходим в нее
<img width="300" height="20" alt="image" src="https://github.com/user-attachments/assets/28fc63b9-82ed-4167-b23a-0a02e0e3f080" />

3. Создаем файл download.sh
<img width="409" height="17" alt="image" src="https://github.com/user-attachments/assets/6d804c34-4643-4029-8093-21098437b96a" />

4. Вставляем в него скрипт

```bash
#!/bin/bash
URL="https://jsonplaceholder.typicode.com/posts/1"
OUTPUT_DIR="./downloads"
LOG_FILE="download_errors.log"
TIMESTAMP=$(date +"%Y-%m-%d-%H-%M-%S")
FILENAME="downloaded-file-${TIMESTAMP}.json"
FILE_PATH="${OUTPUT_DIR}/${FILENAME}"
mkdir -p "$OUTPUT_DIR"
echo "Загрузка $URL ..."
HTTP_STATUS=$(curl -s -o "$FILE_PATH" -w "%{http_code}" "$URL")
if [ "$HTTP_STATUS" -eq 200 ]; then
    echo "✅ Файл успешно скачан: $FILE_PATH (статус: $HTTP_STATUS)"
    echo "Содержимое файла (первые 5 строк):"
    head -n 5 "$FILE_PATH"
else
    echo "❌ Ошибка загрузки!" | tee -a "$LOG_FILE"
    echo "URL: $URL | Статус: $HTTP_STATUS | Дата: $(date)" >> "$LOG_FILE"
    rm -f "$FILE_PATH"
    exit 1
fi
```

<img width="619" height="327" alt="image" src="https://github.com/user-attachments/assets/0f131457-e282-4b4d-a447-288c523412ca" />


6. Проверяем, что файл в папке
<img width="412" height="50" alt="image" src="https://github.com/user-attachments/assets/782a1457-9c08-4f22-954e-4ff5a49e5adb" />

7. Делаем скрипт исполняемым

<img width="438" height="20" alt="image" src="https://github.com/user-attachments/assets/4990476f-2728-4b0f-907a-520c0d3c0ef5" />

8. Запускаем скрипт

<img width="960" height="193" alt="image" src="https://github.com/user-attachments/assets/eb004b2a-7ccd-40f1-a6fc-364532f0bcac" />

9. Проверяем, что файл сохранился
<img width="654" height="50" alt="image" src="https://github.com/user-attachments/assets/b16e7491-f10f-433e-ad2f-358735e9bf60" />

10. Если была ошибка — смотрим лог
<img width="467" height="36" alt="image" src="https://github.com/user-attachments/assets/4f0ec8b9-bba8-4cc2-9818-3914e11ffeec" />



