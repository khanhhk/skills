# Open-Source Agent Skills

Repo này được xây dựng theo hướng open-source để phát triển một bộ **agent skill** có thể mở rộng dần theo nhu cầu thực tế.

Hiện tại repo mới có skill đầu tiên, nhưng định hướng của repo là tiếp tục bổ sung thêm những skill nào thật sự hữu ích trong công việc hằng ngày.

## Tầm nhìn của repo

Mục tiêu của repo là trở thành một nơi lưu trữ các skill cho agent theo hướng:

- Thực dụng
- Dễ mở rộng
- Dễ bảo trì
- Có thể tái sử dụng
- Có ích trong công việc thật

Thay vì viết prompt rời rạc cho từng tác vụ, repo này hướng tới việc đóng gói chúng thành skill có cấu trúc rõ ràng, có quy tắc, có template khi cần, và có thể cải tiến dần theo thời gian.

## Trạng thái hiện tại

Hiện tại repo đang có skill đầu tiên:

- `paper-to-latex-report`: đọc paper và chuyển thành báo cáo LaTeX tiếng Việt nhiều file

Skill này chỉ là điểm khởi đầu để định hình cách tổ chức repo, cách viết `SKILL.md`, cách đặt template, và cách đồng bộ skill giữa các môi trường agent khác nhau.

Trong tương lai, repo có thể có thêm bất kỳ skill nào miễn là nó hữu ích và đáng để chuẩn hóa, ví dụ:

- Xử lý paper
- Dịch thuật
- Tóm tắt tài liệu
- Chuẩn hóa BibTeX
- Tạo báo cáo
- Sinh template
- Kiểm tra cấu trúc tài liệu
- Các workflow cá nhân khác

Repo không tự giới hạn vào một domain cố định.

## Cấu trúc repo hiện tại

```text
.
├── .agents/
│   └── skills/
│       └── paper-to-latex-report/
│           ├── SKILL.md
│           └── templates/
│               └── main.tex
├── .codex/
│   └── skills/
│       └── paper-to-latex-report/
│           ├── SKILL.md
│           └── templates/
│               └── main.tex
└── README.md
```

## Nguyên tắc tổ chức

Repo hiện được tổ chức để một skill có thể tồn tại song song trong hai hệ:

- `.agents/skills/...`
- `.codex/skills/...`

Mục tiêu là giữ logic của skill nhất quán giữa các môi trường chạy agent khác nhau.

Mỗi skill nên có:

- `SKILL.md` để mô tả mục đích, workflow và quy tắc bắt buộc
- `templates/` nếu skill cần skeleton hoặc tài nguyên đi kèm
- Cấu trúc đủ rõ để có thể mở rộng sau này mà không làm skill trở nên mơ hồ

## Skill hiện có

### `paper-to-latex-report`

Skill này dùng để:

- Đọc một research paper
- Hiểu cấu trúc logic của bài báo
- Dịch nội dung sang tiếng Việt theo văn phong học thuật
- Tạo báo cáo LaTeX nhiều file
- Tự sinh `sections/`
- Tự sinh `refs.bib`
- Cập nhật `main.tex` bằng `\input{}` và bibliography

Template mặc định hiện chỉ giữ lại `main.tex`. Agent phải tự tạo các thành phần còn lại trong lúc chạy.

## Quy tắc cốt lõi của skill hiện tại

Skill `paper-to-latex-report` hiện đang được chuẩn hóa với các quy tắc chính sau:

1. Thứ tự đề mục chỉ dùng `\section{}`, `\subsection{}`, `\subsubsection{}`.
2. Mỗi đoạn văn bắt đầu bằng `\noindent`.
3. Khi cần xuống dòng thì dùng `\\`.
4. Không cần xử lý ảnh, hình minh họa, code ví dụ và code minh họa thuật toán.
5. Công thức quan trọng dùng `\begin{equation}...\end{equation}` và để LaTeX tự đánh số.
6. Khi cần tham chiếu công thức, dùng `\label{eq:...}` và `\ref{eq:...}`.
7. Không tự ý dùng `\textbf{}`, `\textit{}`, `\emph{}` nếu không có lý do kỹ thuật rõ ràng.

Các quy tắc này hiện được ghi trong:

- [`.agents/skills/paper-to-latex-report/SKILL.md`](.agents/skills/paper-to-latex-report/SKILL.md)
- [`.codex/skills/paper-to-latex-report/SKILL.md`](.codex/skills/paper-to-latex-report/SKILL.md)

