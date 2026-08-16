# chinese-chess-web

Trang giới thiệu cho app **PHÁO đầu** — game cờ tướng tiếng Việt.
Phục vụ qua GitHub Pages tại **https://mittohoa.github.io/chinese-chess-web/**

<img src="anh/logo.png" width="96" alt="logo PHÁO đầu">

Tên app lấy từ **pháo đầu** trong cờ tướng: đưa Pháo về cột giữa, nhắm thẳng
vào Tướng đối phương — khai cuộc phổ biến nhất của cờ tướng. Cùng khuôn đặt tên
với app cờ vua [TỐT thí](https://mittohoa.github.io/chess-game-web/).

Repo này **chỉ chứa trang web và các bản phát hành**. Mã nguồn app nằm ở repo
riêng và không công khai.

## Vì sao tách khỏi repo mã nguồn

GitHub Pages phục vụ mọi tệp trong repo cho bất kỳ ai. Để trang giới thiệu công
khai mà mã nguồn vẫn riêng tư, hai thứ phải nằm ở hai repo khác nhau. Bản phát
hành treo ở đây để ai cũng tải được mà không cần tài khoản GitHub.

## Cấu trúc

```
index.html      # trang giới thiệu, không phụ thuộc thư viện ngoài
rieng-tu.html   # chính sách quyền riêng tư
anh/            # ảnh chụp màn hình và logo
choi-thu/       # bản web chơi thử ngay trên trình duyệt
```

Trang tự chứa hoàn toàn: không CDN, không phông tải về, không script theo dõi.
Mở thẳng `index.html` bằng trình duyệt là xem được.

## Cập nhật bản chơi thử

Ở repo mã nguồn, dựng bản web **kèm đúng đường dẫn con**:

```powershell
flutter build web --release --base-href "/chinese-chess-web/choi-thu/"
```

> ⚠️ Quên `--base-href` là hỏng câm: trang quay mãi không tải xong, mà kiểm bằng
> HTTP thì mọi tệp đều trả 200 nên không ai thấy. Kiểm ngay sau khi dựng:
> `Select-String -Path build\web\index.html -Pattern "base href"`.
>
> Trên Windows phải truyền cờ này qua **PowerShell**, không qua Git Bash — Git
> Bash biến `/chinese-chess-web/...` thành đường dẫn Windows.

Rồi chép sang đây:

```powershell
Copy-Item -Recurse -Force build\web\* ..\chinese-chess-web\choi-thu
```

## Ảnh từ đâu ra

`anh/logo.png` **được sinh từ chính mã nguồn app**, nên không bao giờ lệch với
biểu tượng thật. Ở repo mã nguồn chạy:

```powershell
flutter test tool/generate_icons_test.dart
```

Các ảnh còn lại là **ảnh chụp từ bản 0.3.0 chạy trên máy Android**, không dựng
lại bằng công cụ đồ hoạ. Việc còn treo: làm một công cụ dựng ảnh từ mã nguồn
(kiểu `design_preview_test.dart` của repo cờ vua) để ảnh tự cập nhật theo giao
diện.

## Phát hành bản mới

```powershell
gh release create v0.4.0 phao-dau-0.4.0.apk `
  -R mittohoa/chinese-chess-web `
  --title "PHÁO đầu 0.4.0 — <câu ngắn>" `
  -F ghi-chu.md
```

Ghi chú phát hành viết cho **người dùng**, không phải cho lập trình viên: mỗi
tính năng nói rõ **nó nằm ở đâu trong app**, và nói cả giới hạn lẫn phần chưa
làm.

## Liên hệ

mittohoa@gmail.com
