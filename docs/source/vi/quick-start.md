<!--⚠️ Tệp này là Markdown nhưng chứa cú pháp riêng của doc-builder (tương tự MDX),
không phải lúc nào cũng hiển thị đúng trong trình xem Markdown thông thường.
-->

# Bắt đầu nhanh

[Hugging Face Hub](https://huggingface.co/) là nơi chia sẻ mô hình, bản demo, tập
dữ liệu và các chỉ số máy học. Thư viện `huggingface_hub` giúp bạn tương tác với
Hub ngay trong môi trường phát triển. Bạn có thể dễ dàng tạo và quản lý kho lưu
trữ, tải lên và tải xuống tệp, cũng như lấy siêu dữ liệu về mô hình và tập dữ liệu.

## Cài đặt

```bash
pip install --upgrade huggingface_hub
```

Xem thêm trong [hướng dẫn cài đặt](installation).

> [!TIP]
> `huggingface_hub` cũng cung cấp [CLI `hf`](../en/guides/cli) để tương tác với Hub
> trực tiếp từ terminal. Nếu bạn sử dụng AI agent như Claude Code, Codex hoặc
> Cursor, hãy cài đặt Skill để agent sử dụng CLI:
>
> ```bash
> hf skills add
> ```
>
> Xem [hướng dẫn Hugging Face CLI cho AI agent](https://huggingface.co/docs/hub/agents-cli).

## Tải tệp xuống

Các kho lưu trữ trên Hub được quản lý phiên bản bằng git. Bạn có thể tải một tệp
hoặc toàn bộ kho lưu trữ bằng hàm [`hf_hub_download`]. Tệp được tải xuống và lưu
vào cache cục bộ để những lần sau không phải tải lại.

Bạn cần biết ID kho lưu trữ và tên tệp. Ví dụ, tải tệp cấu hình của mô hình
[Pegasus](https://huggingface.co/google/pegasus-xsum):

```py
>>> from huggingface_hub import hf_hub_download
>>> hf_hub_download(repo_id="google/pegasus-xsum", filename="config.json")
```

Để tải một phiên bản cụ thể, truyền tên nhánh, thẻ hoặc mã commit vào `revision`.
Nếu dùng mã commit, phải dùng mã đầy đủ thay vì dạng rút gọn 7 ký tự:

```py
>>> from huggingface_hub import hf_hub_download
>>> hf_hub_download(
...     repo_id="google/pegasus-xsum",
...     filename="config.json",
...     revision="4d33b01d79672f27f001f6abade33f22d993b151"
... )
```

Xem thêm tùy chọn trong tài liệu tham khảo API của [`hf_hub_download`].

<a id="login"></a>

## Xác thực

Bạn thường cần đăng nhập để tải kho riêng tư, tải tệp lên hoặc tạo pull request.
Nếu chưa có tài khoản, hãy [tạo tài khoản](https://huggingface.co/join).

### Đăng nhập bằng lệnh

Cách dễ nhất để xác thực là dùng lệnh [`login`]:

```bash
hf auth login
```

Nếu đã đăng nhập, lệnh sẽ kết thúc ngay. Để đăng nhập lại, dùng
`hf auth login --force`. Nếu chưa đăng nhập, bạn sẽ được hướng dẫn mở URL, nhập
mã ngắn và phê duyệt yêu cầu. Token được lưu trong thư mục `HF_HOME` (mặc định là
`~/.cache/huggingface/token`) và tự động làm mới khi bạn tiếp tục sử dụng.

Bạn cũng có thể dùng [User Access Token](https://huggingface.co/docs/hub/security-tokens)
từ [trang Settings](https://huggingface.co/settings/tokens).

> [!TIP]
> Token có quyền `read` hoặc `write`. Chỉ dùng token `write` khi cần tạo hoặc sửa
> kho lưu trữ; nếu không, token `read` sẽ an toàn hơn.

Đăng nhập trong notebook hoặc script:

```py
>>> from huggingface_hub import login
>>> login()
```

Bạn chỉ có thể đăng nhập một tài khoản tại một thời điểm. Chạy
`hf auth whoami` để xem tài khoản đang hoạt động.

> [!WARNING]
> Sau khi đăng nhập, các request sẽ mặc định sử dụng token của bạn. Để tắt việc
> tự động gửi token, đặt `HF_HUB_DISABLE_IMPLICIT_TOKEN=1` (xem [tài liệu biến môi trường](../en/package_reference/environment_variables#hfhubdisableimplicittoken)).

### Quản lý nhiều token cục bộ

Bạn có thể lưu nhiều token bằng cách đăng nhập với từng token. Để chuyển đổi,
dùng:

```bash
hf auth switch
```

Để liệt kê các token đã lưu, chạy `hf auth list`.

### Biến môi trường

Bạn cũng có thể đặt biến môi trường `HF_TOKEN`, đặc biệt hữu ích khi đặt token
như một [Space secret](https://huggingface.co/docs/hub/spaces-overview#managing-secrets).
Biến môi trường hoặc secret có ưu tiên cao hơn token được lưu trên máy.

### Tham số của phương thức

Bạn có thể truyền token vào các phương thức nhận tham số `token`:

```py
from huggingface_hub import whoami

user = whoami(token=...)
```

Không nên hardcode token trong mã nguồn hoặc notebook. Hãy tải token từ một kho
secrets an toàn để tránh rò rỉ.

## Tạo kho lưu trữ

Sau khi đăng ký và đăng nhập, tạo kho bằng hàm [`create_repo`]:

```py
>>> from huggingface_hub import HfApi
>>> api = HfApi()
>>> api.create_repo(repo_id="super-cool-model")
```

Để tạo kho riêng tư:

```py
>>> from huggingface_hub import HfApi
>>> api = HfApi()
>>> api.create_repo(repo_id="super-cool-model", private=True)
```

Kho riêng tư chỉ hiển thị với bạn.

> [!TIP]
> Bạn cần User Access Token có quyền `write` để tạo kho hoặc đẩy nội dung lên Hub.

## Tải tệp lên

Dùng hàm [`upload_file`] và chỉ định:

1. Đường dẫn tệp cần tải lên.
2. Đường dẫn của tệp trong kho.
3. ID của kho đích.

```py
>>> from huggingface_hub import HfApi
>>> api = HfApi()
>>> api.upload_file(
...     path_or_fileobj="/home/lysandre/dummy-test/README.md",
...     path_in_repo="README.md",
...     repo_id="lysandre/test-model",
... )
```

Để tải nhiều tệp, xem [hướng dẫn Upload](../en/guides/upload).

## Bước tiếp theo

Bạn có thể đọc các [hướng dẫn thực hành](../en/guides/overview) để:

- [Quản lý kho lưu trữ](../en/guides/repository).
- [Tải tệp xuống](../en/guides/download).
- [Tải tệp lên](../en/guides/upload).
- [Tìm kiếm Hub](../en/guides/search).
- [Chạy Inference](../en/guides/inference) trên các mô hình được triển khai.
