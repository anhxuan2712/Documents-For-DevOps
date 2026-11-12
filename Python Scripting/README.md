# GIÁO TRÌNH PYTHON SCRIPTING THỰC CHIẾN DÀNH CHO DEVOPS / PLATFORM / SRE
*Viết script đúng, an toàn, kiểm thử được — Tự động hóa hạ tầng thật — Vận hành Production & Phỏng vấn Junior/Mid*

---

## 🎯 CÁCH DÙNG TÀI LIỆU NÀY

* **Đối tượng:** Người mới vào DevOps/Platform/SRE. **Không yêu cầu kinh nghiệm lập trình trước đó**, chỉ cần đã biết dùng terminal Linux (xem giáo trình Hệ điều hành, Module 0–3). Giáo trình đi từ "in ra màn hình dòng đầu tiên" đến một công cụ kiểm tra hạ tầng hoàn chỉnh có test, đóng gói và chạy theo lịch.
* **Đây là README (khung giáo trình):** gồm lộ trình, mục lục chi tiết, bài lab và case study cho từng module. Nội dung chi tiết từng module sẽ được viết thành file riêng theo cùng cấu trúc 10 mục (mục tiêu, vấn đề thực tế, nguyên lý, chi tiết kỹ thuật, lệnh/code thực hành, lab, case study, hiểu lầm phổ biến, câu hỏi tự kiểm tra, tóm tắt và cheat sheet).
* **Cách học hiệu quả:** học theo vòng **đọc ngắn → tự gõ code → chạy → cố ý làm hỏng → sửa**. Đừng chỉ đọc hoặc copy-paste: lập trình là kỹ năng tay. Mỗi module có bài lab; hãy làm xong lab rồi mới đọc phần case study.
* **Môi trường lab khuyến nghị:**
  * 1 máy ảo Linux (Ubuntu Server LTS 24.04 hoặc 26.04), có `sudo`, cài `python3-venv` (xem giáo trình Hệ điều hành, Module 10). Editor: VS Code kèm extension Python, hoặc `vim`/`nano` trên server.
  * Docker (cho Module 6, 11, 13) và `kind` (Kubernetes trong Docker, cho Module 7, 13).
  * Với cloud: dùng `moto` hoặc LocalStack để giả lập, hoặc một **tài khoản sandbox riêng** có cảnh báo ngân sách. **Không chạy lab trên tài khoản hoặc máy production.**
* **Quy ước nhãn:** `[Mở rộng]` = đọc lướt, tra khi cần. `[CẦN XÁC MINH]` = thông tin phụ thuộc phiên bản, hãy đối chiếu tài liệu chính thức hoặc chạy thử trước khi tin. Các thư viện **ngoài thư viện chuẩn** (như `requests`, `PyYAML`, `boto3`, `pytest`) cần cài bằng `pip` trong môi trường ảo (xem Mục 0.4).
* **Về phiên bản Python (tham chiếu tháng 11/2026):**
  * Python ra bản mới mỗi năm vào tháng 10, mỗi bản được hỗ trợ khoảng 5 năm. **3.10 đã hết vòng đời** (bản cuối cùng 3.10.22 ngày 01/10/2026). 3.11 hỗ trợ đến 10/2027, 3.12 đến 10/2028, 3.13 đến 10/2029, 3.14 (phát hành 07/10/2025) đến 10/2030. **3.15 phát hành ngày 09/10/2026**.
  * Khuyến nghị cho người học: luyện trên **Python 3.13 hoặc 3.14**. Với 3.15 mới ra, nhiều thư viện có thể chưa có bản tương thích, hãy kiểm tra trước khi dùng cho production.
  * Phiên bản `python3` mặc định khác nhau theo hệ điều hành (ví dụ Ubuntu 24.04 thường là 3.12, Debian 12 là 3.11, RHEL 9 là 3.9) [CẦN XÁC MINH trên máy bạn bằng `python3 --version`]. Điều này quan trọng khi chạy script trên server (xem Mục 0.2).

---

## 🧭 LỘ TRÌNH HỌC TẬP ĐỀ XUẤT

### 1. LỘ TRÌNH TẬP TRUNG 4 TUẦN (toàn thời gian, ước tính khoảng 60–100 giờ)

```
[Tuần 1: Nền tảng ngôn ngữ, Hàm, Lỗi & Logging (~15.500 từ)]
  Module 0 → Module 1 → Module 2 → Module 3

[Tuần 2: File, CLI, HTTP API & Hạ tầng (SSH/Docker/K8s/Cloud) (~17.500 từ)]
  Module 4 → Module 5 → Module 6 → Module 7

[Tuần 3: OOP, Đồng thời, Kiểm thử & Đóng gói (~15.500 từ)]
  Module 8 → Module 9 → Module 10 → Module 11

[Tuần 4: Bảo mật, Dự án tổng hợp & Mở rộng (~9.000 từ)]
  Module 12 → Module 13 (Dự án) → Module 14 (Phụ lục)
```

*Tuần 4 nhẹ hơn về lý thuyết để dành thời gian cho Module 13 (hoàn thiện dự án `infra-audit` từ đầu đến khi chạy được theo lịch), vì làm một dự án trọn vẹn dạy nhiều hơn đọc thêm.*

### 2. LỘ TRÌNH BÁN THỜI GIAN 10–12 TUẦN (8–10 giờ/tuần)

| Tầng Ưu Tiên | Danh Sách Module | Hướng Dẫn Tiếp Cận |
| :--- | :--- | :--- |
| **Tầng 1: Cốt lõi** | **Module 0, 1, 2, 3, 4, 5, 6, 7** | Học kỹ, làm đủ 100% bài lab. Đây là phần dùng hằng ngày khi viết script vận hành: ngôn ngữ, lỗi, file, CLI, API và SDK hạ tầng. |
| **Tầng 2: Quan trọng** | **Module 8, 9, 10, 11, 12, 13** | Đọc kỹ nguyên lý, làm các lab chọn lọc, riêng Module 13 (dự án tổng hợp) nên làm đầy đủ. |
| **Tầng 3: Mở rộng** | **Module 14 (Phụ lục)** và các mục gắn nhãn `[Mở rộng]` | Đọc lướt nắm khái niệm, tra cứu khi cần hoặc khi phỏng vấn chuyên sâu. |

### 3. LIÊN HỆ VỚI CÁC GIÁO TRÌNH KHÁC TRONG BỘ NỀN TẢNG DEVOPS

* **Hệ điều hành (Linux):** Python script chạy *trên* hệ điều hành, nên các kiến thức về quyền file, tiến trình, tín hiệu, systemd, cron, cgroup ở giáo trình Hệ điều hành là nền tảng. Các chỗ liên quan được ghi rõ dưới dạng "giáo trình Hệ điều hành, Mục X.Y".
* **Mạng máy tính:** Module 6 và 9 dùng kiến thức HTTP, TLS, DNS, TCP (timeout, keepalive, TIME_WAIT). Các chỗ liên quan được ghi dưới dạng "giáo trình Mạng máy tính, Mục X.Y".
* **Build tools / package manager:** Phần quản lý gói Python (`pip`, môi trường ảo, đóng gói) ở Module 0 và Module 11 chỉ lấy mức đủ dùng cho script vận hành; nếu cần đào sâu hãy đọc song song giáo trình Build tools.

---

## 📋 MỤC LỤC CHI TIẾT

---

### MODULE 0: PYTHON TRONG CÔNG VIỆC DEVOPS & MÔI TRƯỜNG LÀM VIỆC
*Ước lượng: ~3.000 từ*
*🎯 Học xong làm được: chọn đúng khi nào dùng Bash hay Python, dựng môi trường ảo sạch, chạy script bằng đúng interpreter và không phá Python của hệ thống.*

* **0.1. Python dùng để làm gì trong DevOps, và khi nào KHÔNG dùng**
  * Các nhóm việc: keo dán giữa các hệ thống (gọi API), xử lý dữ liệu cấu hình/log, công cụ nội bộ (CLI), kiểm thử hạ tầng, exporter/webhook nhỏ, mở rộng công cụ có sẵn (Ansible module, operator Kubernetes).
  * Quy tắc ngón tay cái chọn Bash hay Python: Bash khi chỉ nối vài lệnh có sẵn và script ngắn; Python khi cần cấu trúc dữ liệu (JSON/YAML), gọi API, xử lý lỗi rõ ràng, kiểm thử, hoặc script đã dài và phức tạp (xem giáo trình Hệ điều hành, Mục 2.5).
