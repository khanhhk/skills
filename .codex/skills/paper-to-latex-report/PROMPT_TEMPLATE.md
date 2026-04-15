# Prompt Template

Sao chép prompt dưới đây và thay các placeholder bằng thông tin thực tế trước khi dùng.

```text
Đọc kỹ paper được cung cấp tại: {{PAPER_PATH_OR_DESCRIPTION}}

Mục tiêu:
- Chuyển paper thành báo cáo LaTeX tiếng Việt dạng multi-file.
- Thư mục đích: {{OUTPUT_ROOT}}
- File khung đã có: {{OUTPUT_ROOT}}/templates/main.tex

Yêu cầu bắt buộc:
- Đọc toàn bộ paper trước khi bắt đầu tách section.
- Chỉ tạo `\section{}`, `\subsection{}`, `\subsubsection{}` khi paper gốc thực sự có heading tương ứng.
- Không tự nâng các nhãn inline như `Case 1:`, `Datasets and Models.`, `Baselines and Evaluation.` thành heading LaTeX.
- Giữ tiêu đề bài báo bằng tiếng Anh trong `\title{}`.
- Không tạo `\author{}` nếu tôi không yêu cầu rõ.
- Nếu dùng `\begin{abstract}...\end{abstract}`, phần này chỉ chứa nội dung abstract.
- Không đưa `keywords`, `index terms`, affiliation, submission metadata, hoặc front-matter khác vào abstract.
- Mọi đoạn văn thường phải bắt đầu bằng `\noindent`.
- Khi cần ngắt dòng hoặc tạo text break hiển thị rõ ràng, dùng `\\`.
- Không dùng quy ước xuống dòng khác thay cho `\\` trong các vị trí cần break tường minh.
- Bảo toàn các phương trình quan trọng bằng môi trường `equation`.
- Không đánh số phương trình thủ công.
- Nếu cần tham chiếu phương trình, dùng `\label{eq:...}` và gọi lại bằng `\eqref{...}`.
- Không dùng `\ref{}` để tham chiếu phương trình.
- Không thêm `\textbf{}`, `\textit{}`, hoặc `\emph{}` nếu không có lý do kỹ thuật bắt buộc.
- Bỏ qua hình, minh họa, code demo, và algorithm demonstration code từ paper gốc.
- Tạo `templates/sections/` nếu chưa tồn tại.
- Tách nội dung thành các file `.tex` hợp lý trong `templates/sections/`.
- Cập nhật `templates/main.tex` bằng các dòng `\input{sections/...}` theo đúng thứ tự đọc.
- Nếu paper có tài liệu tham khảo, tạo `templates/refs.bib` với các BibTeX entry cần thiết.
- Thêm khối thư mục tham khảo sau vào cuối `main.tex` nếu chưa có:
  `\bibliographystyle{plain}`
  `\bibliography{refs}`
- Văn phong phải là tiếng Việt học thuật, trung tính, đúng nghĩa kỹ thuật, không tự thêm diễn giải ngoài paper.

Đầu ra mong muốn:
- `templates/main.tex` được cập nhật hoàn chỉnh.
- `templates/sections/*.tex` được tạo theo cấu trúc nội dung của paper.
- `templates/refs.bib` được tạo nếu cần.

Trước khi kết thúc, tự kiểm tra lại toàn bộ đầu ra theo checklist sau:
1. `\title{}` đã giữ bằng tiếng Anh chưa?
2. Có lỡ sinh `\author{}` dù không được yêu cầu không?
3. `abstract` có chứa keywords, metadata, affiliation, hoặc nội dung không liên quan không?
4. Mọi đoạn văn thường đã bắt đầu bằng `\noindent` chưa?
5. Những vị trí cần ngắt dòng tường minh đã dùng `\\` chưa?
6. Mọi tham chiếu phương trình đã dùng `\eqref{}` chưa?
7. Có chỗ nào dùng `\ref{}` cho phương trình không?
8. Có đưa hình hoặc code demo từ paper vào báo cáo không?
9. Tất cả file section đã được `\input{}` từ `main.tex` chưa?
10. `refs.bib` đã được tạo nếu paper có reference list chưa?
11. Có tự sinh heading cấp `section/subsection/subsubsection` nào mà paper gốc không có không?

Khi hoàn tất, chỉ báo cáo ngắn gọn:
- các file đã tạo/cập nhật
- các giả định quan trọng đã dùng
- các mục bị lược bỏ theo rule (nếu có)
```

## Placeholder Guide

- `{{PAPER_PATH_OR_DESCRIPTION}}`: đường dẫn file PDF, nội dung paper, hoặc mô tả nguồn đầu vào.
- `{{OUTPUT_ROOT}}`: thư mục gốc chứa `templates/main.tex`.

## Recommended Use

- Dùng nguyên prompt khi muốn output ổn định giữa nhiều lần chạy.
- Nếu có yêu cầu riêng của từng paper, thêm chúng dưới prompt này thay vì sửa các rule cốt lõi.
