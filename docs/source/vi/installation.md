<!--⚠️ Tệp này là Markdown nhưng chứa cú pháp riêng của doc-builder (tương tự MDX),
không phải lúc nào cũng hiển thị đúng trong trình xem Markdown thông thường.
-->

# Cài đặt

Trước khi bắt đầu, bạn cần thiết lập môi trường bằng cách cài đặt các gói phù hợp.

`huggingface_hub` được kiểm thử trên **Python 3.10+**.

## Cài đặt bằng pip

Bạn nên cài đặt `huggingface_hub` trong một [môi trường ảo](https://docs.python.org/3/library/venv.html).
Môi trường ảo giúp bạn quản lý các dự án khác nhau và tránh xung đột giữa các
phụ thuộc.

Tạo môi trường ảo trong thư mục dự án:

```bash
python -m venv .venv
```

Kích hoạt môi trường ảo trên Linux và macOS:

```bash
source .venv/bin/activate
```

Kích hoạt môi trường ảo trên Windows:

```bash
.venv/Scripts/activate
```

Cài đặt `huggingface_hub` [từ kho PyPI](https://pypi.org/project/huggingface-hub/):

```bash
pip install --upgrade huggingface_hub
```

Sau đó, [kiểm tra cài đặt](#check-installation).

### Cài đặt các phụ thuộc tùy chọn

Một số phụ thuộc của `huggingface_hub` là [tùy chọn](https://setuptools.pypa.io/en/latest/userguide/dependency_management.html#optional-dependencies).
Bạn có thể cài đặt chúng bằng `pip`:

```bash
# Cài đặt phụ thuộc cho các tính năng dành cho torch và MCP.
pip install 'huggingface_hub[mcp,torch]'
```

Các phụ thuộc tùy chọn gồm:

- `fastai`, `torch`: chạy các tính năng dành riêng cho framework.
- `dev`: các phụ thuộc để đóng góp cho thư viện, bao gồm kiểm thử, kiểm tra kiểu
  và lint.

### Cài đặt từ mã nguồn

Bạn có thể cài đặt phiên bản `main` mới nhất trực tiếp từ mã nguồn. Phiên bản này
hữu ích khi một bản sửa lỗi đã có trên GitHub nhưng chưa được phát hành chính thức.
Tuy nhiên, phiên bản `main` có thể chưa ổn định hoàn toàn.

```bash
pip install git+https://github.com/huggingface/huggingface_hub
```

Bạn cũng có thể cài đặt một nhánh cụ thể:

```bash
pip install git+https://github.com/huggingface/huggingface_hub@my-feature-branch
```

### Cài đặt editable

```bash
# Clone kho lưu trữ
git clone https://github.com/huggingface/huggingface_hub.git

# Cài đặt ở chế độ editable
cd huggingface_hub
pip install -e .
```

## Cài đặt Hugging Face CLI

Trình cài đặt độc lập cho macOS và Linux:

```bash
curl -LsSf https://hf.co/cli/install.sh | bash
```

Trên Windows:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://hf.co/cli/install.ps1 | iex"
```

Để nâng cấp, chạy `hf update`.

## Cài đặt bằng conda

```bash
conda install -c conda-forge huggingface_hub
```

Sau đó, [kiểm tra cài đặt](#check-installation).

<a id="check-installation"></a>

## Kiểm tra cài đặt

```bash
python -c "from huggingface_hub import model_info; print(model_info('gpt2'))"
```

Lệnh này lấy thông tin về mô hình [gpt2](https://huggingface.co/gpt2) từ Hub.

## Hạn chế trên Windows

`huggingface_hub` hỗ trợ cả hệ thống Unix và Windows, nhưng Windows có một số
hạn chế:

- Hệ thống cache sử dụng symlink để lưu tệp hiệu quả. Trên Windows, bạn cần bật
  Developer Mode hoặc chạy script với quyền quản trị. Nếu không, cache vẫn hoạt
  động nhưng không được tối ưu.
- Đường dẫn trên Hub có thể chứa các ký tự đặc biệt mà Windows không cho phép,
  vì vậy một số tệp có thể không tải xuống được.

Nếu gặp vấn đề chưa được ghi nhận, hãy [mở issue trên GitHub](https://github.com/huggingface/huggingface_hub/issues/new/choose).

## Bước tiếp theo

Sau khi cài đặt, bạn có thể [cấu hình biến môi trường](../en/package_reference/environment_variables)
hoặc xem [các hướng dẫn](guides/overview).