* **0.2. Interpreter, phiên bản và vòng đời**
  * CPython là bản chuẩn; Python 2 đã hết hỗ trợ từ 2020. Lịch phát hành hằng năm, hỗ trợ 5 năm (xem phần "Về phiên bản Python" ở đầu tài liệu).
  * `python3 --version`, `which python3`, chạy song song nhiều bản (`python3.12`, `python3.13`). Python **của hệ thống** (phục vụ các công cụ hệ điều hành) khác với Python **của bạn**.
  * Khai báo yêu cầu phiên bản (`requires-python`, xem Mục 11.1) và kiểm tra phiên bản ngay đầu script khi cần.
* **0.3. Python của hệ thống và PEP 668**
  * Vì sao không `sudo pip install` vào Python hệ thống: dễ làm hỏng công cụ của hệ điều hành.
  * Debian 12, Ubuntu 23.04 trở lên đánh dấu Python hệ thống là "externally managed": `pip install` ngoài môi trường ảo báo lỗi `externally-managed-environment`. Cách xử lý đúng: môi trường ảo (`venv`), `pipx` cho công cụ dòng lệnh, hoặc gói của distro (`apt install python3-<tên>`) [CẦN XÁC MINH hành vi theo distro].
* **0.4. Môi trường ảo (virtual environment) và pip**
  * `python3 -m venv .venv`, kích hoạt (`source .venv/bin/activate`), kiểm tra `which python` và `pip list`, `deactivate`. Trên Debian/Ubuntu cần gói `python3-venv`. Đưa `.venv/` vào `.gitignore`; không commit môi trường ảo.
  * Luôn gọi `python -m pip` để chắc chắn pip thuộc đúng interpreter. `pip install`, `pip uninstall`, `pip list`, `pip show`, `pip freeze`, `pip install -r requirements.txt`, ghim phiên bản `==`.
  * `pipx` để cài công cụ dòng lệnh Python tách biệt. `uv` là công cụ quản lý môi trường/gói tốc độ cao tương thích pip, tùy chọn `[Mở rộng]`.
* **0.5. Các cách chạy code Python**
  * REPL (`python3`), `python script.py`, `python -m module`, `python -c "..."`, shebang `#!/usr/bin/env python3` kèm `chmod +x`, cờ `-u` (không đệm đầu ra, xem Mục 11.4).
* **0.6. Công cụ làm việc và cách tự học**
  * `help()`, `dir()`, `python -m pydoc`, tài liệu tại docs.python.org. Cấu hình VS Code chọn interpreter của `.venv`. Đọc traceback cơ bản: đọc từ dưới lên, dòng cuối là loại lỗi và thông báo (chi tiết ở Mục 3.2).
* **Lab thực hành:** Trên VM sạch: cài `python3-venv`, tạo `.venv`, cài `requests`, viết script 5 dòng in phiên bản Python, đường dẫn interpreter và hostname; chạy bằng 4 cách (`python`, `python -m`, shebang, từ trong và ngoài venv). Cố ý chạy `pip install` ngoài venv để gặp lỗi `externally-managed-environment` rồi giải quyết bằng venv.
* **Case study sự cố:**
  1. *Case 1:* `pip install` báo `externally-managed-environment` trên Ubuntu mới; phản xạ sai là thêm `--break-system-packages`, cách đúng là dùng venv hoặc `pipx`.
  2. *Case 2:* Script chạy tốt trên laptop nhưng lỗi trên server (`ModuleNotFoundError`, hoặc cú pháp mới không chạy), do chạy nhầm `python3` hệ thống, khác phiên bản, hoặc quên kích hoạt venv; chẩn đoán bằng `which python`, `python -m pip list`, `python -c "import sys; print(sys.executable)"`.

---

### MODULE 1: CÚ PHÁP & KIỂU DỮ LIỆU NỀN TẢNG
*Ước lượng: ~4.500 từ*
*🎯 Học xong làm được: viết script xử lý dữ liệu cơ bản bằng chuỗi, list, dict, set và vòng lặp, và tránh được các bẫy tham chiếu/sao chép kinh điển.*

* **1.1. Biến, kiểu dữ liệu và số**
  * Kiểu động, `type()`, `int` (không giới hạn độ lớn), `float` (sai số nhị phân, vì sao `0.1 + 0.2 != 0.3`), `decimal` khi cần chính xác, `bool`, `None`. Toán tử `//`, `%`, `**`, so sánh chuỗi, toán tử logic.
* **1.2. Chuỗi (str) và bytes**
  * Chuỗi là Unicode và bất biến; f-string (định dạng `:.2f`, `:>10`, `=`), `split`/`join`/`strip`/`replace`/`startswith`, cắt lát (slicing), chuỗi thô `r"..."`, chuỗi nhiều dòng.
  * `str` so với `bytes`, `encode`/`decode` (nền cho Mục 4.2). Template string (t-string, Python 3.14) ở phụ lục.
* **1.3. Cấu trúc dữ liệu cốt lõi**
  * `list`, `tuple`, `dict` (giữ thứ tự chèn từ Python 3.7), `set`; thêm/xóa/duyệt, `in`, `len`, `sorted(key=...)`, giải nén (`a, b = ...`, `*rest`, `**kwargs`).
  * Phương thức `dict.get`, `setdefault`, `items`, gộp dict bằng `|`. Độ phức tạp: kiểm tra phần tử trong `list` là O(n), trong `set`/`dict` trung bình O(1), chọn đúng cấu trúc để script không chậm bất thường.
* **1.4. Điều khiển luồng**
  * `if`/`elif`/`else`, giá trị "truthy/falsy" (chuỗi rỗng, list rỗng, `0`, `None` là falsy), `for`, `while`, `break`/`continue`, `range`, `enumerate`, `zip`. Comprehension (list, dict, set). Toán tử `:=` và `match`/`case` (3.10 trở lên) ở mức nhận biết `[Mở rộng]`.
* **1.5. Tham chiếu, khả biến và sao chép**
  * `is` so với `==`; đối tượng khả biến (list, dict, set) so với bất biến (str, tuple, int); sao chép nông và sâu (`copy.copy`, `copy.deepcopy`); bẫy `[[]] * n`; không sửa list trong lúc đang lặp qua nó.
* **1.6. Nhập xuất cơ bản**
  * `print(..., file=sys.stderr)`, `input()`. Phân biệt stdout và stderr, vì sao script vận hành nên ghi thông báo lỗi ra stderr (xem giáo trình Hệ điều hành, Mục 2.3).
* **Lab thực hành:** Viết script đọc một đoạn log truy cập mẫu (dán sẵn trong file), dùng dict đếm số request theo mã HTTP, tìm top 5 IP, in bảng căn cột bằng f-string. So sánh kết quả với pipeline `awk | sort | uniq -c` (giáo trình Hệ điều hành, Mục 2.4).
* **Case study sự cố:**
  1. *Case 1:* Nhân bản cấu hình môi trường bằng sao chép nông (`dict.copy()`) khiến sửa số `replicas` của `staging` làm đổi luôn `production`, do dict lồng nhau dùng chung tham chiếu; sửa bằng `copy.deepcopy`.
  2. *Case 2:* Script sập với `KeyError`/`TypeError: NoneType` khi thiếu biến môi trường hoặc thiếu trường trong file cấu hình; xử lý bằng `.get()` với giá trị mặc định, kiểm tra sớm và thông báo lỗi rõ ràng kèm mã thoát khác 0.

---

### MODULE 2: HÀM, MODULE, PACKAGE & TỔ CHỨC CODE
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: chia script dài thành hàm và package nhỏ có thể tái sử dụng, kiểm thử và chạy bằng `python -m`.*

* **2.1. Hàm**
  * `def`, `return`, tham số vị trí và từ khóa, giá trị mặc định, `*args`/`**kwargs`, tham số chỉ nhận từ khóa (`*`) và chỉ nhận vị trí (`/`), docstring, type hint cơ bản.
