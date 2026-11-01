# VTV Grid cho Android TV box (bản 1.4.0)

Chức năng giống bản LG webOS 1.4.0: lưới kênh 4 cột, OK để xem, mũi tên lên/xuống để chuyển kênh,
phím số để nhảy kênh, Back/OK để về danh sách, tự lấy tên kênh vtvgo, không có dòng trạng thái / mã phím.

## 1. Đặt file danh sách kênh (chỉ một vị trí duy nhất)

    /sdcard/Android/data/com.vtv.grid/files/channels.txt

(trong bộ nhớ trong của box, thường là /storage/emulated/0/Android/data/com.vtv.grid/files/channels.txt)

- Mở app một lần: app tự tạo thư mục này và chép file mẫu vào đó. Chỉ việc thay bằng file của bạn.
- Chép file bằng: ADB (`adb push channels.txt /sdcard/Android/data/com.vtv.grid/files/channels.txt`),
  hoặc trình quản lý file trên box (một số box Android 11+ chặn thư mục Android/data, khi đó dùng ADB).
- Nếu không đọc được file, màn hình sẽ hiện đúng đường dẫn app đang tìm.

## 2. Build ra APK

### Cách A: không cần cài gì (GitHub)
1. Tạo repo mới trên GitHub, tải toàn bộ thư mục này lên (giữ nguyên thư mục .github).
2. Vào tab Actions, chạy "Build APK" (hoặc tự chạy sau khi push).
3. Khi xong, tải artifact `VTVGrid-apk` về, giải nén ra `app-debug.apk`.

### Cách B: Android Studio
1. File > Open, chọn thư mục này, đợi Gradle đồng bộ (cần JDK 17, Android Studio tự có).
2. Build > Build Bundle(s) / APK(s) > Build APK(s).
3. File nằm tại `app/build/outputs/apk/debug/app-debug.apk`.

### Cách C: dòng lệnh
    gradle assembleDebug        (Gradle 8.7, JDK 17, Android SDK 34)

## 3. Cài lên box
Chép `app-debug.apk` vào box rồi cài (bật "Cài đặt từ nguồn không xác định"), hoặc `adb install app-debug.apk`.
Nếu box có màn hình Android TV, app hiện trong danh sách ứng dụng (có banner); box thường thì nằm trong "Ứng dụng".

## Ghi chú
- Video phát bằng thẻ video của Android System WebView. Box có WebView quá cũ có thể không phát được HLS;
  cập nhật "Android System WebView" nếu gặp tình trạng này.
- Phím CH+/CH- trên remote (nếu có) hoạt động như mũi tên lên/xuống khi đang xem.
