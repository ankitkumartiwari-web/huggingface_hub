<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://huggingface.co/datasets/huggingface/documentation-images/raw/main/huggingface_hub-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://huggingface.co/datasets/huggingface/documentation-images/raw/main/huggingface_hub.svg">
    <img alt="huggingface_hub library logo" src="https://huggingface.co/datasets/huggingface/documentation-images/raw/main/huggingface_hub.svg" width="352" height="59">
  </picture>
</p>

<p align="center">
    <i>CLI và thư viện Python chính thức cho Hugging Face Hub.</i>
</p>

<p align="center">
    <a href="https://huggingface.co/docs/huggingface_hub/vi/index">Tài liệu</a> ·
    <a href="https://github.com/huggingface/huggingface_hub">Mã nguồn</a>
</p>

<h4 align="center">
    <p>
        <a href="https://github.com/huggingface/huggingface_hub/blob/main/README.md">English</a> |
        <b>Tiếng Việt</b> |
        <a href="https://github.com/huggingface/huggingface_hub/blob/main/i18n/README_de.md">Deutsch</a> |
        <a href="https://github.com/huggingface/huggingface_hub/blob/main/i18n/README_fr.md">Français</a>
    </p>
</h4>

## Bắt đầu nhanh

Cài đặt [`hf` CLI](https://huggingface.co/docs/huggingface_hub/vi/guides/cli):

```bash
pip install huggingface_hub
```

Đăng nhập rồi bắt đầu sử dụng Hub:

```bash
hf auth login
hf download Qwen/Qwen3-0.6B
hf upload username/my-cool-model ./model.safetensors
hf --help
```

Hub dùng token để xác thực ứng dụng. Xem [tài liệu về token](https://huggingface.co/docs/hub/security-tokens)
và [hướng dẫn CLI](https://huggingface.co/docs/huggingface_hub/vi/guides/cli).

## `huggingface_hub` là gì?

Thư viện `huggingface_hub` cho phép bạn tương tác với
[Hugging Face Hub](https://huggingface.co/), nền tảng chia sẻ máy học mã nguồn mở
dành cho người sáng tạo và cộng tác viên. Bạn có thể khám phá mô hình, tập dữ
liệu và ứng dụng máy học, hoặc tạo và chia sẻ tài nguyên của mình với cộng đồng.

Bạn có thể:

- [Tải tệp xuống](https://huggingface.co/docs/huggingface_hub/en/guides/download).
- [Tải tệp lên](https://huggingface.co/docs/huggingface_hub/en/guides/upload).
- [Quản lý kho lưu trữ](https://huggingface.co/docs/huggingface_hub/en/guides/repository).
- [Chạy Inference](https://huggingface.co/docs/huggingface_hub/en/guides/inference).
- [Tìm kiếm](https://huggingface.co/docs/huggingface_hub/en/guides/search) mô hình,
  tập dữ liệu và Space.
- [Chia sẻ Model Card](https://huggingface.co/docs/huggingface_hub/vi/guides/model-cards).

## Cài đặt

```bash
pip install huggingface_hub
```

Xem [hướng dẫn cài đặt](https://huggingface.co/docs/huggingface_hub/vi/installation)
để biết thêm về conda, mã nguồn và các phụ thuộc tùy chọn.

## Ví dụ Python

### Tải tệp

```py
from huggingface_hub import hf_hub_download

hf_hub_download(repo_id="zai-org/GLM-5.2", filename="config.json")
```

### Tạo kho

```py
from huggingface_hub import create_repo

create_repo(repo_id="super-cool-model")
```

### Tải tệp lên

```py
from huggingface_hub import upload_file

upload_file(
    path_or_fileobj="/home/lysandre/dummy-test/README.md",
    path_in_repo="README.md",
    repo_id="lysandre/test-model",
)
```