* **2.2. Bẫy tham số mặc định khả biến**
  * `def f(items=[])` dùng chung một list giữa các lần gọi; mẫu sửa bằng `None` làm giá trị canh gác (sentinel).
* **2.3. Phạm vi, closure và decorator**
  * Quy tắc LEGB, `global`/`nonlocal`; hàm là đối tượng; `lambda`; closure; decorator và `functools.wraps`. Ví dụ thực dụng: `@timed` đo thời gian, `@retry` thử lại khi lỗi tạm (retry đầy đủ xem Mục 6.3).
* **2.4. Module và import**
  * `import`, `from ... import`, `sys.path`, `if __name__ == "__main__":`, `__pycache__`, import vòng tròn (circular import) và cách tránh, không dùng `from x import *`. Bẫy đặt tên file trùng thư viện chuẩn hoặc thư viện đã cài (`json.py`, `requests.py`) làm import nhầm.
* **2.5. Package và cấu trúc dự án**
  * `__init__.py`, import tuyệt đối so với tương đối, bố cục `src/`, chạy bằng `python -m tên_package`, tách phần logic khỏi phần giao diện dòng lệnh (nền cho Mục 5.6 và 10.1).
* **2.6. Type hint và kiểm tra tĩnh**
  * `list[str]`, `dict[str, int]`, `X | None` (3.10 trở lên), `Optional`, `TypedDict`; type hint không được kiểm tra lúc chạy, cần `mypy`/`pyright` (xem Mục 10.4).
* **2.7. Phong cách code**
  * PEP 8, đặt tên, docstring ngắn gọn, vì sao nên để công cụ định dạng tự động (`ruff`, xem Mục 10.4).
* **Lab thực hành:** Tái cấu trúc script đếm log của Module 1 thành package `logstats/` gồm các hàm tách bạch, `__main__.py`, chạy bằng `python -m logstats access.log`. Viết decorator `@timed` và `@retry` rồi áp dụng vào một hàm giả lập lỗi ngẫu nhiên.
* **Case study sự cố:**
  1. *Case 1:* Hàm gom danh sách hostname dùng `hosts=[]` làm mặc định, mỗi lần gọi trong cùng một tiến trình lại cộng dồn kết quả của lần trước, nên báo cáo có cả host cũ.
  2. *Case 2:* Tạo file `requests.py` hoặc `json.py` trong thư mục dự án, script lỗi `AttributeError: partially initialized module` hoặc import nhầm file của chính mình; chẩn đoán bằng `python -c "import x; print(x.__file__)"`.

---

### MODULE 3: XỬ LÝ LỖI, CONTEXT MANAGER, LOGGING & MÃ THOÁT
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: viết script không im lặng nuốt lỗi, có log đọc được, trả mã thoát đúng và dừng êm khi nhận tín hiệu.*

* **3.1. Exception**
  * `try`/`except`/`else`/`finally`; phân cấp lỗi (`BaseException` → `Exception`); bắt lỗi cụ thể thay vì `except Exception`; vì sao tuyệt đối không dùng `except:` trần (nuốt cả `KeyboardInterrupt` và `SystemExit`) và `except: pass`.
  * `raise`, `raise ... from ...` (giữ nguyên nhân gốc), exception tùy chỉnh, EAFP so với LBYL. `ExceptionGroup`/`except*` (3.11) ở mức nhận biết `[Mở rộng]`.
* **3.2. Đọc traceback**
  * Đọc từ dưới lên; chuỗi nguyên nhân (`__cause__`); `traceback.print_exc()`; `logging.exception()` để ghi cả traceback vào log.
* **3.3. Context manager**
  * `with` đảm bảo dọn dẹp (file, socket, khóa, kết nối); `contextlib.contextmanager`, `closing`, `suppress`; nhiều `with` trong một dòng.
* **3.4. Module `logging`**
  * Mức độ (DEBUG đến CRITICAL), logger/handler/formatter, `logging.getLogger(__name__)` trong code thư viện, `basicConfig` (không có tác dụng nếu root logger đã có handler, trừ khi `force=True`), `dictConfig`, định dạng chuẩn, ghi ra stderr/stdout trong container.
  * Xoay vòng log: `RotatingFileHandler` / `TimedRotatingFileHandler` so với `logrotate` bên ngoài (giáo trình Hệ điều hành, Mục 9.5). Log có cấu trúc (JSON) cần thư viện thêm hoặc formatter tự viết. Không log secret. Dùng định dạng lười `logger.info("x=%s", x)`.
* **3.5. Mã thoát và tín hiệu**
  * `sys.exit(code)`, `SystemExit`; quy ước: 0 thành công, khác 0 là lỗi (ví dụ 1 lỗi chung, 2 sai cú pháp dòng lệnh theo thói quen của `argparse`). Cron, systemd, CI và Kubernetes đều dựa vào mã thoát để biết job thành công hay thất bại.
  * Bắt `SIGTERM`/`SIGINT` bằng `signal.signal`, tắt êm (hoàn tất việc đang làm, dọn tài nguyên rồi thoát), `atexit`. Hành vi tín hiệu của Docker/Kubernetes xem giáo trình Hệ điều hành, Mục 5.3 và 5.4.
* **Lab thực hành:** Viết `backup_check.py`: đọc danh sách đường dẫn, kiểm tra từng mục, xử lý từng loại lỗi cụ thể (`FileNotFoundError`, `PermissionError`), ghi log ra stderr và file xoay vòng, trả mã thoát 0 (tất cả đạt) / 1 (có mục lỗi) / 2 (sai cấu hình), có handler `SIGTERM` để dừng êm giữa chừng.
* **Case study sự cố:**
  1. *Case 1:* Job sao lưu dùng `except Exception: pass` nên khi gặp `PermissionError` vẫn báo thành công suốt nhiều ngày mà không có bản sao lưu nào; sửa bằng bắt lỗi cụ thể, ghi log lỗi và trả mã thoát khác 0.
  2. *Case 2:* Log không xuất hiện (vì `basicConfig` bị bỏ qua do thư viện đã cấu hình root logger) hoặc bị lặp hai dòng (vì thêm handler mỗi lần gọi hàm khởi tạo); sửa bằng cấu hình logging một lần ở điểm vào chương trình.

---

### MODULE 4: FILE, ĐƯỜNG DẪN & ĐỊNH DẠNG DỮ LIỆU
*Ước lượng: ~4.500 từ*
*🎯 Học xong làm được: đọc/ghi file và các định dạng JSON/YAML/TOML/CSV đúng cách (mã hóa, an toàn khi ghi), và xử lý văn bản bằng regex, thời gian bằng `datetime`.*

* **4.1. `pathlib`, `shutil` và `tempfile`**
  * `Path`, toán tử `/`, `exists`, `mkdir(parents=True, exist_ok=True)`, `glob`/`rglob`, `read_text`/`write_text`, `resolve`, `expanduser`, `stat`; `os.walk`/`os.scandir`.
  * `shutil` (`copy`, `copytree`, `move`, `rmtree`, `which`, `disk_usage`); `tempfile` (`TemporaryDirectory`, `NamedTemporaryFile`, `mkstemp`).
* **4.2. Mở file, văn bản và nhị phân, mã hóa**
  * Chế độ mở file, `with open(...)`, đọc file lớn theo dòng hoặc theo khối thay vì nạp cả file. **Luôn chỉ định `encoding="utf-8"`**: mặc định phụ thuộc locale ở các phiên bản trước 3.15; Python 3.15 chuyển sang UTF-8 mặc định theo PEP 686 [CẦN XÁC MINH theo bản phát hành].
* **4.3. Ghi file an toàn**
  * Ghi vào file tạm trong cùng thư mục rồi `os.replace()` để thay thế nguyên tử trên cùng một filesystem; `flush` + `os.fsync` khi cần độ bền dữ liệu; đặt quyền (`os.chmod`, `umask`; xem giáo trình Hệ điều hành, Mục 3.3); khóa file (`fcntl.flock` trên Unix, xem giáo trình Hệ điều hành, Mục 3.5).
