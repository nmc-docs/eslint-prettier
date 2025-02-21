---
sidebar_position: 1
slug: /
---

# Giới thiệu về ESLint, Prettier, Lint-staged, Husky

## ESLint là gì ?

- ESLint là một công cụ mã nguồn mở dùng để kiểm tra mã JavaScript/TypeScript và báo các lỗi cú pháp, sai sót, vi phạm quy tắc lập trình, hoặc tiềm ẩn các vấn đề khác. Nó cho phép người dùng tùy chỉnh các quy tắc kiểm tra và thực thi chúng trong các quy trình kiểm tra trước khi triển khai mã của họ.
- Sự khác biệt giữa cấu hình **extends** với **plugins**:

| Đặc điểm          | `extends`                                                       | `plugins`                                                                     |
| ----------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Mục đích**      | Kế thừa cấu hình ESLint có sẵn                                  | Đăng ký các plugin để dùng các quy tắc tùy chỉnh                              |
| **Tác dụng**      | Tự động kích hoạt các quy tắc của cấu hình kế thừa              | Chỉ đăng ký plugin, không tự động kích hoạt quy tắc                           |
| **Cách dùng**     | `"extends": ["eslint:recommended", "plugin:react/recommended"]` | `"plugins": ["react"]`, sau đó phải khai báo `rules`                          |
| **Khi nào dùng?** | Khi muốn kế thừa và sử dụng ngay bộ quy tắc có sẵn              | Khi cần thêm quy tắc từ plugin nhưng không muốn dùng toàn bộ thiết lập sẵn có |

👉 **Tóm lại:**

- Nếu muốn sử dụng một bộ quy tắc ESLint có sẵn, hãy dùng `extends`.
- Nếu muốn tự tùy chỉnh quy tắc từ một plugin, hãy dùng `plugins` kết hợp với `rules`.

## Prettier là gì ?

- Prettier là một công cụ định dạng mã nguồn tự động. Nó giúp định dạng code một cách tự động, không cần phải bấm nhiều phím tắt hoặc chỉnh sửa thủ công, giúp tiết kiệm thời gian và giảm các tranh cãi về việc định dạng code.

## Lint-staged là gì ?

- Nếu ta chạy lệnh để ESLint check cú pháp hoặc lệnh để Prettier format code, thì chúng sẽ được chạy trên toàn bộ source code của chúng ta, mà nếu ta sửa có mỗi 1 file, các file còn lại thì đã được format sẵn từ lần commit trước rồi. Điều này dẫn tới việc ta phải tốn thêm thời gian chờ đợi, và nó là thừa thãi.
- Do vậy lint-staged cho phép ta thực hiện một hoặc một số công việc **chỉ** với những file được git staged, hiểu đơn giản là những file vừa được thêm vào hoặc có sự thay đổi ở thời điểm hiện tại.

## Husky là gì ?

- Husky là một công cụ giúp thực hiện các hành động trước khi commit hoặc push code lên Git. Nó cho phép bạn định nghĩa các lệnh tùy ý để thực thi trước khi thực hiện commit hoặc push. Ví dụ, bạn có thể sử dụng Husky để chạy các linter (như ESLint hoặc Prettier) trên mã của mình trước khi commit hoặc push lên Git để đảm bảo rằng mã của bạn đáp ứng được các quy chuẩn của dự án.