* **4.4. JSON**
  * `json.load`/`loads`/`dump`/`dumps` (`indent`, `sort_keys`, `ensure_ascii`), JSON Lines cho log, kiểu không tuần tự hóa được (`datetime`, `set`) và cách xử lý, so sánh với `jq` (giáo trình Hệ điều hành, Mục 2.4).
* **4.5. YAML, TOML, INI, CSV, SQLite**
  * YAML cần `PyYAML` (cài thêm): **luôn `yaml.safe_load`**, không dùng `yaml.load` với dữ liệu không tin cậy. Bẫy YAML: giá trị như `no`, `on`, `1.10` bị hiểu thành boolean/số (cần đặt trong nháy).
  * `tomllib` (3.11 trở lên, chỉ đọc; ghi TOML cần thư viện thêm), `configparser`, `csv` (`DictReader`, mở file với `newline=""`), `sqlite3` trong thư viện chuẩn cho dữ liệu nhỏ cục bộ.
* **4.6. Biến môi trường và quản lý cấu hình**
  * `os.environ`, `os.getenv`, ép kiểu, thứ tự ưu tiên (mặc định < file < biến môi trường < tham số dòng lệnh), không hardcode, `python-dotenv` chỉ phù hợp cho phát triển cục bộ (secret thật xem Mục 12.1). Sinh file cấu hình bằng Jinja2 (cài thêm) `[Mở rộng]`.
* **4.7. Biểu thức chính quy (`re`)**
  * `search`/`match`/`fullmatch`/`findall`/`finditer`/`sub`, nhóm đặt tên, `re.compile`; dùng để bóc tách log; không dùng regex để parse JSON/HTML; biết rủi ro backtracking nghiêm trọng (ReDoS). So sánh với `grep -E` (giáo trình Hệ điều hành, Mục 2.4).
* **4.8. Thời gian**
  * `datetime` ngây thơ (naive) so với có múi giờ (aware), luôn lưu và trao đổi bằng UTC/ISO 8601, `zoneinfo` (3.9 trở lên), `strptime`/`strftime`, `time.monotonic()` để đo khoảng thời gian.
* **Lab thực hành:** Viết `config-merge`: đọc `base.yaml` và `prod.yaml`, gộp sâu (deep merge), kiểm tra schema đơn giản (khóa bắt buộc, kiểu giá trị), ghi `config.json` bằng ghi nguyên tử; cố ý đặt `version: 1.10` không có nháy để thấy lỗi bị hiểu thành số. Thêm một bước đọc log JSON Lines và tính p95 độ trễ bằng `statistics.quantiles`.
* **Case study sự cố:**
  1. *Case 1:* `UnicodeDecodeError` khi đọc file có tiếng Việt trên máy/CI khác locale (hoặc `LANG=C`); sửa bằng chỉ định `encoding="utf-8"` và kiểm soát dữ liệu đầu vào.
  2. *Case 2:* Script ghi thẳng vào file cấu hình mà dịch vụ đang đọc; khi script bị kill hoặc hết đĩa giữa chừng, file bị cụt, dịch vụ khởi động lỗi; sửa bằng ghi nguyên tử (file tạm + `os.replace`).

---

### MODULE 5: SCRIPT DÒNG LỆNH & TƯƠNG TÁC VỚI HỆ ĐIỀU HÀNH
*Ước lượng: ~4.500 từ*
*🎯 Học xong làm được: xây CLI chuẩn có `--help`, mã thoát, `--dry-run`; gọi lệnh hệ thống an toàn bằng `subprocess` mà không bị treo hay bị injection.*

* **5.1. `sys.argv` và `argparse`**
  * Tham số vị trí và tùy chọn, `type`, `choices`, `default`, `required`, `store_true`, `nargs`, subcommand, `--help` tự sinh; sai cú pháp thì `argparse` thoát với mã 2. `click`/`typer` là lựa chọn bên thứ ba `[Mở rộng]`. Đọc stdin và quy ước `-` cho phép dùng trong pipe.
* **5.2. `subprocess`: gọi lệnh bên ngoài**
  * `subprocess.run([...], check=True, capture_output=True, text=True, timeout=..., cwd=..., env=...)`; `CompletedProcess`, `CalledProcessError`, `TimeoutExpired`; mã thoát âm nghĩa là bị tín hiệu (xem giáo trình Hệ điều hành, Mục 5.3).
  * **Truyền lệnh dạng danh sách, tránh `shell=True`** vì nguy cơ command injection; khi bắt buộc dùng shell thì dùng `shlex.quote`. `Popen` cho luồng xuất dài và nguy cơ treo (deadlock) khi pipe đầy mà không có ai đọc; dùng `communicate()`.
* **5.3. `os`, `sys`, `platform`, `shutil`**
  * `os.getenv`, `os.getpid`, `os.cpu_count`, `shutil.which`, `socket.gethostname`, `getpass.getuser`, `platform`, `os.kill`, `signal`.
* **5.4. Gọi công cụ hạ tầng bằng lệnh hay bằng SDK**
  * Gọi `kubectl ... -o json`, `docker ... --format '{{json .}}'` rồi parse JSON so với dùng SDK (Module 7); khi nào subprocess hợp lý (đơn giản, nhanh) và khi nào nên dùng SDK (kiểm soát lỗi, phân trang, kiểu dữ liệu). Gọi `ssh` xem Mục 7.1.
* **5.5. Khác biệt giữa các nền tảng**
  * Dấu phân cách đường dẫn, xuống dòng, lệnh GNU so với BSD (`sed -i`) không còn là vấn đề khi xử lý bằng Python (giáo trình Hệ điều hành, Mục 14.3).
* **5.6. Thiết kế CLI chuyên nghiệp**
  * Hàm `main(argv=None) -> int` để dễ kiểm thử, `if __name__ == "__main__": sys.exit(main())`, các cờ `--verbose/--quiet`, `--dry-run`, `--json`; xử lý `BrokenPipeError` khi dùng `| head`; chỉ in màu khi là TTY (`sys.stdout.isatty()`), tôn trọng `NO_COLOR`.
* **Lab thực hành:** Viết CLI `diskwatch`: lệnh con `scan` (dùng `shutil.disk_usage` và `os.walk` tìm thư mục lớn nhất), `report --json`, `--threshold`, `--dry-run`; gọi `df -i` và `lsof +L1` bằng `subprocess` để phát hiện file đã xóa nhưng còn mở (giáo trình Hệ điều hành, Mục 4.4); thử chạy qua `| head` và `> file`.
* **Case study sự cố:**
  1. *Case 1:* Script ghép tên host lấy từ đầu vào vào lệnh với `shell=True`; giá trị chứa `; rm ...` bị thực thi (command injection); sửa bằng danh sách tham số và kiểm tra đầu vào.
  2. *Case 2:* Job cron treo vô hạn vì `subprocess` chờ một lệnh không bao giờ kết thúc (không đặt `timeout`) hoặc vì pipe đầu ra đầy; sửa bằng `run(timeout=...)`, `communicate()` và xử lý `TimeoutExpired`.

---

### MODULE 6: GỌI API HTTP & TÍCH HỢP DỊCH VỤ
*Ước lượng: ~3.500 từ*
*🎯 Học xong làm được: viết client API đáng tin cậy với timeout, retry có backoff, phân trang và xử lý TLS/xác thực đúng cách.*

* **6.1. HTTP cho người viết script**
  * Method, status code, header, body JSON, REST, xác thực (Bearer token, Basic, API key), khái niệm idempotent (GET/PUT/DELETE thường idempotent, POST thì không). Nền tảng giao thức: giáo trình Mạng máy tính, Mục 6.1.
* **6.2. Thư viện HTTP**
  * `urllib.request` (thư viện chuẩn, dài dòng), `requests` (phổ biến, đồng bộ), `httpx` (đồng bộ và bất đồng bộ). Dùng `Session` để tái sử dụng kết nối (keep-alive), liên hệ giáo trình Mạng máy tính, Mục 7.4 và Mục 4.2 (TIME_WAIT khi tạo quá nhiều kết nối mới).
* **6.3. Timeout, retry và backoff**
  * **Luôn đặt timeout** (thư viện `requests` không có timeout mặc định); tách timeout kết nối và đọc; `raise_for_status()`.
  * Retry chỉ với lỗi tạm thời (lỗi kết nối, 5xx, 429), backoff lũy thừa kèm jitter, tôn trọng header `Retry-After`; chỉ retry thao tác idempotent hoặc dùng idempotency key. `urllib3.util.Retry` với `HTTPAdapter`; `tenacity` `[Mở rộng]`.
* **6.4. Phân trang, giới hạn tốc độ và tải dữ liệu lớn**
  * Phân trang theo trang/offset, theo cursor, theo `Link` header; dùng generator để duyệt qua các trang; header giới hạn tốc độ (như `X-RateLimit-*`); tải file lớn theo luồng (`stream=True`, `iter_content`) và kiểm tra checksum.
* **6.5. TLS, proxy và bảo vệ token**
  * Xác minh chứng chỉ bật mặc định; **không dùng `verify=False` để "cho chạy được"**; với CA nội bộ chỉ định bộ CA (`verify="/path/ca.pem"` hoặc `REQUESTS_CA_BUNDLE`); lỗi chuỗi chứng chỉ xem giáo trình Mạng máy tính, Mục 6.3; proxy qua `HTTPS_PROXY`. Token không hardcode, không ghi vào log (xem Mục 12.1).
* **6.6. Webhook và tích hợp thường gặp**
  * Gửi thông báo Slack/Teams qua webhook, gọi API GitHub/GitLab, Alertmanager, ArgoCD. Nhận webhook và xác thực chữ ký HMAC bằng `hmac.compare_digest` (dựng server nhỏ bằng FastAPI hoặc `http.server` `[Mở rộng]`).
* **Lab thực hành:** Chạy `httpbin` bằng Docker để mô phỏng lỗi 429/500 và phản hồi chậm. Viết `api_inventory.py`: dùng `Session`, timeout, retry có backoff, duyệt phân trang bằng generator, ghi kết quả ra JSON Lines; so sánh khi tắt retry/timeout.
* **Case study sự cố:**
  1. *Case 1:* Script gọi API đối tác không đặt timeout; khi đối tác treo, mỗi lần cron chạy lại tạo thêm một tiến trình bị kẹt, dẫn đến cạn tài nguyên; sửa bằng timeout, giới hạn thời gian chạy tổng và khóa chống chạy chồng.
  2. *Case 2:* Báo cáo kiểm kê thiếu dữ liệu vì chỉ lấy trang đầu tiên của API phân trang (ví dụ mặc định 30 mục mỗi trang); sửa bằng duyệt hết các trang và kiểm tra tổng số.

---

### MODULE 7: LÀM VIỆC VỚI HẠ TẦNG: SSH, DOCKER, KUBERNETES & CLOUD SDK
*Ước lượng: ~5.000 từ*
*🎯 Học xong làm được: viết script liệt kê, kiểm kê và dọn dẹp tài nguyên trên SSH/Docker/Kubernetes/AWS theo cách an toàn (dry-run trước, phân trang đầy đủ, không lộ khóa).*

* **7.1. SSH bằng Python**
  * `paramiko` (client, `known_hosts`, chạy lệnh, chuyển file); **không dùng `AutoAddPolicy` ở production** vì vô hiệu hóa việc xác minh host key; Fabric ở mức khái niệm; so sánh với gọi `ssh` bằng `subprocess` và với Ansible (giáo trình Hệ điều hành, Mục 8.3 và 13.4). Chạy song song nhiều host xem Mục 9.2.
* **7.2. Docker SDK**
  * Gói `docker`: `docker.from_env()`, liệt kê/khởi chạy/dừng container, đọc log, dọn tài nguyên rác; khi nào dùng SDK thay vì CLI (liên hệ giáo trình Hệ điều hành, Mục 11.5).
* **7.3. Kubernetes client**
  * Gói `kubernetes`: `config.load_kube_config()` (chạy từ máy cá nhân) so với `config.load_incluster_config()` (chạy trong Pod); `CoreV1Api().list_namespaced_pod`, phân trang bằng `limit` và `_continue`, `watch`; ServiceAccount và RBAC với quyền tối thiểu; so sánh với `kubectl -o json`. Viết Operator bằng `kopf` `[Mở rộng]`.
* **7.4. AWS với boto3**
  * `client` so với `resource`: giao diện `resource` không còn được bổ sung tính năng mới (bản vẫn dùng được), ưu tiên `client` cho code mới. Session, profile, region.
  * **Chuỗi tìm thông tin xác thực (credential chain):** biến môi trường, file cấu hình/SSO, role gắn vào EC2/ECS/EKS; kiểm tra danh tính hiện tại bằng `sts.get_caller_identity()` trước khi chạy lệnh có tác động.
  * Phân trang bằng `get_paginator` (ví dụ `list_objects_v2` trả tối đa 1.000 đối tượng mỗi lần gọi), cấu hình retry (`botocore.config.Config(retries={"mode": "standard"})`), bắt `botocore.exceptions.ClientError` và đọc `response["Error"]["Code"]`, waiters, `DryRun=True` (EC2). IAM quyền tối thiểu. Đối chiếu SDK GCP/Azure ở mức khái niệm.
* **7.5. Kiểm thử mà không chạm cloud thật**
  * `moto` (mô phỏng AWS trong tiến trình), LocalStack, `botocore.stub.Stubber`, tài khoản sandbox riêng; lưu ý chi phí và luôn xóa tài nguyên sau lab (kiểm thử xem Mục 10.3).
* **7.6. Mẫu "dọn dẹp tài nguyên" an toàn**
  * Liệt kê → lọc (theo tag, tuổi, môi trường) → in kế hoạch → chỉ khi có `--apply` mới thực hiện; bảo vệ tài nguyên có tag `keep`; ghi log mọi hành động; giới hạn số lượng xóa tối đa mỗi lần chạy.
* **Lab thực hành:** (a) Viết `ec2_cleaner.py` hoặc `s3_audit.py` bằng boto3 chạy trên moto/LocalStack/sandbox: liệt kê, lọc theo tag, mặc định dry-run, `--apply`, phân trang đầy đủ. (b) Dựng cụm `kind`, viết `k8s_pod_report.py` liệt kê Pod không Ready hoặc restart nhiều, xuất JSON.
* **Case study sự cố:**
  1. *Case 1:* Script đồng bộ/kiểm kê bucket chỉ xử lý 1.000 đối tượng đầu tiên vì gọi `list_objects_v2` một lần, trong khi bucket có hàng trăm nghìn đối tượng; sửa bằng paginator.
  2. *Case 2:* Khóa truy cập AWS bị hardcode trong script và commit lên Git; sửa theo thứ tự: **thu hồi/xoay vòng khóa ngay**, chuyển sang credential chain/role, quét lịch sử Git bằng công cụ phát hiện secret, rồi mới dọn lịch sử.

---

### MODULE 8: HƯỚNG ĐỐI TƯỢNG, GENERATOR & CẤU TRÚC DỮ LIỆU NÂNG CAO
*Ước lượng: ~3.500 từ*
*🎯 Học xong làm được: mô hình hóa dữ liệu bằng dataclass/enum, xử lý dữ liệu lớn bằng generator và tổ chức nhiều loại "check" bằng mẫu plugin đơn giản.*

* **8.1. Lớp và đối tượng**
  * `class`, `__init__`, thuộc tính, phương thức, `@property`, `@classmethod`/`@staticmethod`, `__repr__`; ưu tiên composition hơn kế thừa; khi nào **không** cần class (hàm cùng dict hoặc dataclass thường là đủ cho script).
* **8.2. `dataclasses`, `enum` và kiểu dữ liệu có cấu trúc**
  * `@dataclass`, `field(default_factory=...)`, `frozen=True`, `slots=True`, `__post_init__`; so sánh với `NamedTuple`/`TypedDict`; `Enum`/`StrEnum` (3.11).
* **8.3. Kiểm tra dữ liệu đầu vào**
  * Giới thiệu `pydantic` và `jsonschema` (cài thêm) để kiểm tra cấu hình theo schema, thay cho tự viết nhiều `if`.
* **8.4. Iterator, generator và thư viện chuẩn hữu ích**
  * `yield`, generator expression, xử lý lười (lazy) cho file/log lớn và API phân trang; generator chỉ dùng được một lần; `itertools` (`chain`, `islice`, `groupby` cần sắp xếp trước, `batched` từ 3.12); `collections` (`Counter`, `defaultdict`, `deque`).
* **8.5. Duck typing, `Protocol` và mẫu plugin**
  * `Protocol`/`ABC`, đăng ký "check" theo tên (registry) để thêm kiểm tra mới mà không sửa lõi (dùng cho dự án ở Mục 13.3).
* **8.6. Bộ nhớ và hiệu năng cơ bản**
  * `"".join` thay vì nối chuỗi trong vòng lặp lớn, đọc file theo dòng, `__slots__`, `tracemalloc` để tìm rò rỉ (liên hệ giáo trình Hệ điều hành, Mục 6.7).
* **Lab thực hành:** Mô hình hóa `Host` và `CheckResult` bằng dataclass và enum; viết generator đọc file log lớn theo dòng và đếm lỗi theo phút mà không nạp cả file vào bộ nhớ; viết hệ thống plugin với hai "check" mẫu (TCP connect, HTTP status) đăng ký qua registry.
* **Case study sự cố:**
  1. *Case 1:* Một generator bị duyệt hai lần (lần đầu để đếm, lần hai để ghi báo cáo) nên lần hai không có dữ liệu và báo cáo ghi "0 lỗi"; sửa bằng `list(...)` khi cần dùng lại, hoặc tạo lại generator.
  2. *Case 2:* Thuộc tính list khai báo ở cấp class bị chia sẻ giữa mọi đối tượng, nên kết quả kiểm tra của host này lọt sang host khác (với `dataclass`, Python chặn kiểu default này và yêu cầu `default_factory`).

---

### MODULE 9: ĐỒNG THỜI & HIỆU NĂNG: THREAD, PROCESS, ASYNCIO
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: rút ngắn script chạy hàng trăm host/API từ hàng giờ xuống vài phút một cách có kiểm soát, và chọn đúng giữa thread, process và asyncio.*

* **9.1. Khái niệm: tuần tự, đồng thời, song song**
  * Tác vụ I/O-bound (chờ mạng/đĩa) so với CPU-bound (tính toán). **GIL** (Global Interpreter Lock): trong bản CPython build mặc định, tại một thời điểm chỉ một thread thực thi bytecode Python; thread nhả GIL khi chờ I/O, nên thread phù hợp với I/O-bound; CPU-bound nên dùng nhiều process.
* **9.2. `concurrent.futures`**
  * `ThreadPoolExecutor`, `ProcessPoolExecutor`, `submit`/`map`/`as_completed`, bắt lỗi từng future, timeout cho từng tác vụ. **Chọn số worker có chủ đích**: bị giới hạn bởi rate limit của API, số kết nối, `ulimit -n` (giáo trình Hệ điều hành, Mục 5.6).
* **9.3. `threading`**
  * `Lock`, race condition, `queue.Queue`, daemon thread. Không chia sẻ trạng thái khả biến giữa thread nếu không cần. Với boto3: client thường an toàn giữa các thread, còn session và resource thì nên tạo riêng cho mỗi thread (theo tài liệu boto3).
* **9.4. `multiprocessing`**
  * Phương thức khởi tạo `fork`/`spawn`/`forkserver`; trên Linux mặc định là `fork` đến 3.13 và chuyển sang `forkserver` từ 3.14 [CẦN XÁC MINH]; tham số truyền sang tiến trình phải pickle được; luôn dùng `if __name__ == "__main__":`.
* **9.5. `asyncio`**
  * `async`/`await`, event loop, `asyncio.run`, `gather`, `TaskGroup` và `asyncio.timeout` (3.11 trở lên), `Semaphore` để giới hạn đồng thời, `httpx.AsyncClient`/`aiohttp`. **Không gọi hàm chặn (`time.sleep`, `requests.get`) trong coroutine**; dùng `asyncio.to_thread`. Hủy task.
* **9.6. [Mở rộng] Free-threaded và subinterpreter**
  * Python 3.14: bản build free-threaded (không GIL) được hỗ trợ chính thức nhưng là bản build tùy chọn (bản mặc định vẫn có GIL, và nhiều thư viện C chưa hỗ trợ đầy đủ); `InterpreterPoolExecutor` (3.14).
* **9.7. Đo lường và giới hạn an toàn**
  * `time.perf_counter()`, đo trước/sau tối ưu; backpressure; không để script "tự DDoS" API hay hạ tầng của chính mình.
* **Lab thực hành:** Kiểm tra 200 endpoint giả lập (server local có độ trễ ngẫu nhiên) bằng ba cách: tuần tự, `ThreadPoolExecutor`, `asyncio` kèm `Semaphore`; đo thời gian và so sánh. Thử `ProcessPoolExecutor` với tác vụ CPU-bound (băm nhiều file) và so với thread. Thêm giới hạn đồng thời để không vượt rate limit.
* **Case study sự cố:**
  1. *Case 1:* Kiểm tra 500 host tuần tự mất hàng giờ; chuyển sang thread pool giảm xuống vài phút, nhưng khi mở 500 thread cùng lúc thì cạn file descriptor hoặc bị API chặn; giải pháp là giới hạn worker, timeout từng host và gom kết quả có thứ tự.
  2. *Case 2:* Ứng dụng `asyncio` bị "đóng băng", mọi tác vụ chờ nhau, vì có một lời gọi `requests.get`/`time.sleep` đồng bộ trong coroutine làm nghẽn event loop; sửa bằng `httpx.AsyncClient`, `asyncio.sleep` hoặc `asyncio.to_thread`.

---

### MODULE 10: KIỂM THỬ, CHẤT LƯỢNG CODE & GỠ LỖI
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: viết test cho script hạ tầng mà không chạm hệ thống thật, thiết lập lint/format/kiểm tra kiểu tự động và gỡ lỗi có phương pháp.*

* **10.1. Vì sao phải test script hạ tầng**
  * Script chạy trên production, lỗi có thể xóa dữ liệu hoặc tốn tiền. Thiết kế để dễ test: tách logic thuần khỏi I/O, truyền phụ thuộc (client, đồng hồ) vào hàm thay vì tạo bên trong, hàm `main(argv)` (xem Mục 5.6).
* **10.2. `pytest`**
  * `assert`, `-k`, `-x`, `-q`, `-vv`; fixture (`tmp_path`, `monkeypatch`, `capsys`, `caplog`), `parametrize`, `pytest.raises`, `conftest.py`, thư mục `tests/`.
* **10.3. Mock và giả lập**
  * `unittest.mock` (`patch`, `MagicMock`, `autospec`): patch ở nơi hàm **được dùng**, không phải nơi định nghĩa. `responses`/`respx` cho HTTP, `moto` cho AWS, giả lập `subprocess.run`, dùng `tmp_path` cho file. Test không được chạm mạng hoặc cloud thật.
* **10.4. Chất lượng code tĩnh**
  * `ruff` (lint và format), `mypy`/`pyright` (kiểu), `bandit` (lỗi bảo mật thường gặp), `pre-commit`; cấu hình tập trung trong `pyproject.toml`; chạy cùng bộ kiểm tra này trong CI (Mục 11.5).
* **10.5. Độ phủ (coverage)**
  * `pytest-cov`; coverage cao không bằng đúng, nhưng vùng không được test là vùng rủi ro; đặt ngưỡng hợp lý, không chạy theo con số.
* **10.6. Gỡ lỗi**
  * Đọc traceback (Mục 3.2), `logging` thay cho `print` rải rác, `breakpoint()`/`pdb` (`n`, `s`, `c`, `p`, `l`, `bt`, `q`), `python -X dev`, `faulthandler`. Python 3.14 bổ sung giao diện gỡ lỗi từ bên ngoài an toàn (PEP 768) cho phép gắn pdb vào tiến trình đang chạy [CẦN XÁC MINH cú pháp]. `py-spy` (cài thêm; trong container cần quyền ptrace), `strace -p` (giáo trình Hệ điều hành, Mục 5.8), `cProfile`, `timeit`, `tracemalloc`.
* **Lab thực hành:** Viết test cho `logstats` (Module 2), `api_inventory` (mock HTTP trả 200/429/500), `ec2_cleaner` (moto); cấu hình `ruff`, `mypy` và `pre-commit`; chạy `pytest --cov`; cố ý đưa vào một lỗi logic và dùng `pdb` để tìm ra.
* **Case study sự cố:**
  1. *Case 1:* Bộ test gọi API/cloud thật nên chậm, chập chờn, tốn tiền, và một lần test dọn dẹp xóa nhầm tài nguyên thật; sửa bằng mock/moto, tài khoản sandbox và chặn mạng trong test.
  2. *Case 2:* Test lúc qua lúc hỏng (flaky) do phụ thuộc thời gian thực, thứ tự chạy, dữ liệu ngẫu nhiên hoặc múi giờ; sửa bằng truyền đồng hồ giả, cố định seed, dùng `tmp_path` và độc lập giữa các test.

---

### MODULE 11: ĐÓNG GÓI, PHỤ THUỘC & CHẠY PYTHON TRONG CONTAINER/CI
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: đóng gói script thành công cụ cài được, quản lý phụ thuộc tái lập được, build image Python gọn và an toàn, và chạy theo lịch hoặc như một dịch vụ.*

* **11.1. `pyproject.toml` và đóng gói**
  * `[project]` (tên, phiên bản, `requires-python`, `dependencies`, `optional-dependencies`), `[project.scripts]` (lệnh `console_scripts`), `[build-system]`; `python -m build` tạo sdist và wheel; `pip install -e .` (editable). Đào sâu về `pip`/packaging xem giáo trình Build tools.
* **11.2. Quản lý phụ thuộc và khả năng tái lập**
  * `requirements.txt` ghim phiên bản; hạn chế của `pip freeze`; file ràng buộc; `pip-compile` (pip-tools); `pip install --require-hashes`; công cụ khóa phiên bản (`uv`, Poetry, PDM) `[Mở rộng]`, hãy chọn một công cụ thống nhất cho cả team; `pip check`, `pip-audit`, cập nhật có kiểm soát bằng Dependabot/Renovate.
* **11.3. Wheel, sdist và thư viện biên dịch**
  * Wheel nhị phân (thẻ như `manylinux`, `musllinux`, `cp312`); khi không có wheel phù hợp, `pip` phải build từ source và cần compiler cùng header (`gcc`, `python3-dev`); bẫy Alpine/musl: wheel `manylinux` không dùng được trên musl.
* **11.4. Dockerfile cho Python**
  * Base image `python:<phiên bản>-slim` so với Alpine; multi-stage (tạo venv ở stage build rồi sao chép sang stage chạy); `pip install --no-cache-dir`; `PYTHONUNBUFFERED=1`, `PYTHONDONTWRITEBYTECODE=1`; chạy bằng user không phải root; `.dockerignore`; tối ưu cache layer (copy `requirements` trước mã nguồn); `ENTRYPOINT` dạng exec để nhận tín hiệu đúng (giáo trình Hệ điều hành, Mục 5.4); root filesystem chỉ đọc cần thư mục ghi riêng (giáo trình Hệ điều hành, Mục 11.6).
* **11.5. CI/CD cho script Python**
  * Pipeline mẫu: lint → kiểm tra kiểu → test → build → đẩy image/package; cache pip; chạy trên nhiều phiên bản Python (`tox`/`nox` `[Mở rộng]`); kho package nội bộ (private index); cài công cụ nội bộ bằng `pipx`.
  * Chạy trong Kubernetes: Job/CronJob, giới hạn tài nguyên và OOM (giáo trình Hệ điều hành, Mục 11.3 và 6.4).
* **11.6. Chạy theo lịch và chạy như dịch vụ**
  * cron/systemd timer (giáo trình Hệ điều hành, Mục 13.1 và 9.3); unit chạy bằng Python trong venv (`ExecStart=/opt/app/.venv/bin/python -m app`, xem giáo trình Hệ điều hành, Mục 9.2), user riêng, `Restart=`, log vào journald (giáo trình Hệ điều hành, Mục 9.5). Không dựa vào `python` hệ thống.
* **Lab thực hành:** Đóng gói `logstats` thành package có entry point, build wheel và cài vào venv sạch từ wheel. Viết Dockerfile multi-stage chạy non-root, so sánh kích thước `slim` và Alpine, quan sát độ trễ log khi bật/tắt `PYTHONUNBUFFERED`. Viết systemd unit và timer chạy công cụ bằng Python của venv.
* **Case study sự cố:**
  1. *Case 1:* Build image Alpine cho một dự án có thư viện biên dịch rất chậm hoặc lỗi vì không có wheel phù hợp với musl và thiếu compiler; sửa bằng image `slim`, hoặc cài toolchain trong stage build, hoặc dùng wheel `musllinux` nếu thư viện có.
  2. *Case 2:* `docker logs` trống hoặc trễ vì đầu ra bị đệm khi không có TTY; sửa bằng `PYTHONUNBUFFERED=1` (hoặc `python -u`), hoặc ghi log trực tiếp ra stderr qua `logging`.

---

### MODULE 12: BẢO MẬT & VẬN HÀNH SCRIPT PRODUCTION
*Ước lượng: ~3.500 từ*
*🎯 Học xong làm được: rà soát và vá các lỗ hổng phổ biến trong script hạ tầng, và làm cho script chạy lặp lại an toàn, quan sát được.*

* **12.1. Quản lý secret**
  * Không hardcode, không commit; không truyền secret qua tham số dòng lệnh (lộ qua `ps` và `/proc/<pid>/cmdline`); biến môi trường có rủi ro (lộ qua `/proc/<pid>/environ`, crash dump, log); file quyền `600`; secret manager (Vault, AWS Secrets Manager, Kubernetes Secret); `getpass`; che secret trong log; xoay vòng định kỳ; quét secret trong Git (như `gitleaks`) bằng `pre-commit`. Khi lỡ lộ: thu hồi trước, dọn lịch sử sau.
* **12.2. Đầu vào không đáng tin**
  * Kiểm tra và làm sạch đầu vào; injection (lệnh: Mục 5.2; SQL: truy vấn có tham số, không ghép chuỗi); path traversal (`Path.resolve()` rồi kiểm tra `is_relative_to` thư mục gốc); SSRF khi gọi URL do người dùng cung cấp `[Mở rộng]`.
* **12.3. Giải tuần tự hóa và giải nén**
  * `pickle` chỉ dùng với dữ liệu tin cậy (có thể thực thi mã tùy ý), `yaml.safe_load`, tránh `eval`/`exec`. `tarfile.extractall` có nguy cơ path traversal: dùng tham số `filter="data"` (có từ 3.12; từ 3.14 là mặc định [CẦN XÁC MINH theo phiên bản]); giới hạn kích thước giải nén (zip bomb).
* **12.4. Chuỗi cung ứng phụ thuộc**
  * Typosquatting, dependency confusion (`--index-url` so với `--extra-index-url`), ghim phiên bản kèm hash, `pip-audit`, xem xét gói mới trước khi thêm, khái niệm SBOM.
* **12.5. Quyền tối thiểu và môi trường chạy**
  * User riêng, quyền file (giáo trình Hệ điều hành, Module 3), tăng cường bảo mật cho unit systemd (giáo trình Hệ điều hành, Mục 9.2), container non-root và rootfs chỉ đọc (giáo trình Hệ điều hành, Mục 11.6), IAM tối thiểu, token phạm vi hẹp và có hạn.
* **12.6. Độ tin cậy vận hành**
  * Idempotent, khóa chống chạy chồng (`fcntl.flock` hoặc file khóa), timeout ở mọi lời gọi ra ngoài, giới hạn số lần retry, dry-run mặc định cho thao tác phá hủy, kiểm tra tên môi trường trước khi thực hiện, báo động khi thất bại, thử ở staging trước.
* **12.7. Quan sát script**
  * Log có cấu trúc kèm `run_id`; metric với `prometheus_client`: job ngắn dùng Pushgateway hoặc textfile collector của node_exporter (giáo trình Hệ điều hành, Mục 12.6); "heartbeat" để phát hiện job *không chạy*; đo thời gian chạy và số mục xử lý.
* **Lab thực hành:** Rà soát một script mẫu có chủ đích chứa lỗi (hardcode secret, `shell=True`, `yaml.load`, `tarfile.extractall`, SQL ghép chuỗi, `verify=False`) bằng `bandit`, `pip-audit` và đọc code; sửa từng lỗi và viết test chống tái phát. Thêm khóa chống chạy chồng và metric `last_success_timestamp`.
* **Case study sự cố:**
  1. *Case 1:* Mật khẩu truyền qua tham số dòng lệnh xuất hiện trong `ps`, trong log của công cụ giám sát và trong lịch sử shell; sửa bằng đọc secret từ file/biến môi trường/secret manager và thu hồi mật khẩu đã lộ.
  2. *Case 2:* Script dọn dẹp xóa nhầm tài nguyên production do lọc sai (thiếu điều kiện môi trường/tag) và chạy nhầm môi trường; sửa bằng dry-run mặc định, xác nhận tên môi trường, danh sách bảo vệ (allowlist) và giới hạn số lượng xóa tối đa mỗi lần.

---

### MODULE 13: DỰ ÁN TỔNG HỢP & MẪU THIẾT KẾ AUTOMATION
*Ước lượng: ~3.000 từ*
*🎯 Học xong làm được: xây dựng, kiểm thử, đóng gói và đưa vào vận hành một công cụ kiểm tra hạ tầng hoàn chỉnh theo quy trình chuyên nghiệp.*

* **13.1. Quy trình làm một công cụ automation**
  * Yêu cầu → thiết kế → làm bản nhỏ nhất chạy được → test → đóng gói → triển khai → vận hành. Nguyên tắc: bắt đầu bằng thao tác chỉ đọc, ghi sau; làm nhỏ và an toàn trước.
* **13.2. Các mẫu thiết kế thường dùng**
  * Plan/apply (dry-run), vòng lặp đối soát (reconcile: so trạng thái mong muốn với thực tế, nền tảng của Kubernetes controller), retry/backoff, circuit breaker (khái niệm), pipeline đọc-lọc-biến đổi-ghi, plugin registry, phân tầng cấu hình, worker pool có giới hạn tốc độ, checkpoint để chạy tiếp.
* **13.3. Dự án `infra-audit`**
  * Yêu cầu: đọc `inventory.yaml` (danh sách host, cổng, loại kiểm tra); chạy đồng thời các kiểm tra TCP connect, HTTP health, DNS resolve và hạn chứng chỉ TLS (`ssl` + `socket`, cảnh báo khi còn ít hơn N ngày; bối cảnh tại giáo trình Mạng máy tính, Mục 6.4); xuất bảng/JSON/textfile Prometheus; mã thoát: 0 tất cả đạt, 1 có kiểm tra thất bại, 2 lỗi cấu hình hoặc đối số.
* **13.4. Tiêu chí hoàn thành (Definition of Done)**
  * Có README và ví dụ cấu hình; test pass; `ruff` và `mypy` sạch; đóng gói được; có Dockerfile; chạy được theo lịch; có metric/heartbeat; có runbook ngắn khi lỗi.
* **13.5. Đưa vào vận hành**
  * systemd timer (giáo trình Hệ điều hành, Mục 9.3) hoặc Kubernetes CronJob (`concurrencyPolicy: Forbid`, `activeDeadlineSeconds`), cảnh báo khi thất bại, xử lý secret, review code.
* **Lab thực hành (dự án chính):** Hoàn thiện `infra-audit` theo Definition of Done; chạy bằng systemd timer trên VM và bằng CronJob trên `kind`; cố ý làm hỏng một host (đóng cổng, cho cert hết hạn, sai DNS) để kiểm chứng mã thoát, metric và cảnh báo.
* **Case study sự cố:**
  1. *Case 1:* Kubernetes CronJob tạo nhiều Pod chạy chồng nhau khi một lần chạy kéo dài (chính sách mặc định cho phép chạy đồng thời), làm quá tải API đích; sửa bằng `concurrencyPolicy: Forbid`, `activeDeadlineSeconds` và timeout trong chính script.
  2. *Case 2:* Script "chạy được" nhưng thất bại âm thầm suốt nhiều tuần vì không ai biết job đã ngừng chạy (hoặc luôn thoát mã 0 dù lỗi); sửa bằng mã thoát đúng, metric `last_success_timestamp` và cảnh báo khi không có lần chạy thành công gần đây.

---

### MODULE 14: PHỤ LỤC MỞ RỘNG (TÍNH NĂNG MỚI, HIỆU NĂNG & HỆ SINH THÁI)
*Ước lượng: ~2.500 từ*

* **14.1. [Mở rộng] Tính năng đáng chú ý theo phiên bản Python (tham chiếu, đối chiếu "What's New" chính thức)**
  * 3.11: `tomllib`, `ExceptionGroup`/`except*`, `TaskGroup`, vị trí lỗi chi tiết trong traceback. 3.12: f-string linh hoạt hơn (PEP 701), `itertools.batched`, bộ lọc giải nén `tarfile`. 3.13: REPL mới, build free-threaded và JIT ở mức thử nghiệm.
  * 3.14: template string `t"..."` (PEP 750), free-threaded được hỗ trợ chính thức (PEP 779), đánh giá annotation hoãn (PEP 649), module `compression.zstd` (PEP 784), cho phép `except A, B:` không cần ngoặc (PEP 758), giao diện gỡ lỗi ngoài an toàn (PEP 768), `InterpreterPoolExecutor`. 3.15 phát hành 09/10/2026: xem "What's New in Python 3.15".
* **14.2. [Mở rộng] Kỹ thuật ngôn ngữ nâng cao**
  * `functools` (`lru_cache`, `cache`, `partial`), `contextvars`, decorator có tham số, descriptor và metaclass ở mức khái niệm.
* **14.3. [Mở rộng] Hiệu năng và lựa chọn ngôn ngữ**
  * `cProfile`, `py-spy`, khi nào chuyển phần nóng sang Cython/mypyc, và khi nào nên chọn Go/Rust cho công cụ CLI cần hiệu năng cao hoặc phân phối một file nhị phân duy nhất.
* **14.4. [Mở rộng] Python trong hệ sinh thái DevOps**
  * Ansible (module viết bằng Python), Pulumi và AWS CDK (hạ tầng bằng mã với Python), Airflow (điều phối workflow), Fabric, `kopf` (Operator Kubernetes), FastAPI cho công cụ nội bộ/webhook, Jupyter để điều tra sự cố.

---

## 📊 TỔNG KẾT QUY MÔ GIÁO TRÌNH (ĐẾM THỰC TẾ)

* **Tổng số module:** 15 module (Module 0 → Module 14).
* **Tổng số bài Lab thực hành:** 14 bài lab (Module 0 → Module 13; Module 14 là phụ lục mở rộng không có lab).
* **Tổng số Case Study sự cố production:** 28 kịch bản (Module 0 → Module 13, mỗi module 2 case; Module 14 không có case).
* **Tổng số từ dự kiến toàn giáo trình:** ~57.500 từ (bằng tổng ước lượng của 15 module).
* **Tài liệu bàn giao sau khi hoàn thành toàn bộ module:**
  1. Bảng thuật ngữ chuyên ngành Anh – Việt.
  2. Cheat Sheet lệnh và thư viện tổng hợp dành cho người viết script vận hành.
  3. Bộ 20 câu hỏi phỏng vấn DevOps/SRE mức Junior–Mid có lời giải chi tiết.
  4. Lộ trình ôn tập 4 tuần có phân bổ thời gian cụ thể.

---

## 📚 TÀI LIỆU THAM KHẢO CHÍNH THỨC

* Tài liệu Python (ngôn ngữ, thư viện chuẩn, "What's New"): https://docs.python.org/3/
* Lịch phát hành và vòng đời các phiên bản Python: https://devguide.python.org/versions/
* Python Packaging User Guide (pip, venv, pyproject.toml, wheel): https://packaging.python.org/
* PEP 8 (phong cách code) và PEP 668 (môi trường do hệ điều hành quản lý): https://peps.python.org/
* Tài liệu boto3 và botocore: https://boto3.amazonaws.com/v1/documentation/api/latest/index.html
* Tài liệu `pytest`: https://docs.pytest.org/
