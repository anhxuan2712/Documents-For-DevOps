# GIÁO TRÌNH HỆ ĐIỀU HÀNH (LINUX) THỰC CHIẾN DÀNH CHO DEVOPS / PLATFORM / SRE
*Hiểu bản chất — Đọc được hệ thống đang chạy — Vận hành Production & Phỏng vấn Junior/Mid*

---

## 🎯 CÁCH DÙNG TÀI LIỆU NÀY

* **Đối tượng:** Người mới vào DevOps/Platform/SRE, đã biết mở terminal và gõ các lệnh cơ bản (`ls`, `cd`, `ssh`). Không cần nền tảng lập trình.
* **Đây là README (khung giáo trình):** gồm lộ trình, mục lục chi tiết, bài lab và case study cho từng module. Nội dung chi tiết từng module sẽ được viết thành file riêng theo cùng cấu trúc 10 mục (mục tiêu, vấn đề thực tế, nguyên lý, chi tiết kỹ thuật, lệnh thực hành, lab, case study, hiểu lầm phổ biến, câu hỏi tự kiểm tra, tóm tắt và cheat sheet).
* **Cách học hiệu quả:** học theo vòng **Lab → Case study → đọc lý thuyết**, không đọc một mạch hết lý thuyết rồi mới làm. Tự gõ lệnh, không chỉ copy-paste. Ghi các lệnh đã chạy thật vào cheat sheet riêng của bạn.
* **Môi trường lab khuyến nghị:**
  * 1 máy ảo Linux (Ubuntu Server LTS 24.04 hoặc 26.04), có quyền `sudo`, tối thiểu 2 vCPU / 4 GB RAM / 20 GB đĩa. Chụp snapshot trước khi thử các lệnh có rủi ro.
  * 1 máy ảo thứ hai thuộc họ RHEL (Rocky Linux hoặc AlmaLinux 9 trở lên) cho các bài về SELinux và `dnf` (Module 8, Module 10).
  * Docker (hoặc Podman) cho Module 1, 5 và 11.
  * **Không chạy lab trên máy production hoặc máy của công ty.**
* **Quy ước nhãn:** `[Mở rộng]` = đọc lướt, tra khi cần. `[CẦN XÁC MINH]` = thông tin phụ thuộc phiên bản, hãy đối chiếu tài liệu chính thức hoặc chạy thử trên máy của bạn trước khi tin.
* **Về phiên bản (tham chiếu tháng 11/2026):** Ubuntu 26.04 LTS phát hành ngày 23/04/2026 (kernel 7.0, systemd 259); Ubuntu 24.04 LTS dùng kernel 6.8 và systemd 255. Hãy luôn kiểm tra máy của bạn bằng `cat /etc/os-release`, `uname -r` và `systemctl --version`. Mọi ví dụ lệnh cần được chạy thử và đối chiếu với `man` của phiên bản đang dùng.

---

## 🧭 LỘ TRÌNH HỌC TẬP ĐỀ XUẤT

### 1. LỘ TRÌNH TẬP TRUNG 4 TUẦN (toàn thời gian, ước tính khoảng 60–100 giờ)

```
[Tuần 1: Tư duy khảo sát, Shell, File & Quyền (~15.500 từ)]
  Module 0 → Module 1 → Module 2 → Module 3

[Tuần 2: Lưu trữ, Tiến trình, Bộ nhớ & CPU (~16.500 từ)]
  Module 4 → Module 5 → Module 6 → Module 7

[Tuần 3: Bảo mật, systemd, Package & Nền tảng Container (~16.500 từ)]
  Module 8 → Module 9 → Module 10 → Module 11

[Tuần 4: Tinh chỉnh, Tự động hóa, Phụ lục + Ôn tập & Dự án tổng hợp (~9.000 từ)]
  Module 12 → Module 13 → Module 14 (Phụ lục)
```

*Tuần 4 nhẹ hơn về lý thuyết để dành thời gian ôn tập và làm một dự án tổng hợp (ví dụ: dựng một VM "production nhỏ" có SSH hardening, service systemd, log rotation, giới hạn tài nguyên bằng cgroup, và một bộ cron/timer sao lưu).*

### 2. LỘ TRÌNH BÁN THỜI GIAN 10–12 TUẦN (8–10 giờ/tuần)

| Tầng Ưu Tiên | Danh Sách Module | Hướng Dẫn Tiếp Cận |
| :--- | :--- | :--- |
| **Tầng 1: Cốt lõi** | **Module 0, Module 2, Module 3, Module 5, Module 6, Module 8, Module 9, Module 11** | Học kỹ lý thuyết, làm đầy đủ bài lab, nắm chắc từng case study. Đây là phần gặp hằng ngày khi vận hành server và container. |
| **Tầng 2: Quan trọng** | **Module 1, Module 4, Module 7, Module 10, Module 12, Module 13** | Đọc kỹ nguyên lý, làm các bài lab chọn lọc phục vụ công việc. |
| **Tầng 3: Mở rộng** | **Module 14 (Phụ lục)** và các mục gắn nhãn `[Mở rộng]` | Đọc lướt nắm khái niệm, tra cứu khi thiết kế kiến trúc nâng cao hoặc phỏng vấn chuyên sâu. |

### 3. LIÊN HỆ VỚI CÁC GIÁO TRÌNH KHÁC TRONG BỘ NỀN TẢNG DEVOPS

* **Python Scripting:** học song song với phần Shell (Module 2) và Tiến trình (Module 5). Các script vận hành bằng Python sẽ dùng kiến thức file, quyền, tiến trình, systemd ở giáo trình này.
* **Mạng máy tính (Computer Networking):** nên học sau khi nắm Module 0–5 của giáo trình này. Các mục về netns, Netfilter, sysctl mạng ở giáo trình Mạng nối tiếp trực tiếp với Module 11 và Module 12 ở đây.

---

## 📋 MỤC LỤC CHI TIẾT

---

### MODULE 0: TƯ DUY KHẢO SÁT HỆ THỐNG & HỘP CÔNG CỤ NỀN TẢNG
*Ước lượng: ~3.500 từ*
*🎯 Học xong làm được: vào một server lạ, trong vài phút biết tài nguyên nào (CPU, RAM, đĩa, mạng) đang nghẽn, và thao tác an toàn.*

* **0.1. Phương pháp luận xử lý sự cố trên Linux**
  * Quy trình: Triệu chứng → Giả thuyết → Kiểm chứng → Giảm thiểu → Root Cause → Postmortem.
  * Phương pháp USE (Utilization, Saturation, Errors) áp dụng cho CPU, bộ nhớ, đĩa, mạng. Nguyên tắc "đo trước, sửa sau", không đoán mò.
* **0.2. Tự học từ tài liệu có sẵn**
  * `man` (section 1: lệnh, 5: file cấu hình, 8: quản trị), `--help`, `apropos`, `/usr/share/doc`, `info`.
  * Cách đọc một man page: SYNOPSIS, OPTIONS, EXAMPLES, SEE ALSO, và tra cứu bản trực tuyến tại man7.org.
* **0.3. "60 giây đầu tiên" khi vào một server (checklist 10 lệnh)**
  * `uptime`, `dmesg -T | tail`, `vmstat 1`, `mpstat -P ALL 1`, `pidstat 1`, `iostat -xz 1`, `free -m`, `sar -n DEV 1`, `sar -n TCP,ETCP 1`, `top` (các lệnh `mpstat`, `pidstat`, `iostat`, `sar` nằm trong gói `sysstat`).
  * Mỗi lệnh trả lời một câu hỏi cụ thể: máy có đang quá tải không, có lỗi phần cứng/kernel không, nghẽn ở CPU, bộ nhớ, đĩa hay mạng. Chi tiết từng loại tài nguyên xem Module 4, 5, 6, 7.
* **0.4. Công cụ quan sát tiến trình và file đang mở**
  * `ps`, `top`/`htop`, `lsof`, giới thiệu `strace`, `journalctl`, `dmesg`.
  * `/proc` và `/sys`: kernel công bố thông tin dưới dạng file (đọc bằng `cat`).
* **0.5. Thao tác an toàn trên máy thật**
  * Kiểm tra `hostname` trước khi gõ lệnh phá hoại, dùng `--dry-run` khi có, sao lưu cấu hình trước khi sửa (`cp -a file file.bak`).
  * Dùng `tmux`/`screen` để không mất phiên khi rớt SSH. Mỗi lần chỉ thay đổi một thứ và có đường lui (rollback).
* **Lab thực hành:** Tạo sự cố "server chậm" có chủ đích trên VM (tiến trình ăn CPU, ăn RAM, ghi đĩa liên tục bằng `stress-ng` hoặc `dd`), dùng checklist 60 giây để xác định tài nguyên nào đang nghẽn mà không biết trước nguyên nhân.
* **Case study sự cố:**
  1. *Case 1:* Load average 25 trên máy 4 vCPU nhưng CPU idle 80%: nguyên nhân là nhiều tiến trình ở trạng thái `D` chờ I/O (xem Mục 5.2, 5.5 và `iostat` ở Mục 4.5).
  2. *Case 2:* Mất phiên SSH giữa lúc đang chạy lệnh dài (nâng cấp gói, di chuyển dữ liệu) khiến thao tác dở dang; khắc phục bằng `tmux` và quy trình có thể chạy lại (resume).

---

### MODULE 1: KIẾN TRÚC HỆ ĐIỀU HÀNH & LINUX
*Ước lượng: ~3.500 từ*
*🎯 Học xong làm được: giải thích được ứng dụng nói chuyện với kernel thế nào, chọn được distro phù hợp và hiểu vì sao image Alpine khác Ubuntu.*

* **1.1. Hệ điều hành làm những việc gì**
  * Trừu tượng hóa phần cứng, quản lý tài nguyên (CPU, bộ nhớ, I/O), cô lập tiến trình, cung cấp API cho ứng dụng.
  * Chế độ kernel (kernel mode) và chế độ người dùng (user mode): vì sao ứng dụng không chạm trực tiếp vào phần cứng.
* **1.2. System call**
  * Khái niệm; các syscall tiêu biểu: `open`, `read`, `write`, `fork`, `execve`, `mmap`, `socket`.
  * Thư viện C (libc) bọc syscall; vDSO giúp một số lời gọi như `clock_gettime` không cần vào kernel.
  * Quan sát bằng `strace -c` (thống kê), `strace -f -e trace=file`. Chi phí của syscall và chuyển ngữ cảnh (context switch).
* **1.3. Kiến trúc Linux**
  * Kernel nguyên khối (monolithic) có thể nạp module (`lsmod`, `modinfo`, `modprobe`); các hệ thống con: VFS, lập lịch, quản lý bộ nhớ, mạng, block layer.
  * Phiên bản kernel (`uname -r`), kernel LTS; "distro = kernel + userland (GNU coreutils, glibc, trình khởi tạo)".
  * `/proc`, `/sys`, `/dev` là các giao diện của kernel dưới dạng file.
* **1.4. Họ distro và cách chọn**
  * Debian/Ubuntu (`apt`, `.deb`), RHEL/Rocky/AlmaLinux/Fedora/Amazon Linux (`dnf`, `.rpm`), Alpine (`apk`, musl, BusyBox), SUSE.
  * Bản LTS và vòng đời hỗ trợ; glibc so với musl (khác biệt hành vi và tương thích binary, ảnh hưởng khi chọn base image cho container).
* **1.5. Quy trình khởi động ở mức tổng quan**
  * Firmware (UEFI/BIOS) → bootloader (GRUB) → kernel + initramfs → PID 1 (systemd) → targets. Chi tiết và cách khôi phục xem Mục 9.4.
* **Lab thực hành:** Khám phá hệ thống đang chạy (`cat /etc/os-release`, `uname -a`, `lsmod`, `ls /proc`), dùng `strace -c` và `strace -f -e trace=openat` để thấy một lệnh đơn giản gọi những syscall nào, chạy cùng một lệnh trong container Ubuntu và Alpine để so sánh (`ldd`, `file`).
* **Case study sự cố:**
  1. *Case 1:* Binary build trên Ubuntu (glibc) chạy trên Alpine (musl) báo lỗi `not found` dù file tồn tại; chẩn đoán bằng `file`, `ldd` và hiểu liên kết động so với liên kết tĩnh.
  2. *Case 2:* Ứng dụng chậm bất thường vì ghi từng byte một (hàng triệu syscall nhỏ, không có bộ đệm); `strace -c` chỉ ra `write` chiếm phần lớn thời gian.

---

### MODULE 2: SHELL & DÒNG LỆNH
*Ước lượng: ~4.500 từ*
*🎯 Học xong làm được: kết hợp lệnh bằng pipe để phân tích log nhanh và viết một Bash script an toàn, có thể chạy lại nhiều lần.*

* **2.1. Shell là gì**
  * Phân biệt terminal, shell và TTY. Bash so với `sh` (trên Debian/Ubuntu `/bin/sh` thường là `dash`, thiếu một số tính năng của Bash như `[[ ]]` và mảng), zsh.
  * Shell tương tác và không tương tác, login và non-login; các file khởi tạo (`~/.bashrc`, `~/.profile`, `/etc/profile`). Shebang `#!/usr/bin/env bash`.
* **2.2. Biến, môi trường và quoting**
  * Biến shell so với biến môi trường (`export`), `PATH`, mở rộng tham số (`${var:-mặc định}`), thay thế lệnh `$(...)`, số học `$((...))`.
  * Quote: nháy đơn và nháy kép; vì sao hầu như luôn phải đặt `"$biến"` trong nháy kép (tách từ và mở rộng ký tự đại diện).
* **2.3. Pipe, redirect và file descriptor**
  * stdin/stdout/stderr (0/1/2), `>`, `>>`, `2>&1`, `|`, `tee`, here-document, process substitution `<(...)`, `/dev/null`.
  * Mã thoát `$?`, toán tử `&&` và `||`, `pipefail`.
* **2.4. Bộ công cụ xử lý văn bản**
  * `grep` (`-E`, `-r`, `-n`), `sed` (`s///`, `-i`), `awk` (trường, điều kiện), `cut`, `sort`, `uniq -c`, `tr`, `wc`, `head`, `tail -f`.
  * `find` (`-name`, `-mtime`, `-size`, `-exec`), `xargs` (`-0`, `-P`), `jq` để xử lý JSON (cần cài thêm). Biểu thức chính quy cơ bản (BRE/ERE).
* **2.5. Viết Bash script an toàn**
  * Cấu trúc script, kiểm tra tham số, hàm, `getopts`, `mktemp`, `trap` để dọn dẹp.
  * `set -euo pipefail` và các bẫy của `set -e` (không có tác dụng trong điều kiện `if`, sau `||`, trong một số trường hợp subshell). Dùng ShellCheck để kiểm tra lỗi.
  * Nguyên tắc script có thể chạy lại (idempotent), hỗ trợ `--dry-run`. Khi logic phức tạp hoặc cần gọi API, nên chuyển sang Python (xem giáo trình Python Scripting).
* **2.6. Điều khiển job và phiên làm việc**
  * `&`, `jobs`, `fg`/`bg`, `nohup`, `disown`, `tmux`/`screen`, `timeout`, `watch`, phím tắt `Ctrl+C` và `Ctrl+Z`.
* **Lab thực hành:** Dùng pipeline `grep`/`awk`/`sort`/`uniq` phân tích access log Nginx mẫu (top 10 IP, tỷ lệ mã 5xx theo phút). Viết script sao lưu một thư mục có `set -euo pipefail`, `trap` dọn dẹp, tùy chọn `--dry-run` và không còn cảnh báo ShellCheck.
* **Case study sự cố:**
  1. *Case 1:* Lệnh `rm -rf "$DIR"/*` với `$DIR` rỗng trở thành `rm -rf /*` và xóa hàng loạt dữ liệu; phòng tránh bằng `set -u`, `${DIR:?}` và kiểm tra trước khi xóa.
  2. *Case 2:* Script chạy tay thì đúng nhưng chạy bằng cron thì báo `command not found` hoặc sai đường dẫn, do môi trường cron tối giản (xem Mục 13.1).

---

### MODULE 3: HỆ THỐNG TỆP & QUYỀN TRUY CẬP
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: đọc hiểu `ls -l`, giải thích và sửa lỗi `Permission denied`, thiết lập thư mục dùng chung cho nhóm một cách đúng đắn.*

* **3.1. Cây thư mục chuẩn (FHS)**
  * `/etc`, `/var`, `/usr`, `/opt`, `/home`, `/tmp`, `/run`, `/boot`, `/srv`, và các hệ thống tệp ảo `/proc`, `/sys`, `/dev`. Khái niệm tmpfs, merged-usr (`/bin` liên kết tới `/usr/bin`).
* **3.2. "Mọi thứ là file", inode và liên kết**
  * Các loại file: thường, thư mục, symlink, thiết bị khối/ký tự, socket, FIFO.
  * inode chứa metadata (không chứa tên); hard link so với symbolic link; số link; xóa file thực chất là `unlink`. Công cụ `ls -li`, `stat`, `ln`.
* **3.3. Quyền rwx và quyền sở hữu**
  * user/group/other, `chmod` (dạng số và dạng ký hiệu), `chown`, `umask`.
  * Ý nghĩa quyền trên thư mục (`x` = cho phép đi qua), setuid, setgid, sticky bit (ví dụ `/tmp` có mode `1777`).
  * `umask` mặc định `022` trên nhiều distro; họ RHEL thường dùng `002` cho người dùng thường (nhóm riêng theo người dùng).
* **3.4. ACL và thuộc tính mở rộng**
  * `getfacl`/`setfacl` (ACL mặc định cho thư mục), `chattr +i`/`lsattr` (file bất biến).
* **3.5. Tìm, sao chép và thao tác file an toàn**
  * `find`, `du -sh`, `df -h`, `ls -lah`, `rsync` (`-a`, `--delete`, `--dry-run`), `tar`, nén `gzip`/`zstd`, `cp -a`, `scp`, kiểm tra toàn vẹn `sha256sum`.
  * Mẫu ghi file nguyên tử (ghi file tạm rồi `mv`), khóa file bằng `flock`.
* **Lab thực hành:** Dựng thư mục dùng chung cho nhóm dev (group riêng, setgid, `umask`, ACL mặc định), thực nghiệm hard link so với symlink khi xóa và đổi tên file, quan sát số inode bằng `stat`.
* **Case study sự cố:**
  1. *Case 1:* Ứng dụng báo `Permission denied` khi đọc file dù chủ sở hữu và quyền file đúng, do thiếu quyền `x` trên một thư mục cha; chẩn đoán bằng `namei -l`.
  2. *Case 2:* Sau deploy, file do user khác tạo ra không ghi được vì thiếu setgid/`umask`/ACL mặc định cho thư mục chung.

---

### MODULE 4: LƯU TRỮ, FILESYSTEM & I/O
*Ước lượng: ~4.500 từ*
*🎯 Học xong làm được: thêm và mở rộng đĩa an toàn, tìm nguyên nhân đĩa đầy, đọc được số liệu `iostat` để biết đĩa có nghẽn không.*

* **4.1. Block device và phân vùng**
  * `lsblk`, `blkid`, `fdisk`/`parted`; MBR so với GPT. Tên thiết bị (`/dev/sda`, `/dev/nvme0n1`) không ổn định, nên dùng UUID/LABEL. Cách đĩa cloud hiển thị trong Linux.
* **4.2. Filesystem và mount**
  * ext4, XFS, Btrfs: đặc điểm chính (XFS chỉ mở rộng chứ không thu nhỏ được; ext4 thu nhỏ được khi ngắt mount). `mkfs`, `mount`, `findmnt`.
  * `/etc/fstab`: các trường, UUID, tùy chọn `nofail` và `noatime`. tmpfs, giới thiệu NFS, khái niệm journaling, `fsck`.
* **4.3. LVM và mở rộng đĩa**
  * PV/VG/LV, `pvcreate`, `vgextend`, `lvextend -r`; `growpart`, `resize2fs`, `xfs_growfs`. Quy trình mở rộng volume cloud khi hệ thống đang chạy; khái niệm snapshot.
* **4.4. Dung lượng và inode**
  * `df -h`, `df -i`, `du`, `ncdu`. Hết inode do hàng triệu file nhỏ; khối dự trữ (reserved blocks) của ext4.
  * File đã bị xóa nhưng tiến trình vẫn đang mở vẫn chiếm dung lượng (`lsof +L1`). Xoay vòng log để tránh đầy đĩa (xem Mục 9.5).
* **4.5. Page cache và I/O**
  * Đọc/ghi đi qua page cache; dirty page và writeback; `sync` và `fsync` (độ bền dữ liệu).
  * I/O scheduler (`none`, `mq-deadline`, `bfq`, `kyber`). IOPS, thông lượng và độ trễ.
  * Đọc `iostat -xz` (các cột `r/s`, `w/s`, `await`, `aqu-sz`, `%util`; lưu ý `%util` kém ý nghĩa với thiết bị xử lý song song như NVMe), `pidstat -d`, `iotop`. Giới hạn IOPS/băng thông và burst của volume cloud.
* **4.6. RAID và độ bền dữ liệu**
  * RAID 0/1/5/6/10, giới thiệu `mdadm`. RAID không phải sao lưu; snapshot không phải sao lưu; quy tắc 3-2-1 và việc kiểm tra khôi phục định kỳ.
* **4.7. OverlayFS và lưu trữ của container**
  * lowerdir/upperdir/merged, copy-on-write; thư mục `/var/lib/docker/overlay2`; vì sao đĩa của node bị đầy (xem thêm Mục 11.5).
* **Lab thực hành:** Thêm một đĩa ảo vào VM, tạo bảng phân vùng GPT, tạo LVM, `mkfs`, mount, ghi vào `fstab` bằng UUID, rồi mở rộng online. Tạo tình huống hết inode và tình huống "đĩa đầy ảo" do file đã xóa nhưng còn mở.
* **Case study sự cố:**
  1. *Case 1:* `df` báo 100% nhưng `du` chỉ thấy 40%: file log đã bị xóa nhưng tiến trình vẫn giữ mở; chẩn đoán bằng `lsof +L1` và xử lý bằng cách truncate qua `/proc/<pid>/fd/<n>` hoặc restart có kiểm soát.
  2. *Case 2:* Server không boot được sau khi reboot, rơi vào emergency mode do dòng `/etc/fstab` sai hoặc UUID không còn tồn tại (thiếu `nofail`); xem cách khôi phục ở Mục 9.4.

---

### MODULE 5: TIẾN TRÌNH, TÍN HIỆU & TÀI NGUYÊN
*Ước lượng: ~4.500 từ*
*🎯 Học xong làm được: đọc trạng thái tiến trình, dừng dịch vụ đúng cách, xử lý lỗi `Too many open files` và hiểu vì sao container cần init.*

* **5.1. Tiến trình và luồng**
  * PID, PPID; `fork()`, `exec()`, `wait()`; copy-on-write; luồng là tác vụ chia sẻ không gian địa chỉ (`clone()`).
  * `ps -ef`, `ps aux`, `pstree`, `ps -eLf` để xem cả luồng.
* **5.2. Trạng thái tiến trình**
  * `R` (chạy), `S` (ngủ có thể ngắt), `D` (ngủ không thể ngắt, thường chờ I/O), `Z` (zombie), `T` (dừng), `I` (luồng kernel rảnh). Vì sao tiến trình ở trạng thái `D` không `kill` được.
* **5.3. Tín hiệu (signal)**
  * `SIGTERM` (15), `SIGKILL` (9), `SIGINT` (2), `SIGHUP` (1), `SIGSTOP`/`SIGCONT`, `SIGCHLD`, `SIGPIPE`, `SIGUSR1/2`. `SIGKILL` và `SIGSTOP` không thể bị bắt.
  * `kill`, `pkill`, `killall`. Mẫu tắt êm (graceful shutdown): nhận `SIGTERM` → hoàn tất công việc đang làm → thoát. Docker và Kubernetes gửi `SIGTERM` trước, sau thời gian chờ (Kubernetes mặc định 30 giây; `docker stop` mặc định 10 giây) mới gửi `SIGKILL`.
* **5.4. PID 1, zombie và orphan**
  * Zombie là tiến trình đã kết thúc nhưng cha chưa gọi `wait()`; orphan được tiến trình PID 1 nhận nuôi.
  * PID 1 trong container phải biết thu dọn zombie và chuyển tiếp tín hiệu: dùng `docker run --init` hoặc `tini`. Dạng exec và dạng shell của `CMD`/`ENTRYPOINT` trong Dockerfile (dạng shell thường chạy qua `/bin/sh -c` và có thể không chuyển tiếp `SIGTERM`). Liên hệ PID namespace ở Mục 11.2.
* **5.5. Load average và cách đọc `top`**
  * Load average trên Linux gồm tiến trình đang chạy/chờ chạy cộng tiến trình ở trạng thái `D`, tính trung bình 1/5/15 phút; không phải phần trăm CPU. So sánh với số core (`nproc`).
  * `top`: các dòng CPU (`us`, `sy`, `ni`, `id`, `wa`, `hi`, `si`, `st`) và các cột `VIRT`/`RES`/`SHR`/`S`/`%CPU`; `htop`.
* **5.6. File descriptor và giới hạn tài nguyên**
  * fd (file, socket, pipe), `ulimit -n`, `/proc/<pid>/limits`, `/proc/<pid>/fd`, `lsof`, `fs.file-max`. Lỗi `Too many open files`.
  * `ulimit` và `/etc/security/limits.conf` (do PAM áp dụng cho phiên đăng nhập) không áp dụng cho dịch vụ chạy bằng systemd; dùng `LimitNOFILE=` trong unit (xem Mục 9.2 và 12.3).
* **5.7. Điều khiển ưu tiên**
  * `nice`/`renice` (từ -20 đến 19), `ionice`, `taskset` (gán CPU). Giới hạn ở mức cấu trúc dùng cgroup (xem Mục 11.3).
* **5.8. Gỡ lỗi một tiến trình đang chạy**
  * `strace -p`, `lsof -p`, các file `/proc/<pid>/status`, `/proc/<pid>/wchan`, `/proc/<pid>/environ`; core dump xem Mục 12.4.
* **Lab thực hành:** Tạo tiến trình zombie bằng một script nhỏ (fork mà không `wait`) và quan sát trạng thái `Z`; so sánh `SIGTERM` với `SIGKILL` và viết handler `trap` trong Bash; đặt `ulimit -n` thấp rồi mở nhiều file để gây lỗi `Too many open files`; chạy container có và không có `--init` để so sánh.
* **Case study sự cố:**
  1. *Case 1:* Container tích tụ hàng nghìn tiến trình zombie cho đến khi cạn PID, do tiến trình PID 1 không thu dọn tiến trình con; khắc phục bằng `--init`/`tini`.
  2. *Case 2:* Mỗi lần deploy, một số request bị cắt ngang vì dịch vụ không xử lý `SIGTERM` (hoặc shell bọc ngoài nuốt tín hiệu) nên bị `SIGKILL` sau hết thời gian chờ.

---

### MODULE 6: QUẢN LÝ BỘ NHỚ
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: đọc đúng `free`, giải thích vì sao tiến trình bị OOM-kill và phân biệt rò rỉ bộ nhớ với page cache.*

* **6.1. Bộ nhớ ảo và phân trang**
  * Không gian địa chỉ ảo, trang nhớ (thường 4 KiB), bảng trang, MMU, page fault (minor và major), `mmap`, nạp trang theo yêu cầu.
  * `VSZ`, `RSS`, `PSS` khác nhau thế nào và vì sao `VSZ` lớn không có nghĩa là dùng nhiều RAM.
* **6.2. Đọc `free`, `/proc/meminfo`, `vmstat`**
  * Cột `used`, `free`, `buff/cache`, `available`: dùng `available` để đánh giá còn bao nhiêu bộ nhớ, không dùng `free`. Page cache là bộ nhớ "mượn" có thể thu hồi.
  * `slab` (`slabtop`), `Dirty`, `Writeback`, `Committed_AS`.
* **6.3. Swap và `swappiness`**
  * Swap giải phóng các trang ẩn danh ít dùng; `vm.swappiness`; hiện tượng thrashing (cột `si`/`so` của `vmstat`); giới thiệu zswap/zram.
  * Có nên tắt swap không: Kubernetes truyền thống yêu cầu tắt swap, các phiên bản mới có hỗ trợ swap theo cấu hình [CẦN XÁC MINH theo phiên bản].
* **6.4. OOM killer**
  * Khi nào kích hoạt; chọn nạn nhân theo `oom_score` và `oom_score_adj` (từ -1000 đến 1000; -1000 loại trừ khỏi OOM killer); `vm.overcommit_memory` (0, 1, 2).
  * Đọc log: `dmesg | grep -i "killed process"`. Mã thoát 137 = 128 + 9 (`SIGKILL`). Phân biệt OOM toàn hệ thống với OOM trong cgroup (xem Mục 11.3).
* **6.5. HugePages và Transparent Huge Pages**
  * HugePages tĩnh so với THP (`always`, `madvise`, `never` tại `/sys/kernel/mm/transparent_hugepage/enabled`). Một số cơ sở dữ liệu như Redis và MongoDB khuyến nghị tắt THP; hãy xem tài liệu của từng sản phẩm.
* **6.6. NUMA và giới hạn bộ nhớ**
  * Khái niệm NUMA, `numactl --hardware`. Giới hạn bộ nhớ theo cgroup xem Mục 11.3.
* **6.7. Chẩn đoán rò rỉ bộ nhớ**
  * Theo dõi RSS theo thời gian (`pidstat -r`, `/proc/<pid>/smaps_rollup`); phân biệt rò rỉ thật với cache tăng tự nhiên; công cụ theo ngôn ngữ (heap dump của Java, `tracemalloc` của Python); giới thiệu `memleak` của eBPF.
* **Lab thực hành:** Dùng `stress-ng --vm` hoặc script nhỏ để ăn RAM và quan sát `free`, `vmstat`, `dmesg`; tạo OOM trong cgroup giới hạn bằng `systemd-run --scope -p MemoryMax=200M` (xem Mục 11.3); chỉnh `oom_score_adj` để bảo vệ `sshd`.
* **Case study sự cố:**
  1. *Case 1:* Giám sát báo RAM 95% "sắp hết" nhưng hệ thống hoạt động bình thường, do nhầm page cache là bộ nhớ đang dùng.
  2. *Case 2:* OOM killer của hệ thống giết nhầm tiến trình cơ sở dữ liệu thay vì ứng dụng đang ăn RAM; khắc phục bằng `oom_score_adj` và đặt giới hạn bộ nhớ đúng chỗ.

---

### MODULE 7: CPU, LẬP LỊCH & PHÂN TÍCH HIỆU NĂNG
*Ước lượng: ~3.500 từ*
*🎯 Học xong làm được: phân biệt CPU bận, I/O wait và steal time, và dùng phương pháp có hệ thống để tìm điểm nghẽn.*

* **7.1. CPU, core, luồng**
  * Socket/core/hyper-thread (`lscpu`, `nproc`); vCPU trong cloud thường tương ứng một hyper-thread; chuyển ngữ cảnh, ngắt, softirq.
* **7.2. Bộ lập lịch Linux**
  * Chia thời gian CPU, trọng số theo `nice`, các lớp lập lịch (`SCHED_OTHER`, `SCHED_FIFO`, `SCHED_RR`, `SCHED_DEADLINE`). EEVDF thay thế CFS làm bộ lập lịch mặc định từ Linux 6.6.
* **7.3. Đọc thời gian CPU**
  * Các trạng thái `us`, `sy`, `ni`, `id`, `wa`, `hi`, `si`, `st`; `mpstat -P ALL`, `pidstat`. `st` (steal) trong máy ảo; I/O wait không có nghĩa CPU bận; nghẽn một luồng (một core 100%).
* **7.4. Load average, utilization và saturation**
  * Hàng đợi chạy (`vmstat` cột `r`) và dấu hiệu bão hòa; vì sao load cao có thể do trạng thái `D` (xem Mục 5.5).
* **7.5. CPU throttling trong cgroup/container**
  * Cơ chế quota và period (`cpu.max`), các bộ đếm `nr_throttled` và `throttled_usec` trong `cpu.stat`; giới hạn CPU của Kubernetes có thể gây throttle dù node còn rảnh. Chi tiết xem Mục 11.3.
* **7.6. Phương pháp và công cụ phân tích hiệu năng**
  * Phương pháp USE, `perf top`, `perf record -g`, khái niệm flame graph, `pidstat -w` (chuyển ngữ cảnh).
* **Lab thực hành:** Tạo tiến trình ăn CPU, so sánh chạy với `nice` 0 và 19, quan sát bằng `mpstat` và `top`; dùng `perf top` (nếu có) để xem hàm nào tiêu tốn CPU; đọc `st` trên một VM cloud.
* **Case study sự cố:**
  1. *Case 1:* Dịch vụ phản hồi chậm dù CPU tổng chỉ 25%, vì một core ở 100% (điểm nghẽn đơn luồng); phát hiện bằng `mpstat -P ALL`.
  2. *Case 2:* Máy ảo cloud chậm bất thường nhưng không tiến trình nào ăn CPU: steal time cao do hàng xóm ồn hoặc hết CPU credit (instance dạng burstable).

---

### MODULE 8: NGƯỜI DÙNG, SSH & BẢO MẬT HỆ ĐIỀU HÀNH
*Ước lượng: ~4.000 từ*
*🎯 Học xong làm được: cấu hình SSH an toàn, quản lý user/sudo đúng nguyên tắc tối thiểu quyền và xử lý được lỗi SELinux thay vì tắt nó.*

* **8.1. Người dùng và nhóm**
  * `/etc/passwd`, `/etc/shadow`, `/etc/group`; UID/GID (root là 0; tài khoản hệ thống thường dưới 1000); `useradd`, `usermod`, `userdel`, `id`, `getent`; shell `nologin`; tài khoản dịch vụ; `su` so với `sudo`.
* **8.2. sudo và nguyên tắc đặc quyền tối thiểu**
  * `visudo`, `/etc/sudoers.d/`, nhóm `sudo`/`wheel`, cân nhắc `NOPASSWD`, log của `sudo`. Ubuntu mới có thể dùng bản `sudo-rs` làm mặc định [CẦN XÁC MINH theo phiên bản], hãy đối chiếu ghi chú phát hành.
* **8.3. SSH chuẩn production**
  * Khóa `ed25519` (`ssh-keygen -t ed25519`), `~/.ssh/authorized_keys`, quyền thư mục và file (`StrictModes`).
  * Củng cố `sshd_config`: `PasswordAuthentication no`, `PermitRootLogin`, `AllowUsers`/`AllowGroups`; đổi cổng không phải là biện pháp bảo mật thực sự.
  * `ssh-agent` và rủi ro của agent forwarding, `~/.ssh/config`, `ProxyJump`, chuyển tiếp cổng (`-L`, `-R`, `-D`), `known_hosts` và dấu vân tay host key, giới thiệu chứng chỉ SSH.
  * Kiểm tra cấu hình bằng `sshd -t` trước khi reload và luôn giữ một phiên SSH dự phòng khi sửa cấu hình.
* **8.4. PAM, mật khẩu và xác thực**
  * Khái niệm PAM (`/etc/pam.d`), `pam_limits`, chính sách mật khẩu, khóa tài khoản khi đăng nhập sai (`pam_faillock`), nhắc đến fail2ban và xác thực 2 yếu tố.
* **8.5. Capabilities và giảm đặc quyền**
  * Linux capabilities (`CAP_NET_BIND_SERVICE`, `CAP_SYS_ADMIN`, ...), `getcap`/`setcap`; vì sao không chạy ứng dụng bằng root trong container; rủi ro của setuid; `no_new_privs`.
* **8.6. SELinux và AppArmor**
  * DAC so với MAC. SELinux (họ RHEL): các chế độ enforcing/permissive/disabled, `getenforce`, `setenforce`, ngữ cảnh (`ls -Z`), `restorecon`, `semanage fcontext`, boolean (`setsebool -P`), đọc AVC bằng `ausearch -m avc`, `sealert`.
  * AppArmor (Ubuntu/Debian): profile, `aa-status`, chế độ complain và enforce. Không tắt MAC như phản xạ khi gặp lỗi.
* **8.7. Firewall host, audit và vá bảo mật**
  * `ufw`, `firewalld`, `nftables` (chi tiết Netfilter xem giáo trình Mạng máy tính, Mục 8.2). `auditd`, `ss -ltnp` để rà các cổng đang lắng nghe, tắt dịch vụ không dùng, cập nhật bảo mật tự động (`unattended-upgrades`), nhắc đến CIS Benchmarks.
* **Lab thực hành:** Tạo user dịch vụ và thiết lập SSH chỉ dùng khóa với các tùy chọn củng cố (giữ phiên dự phòng), thử `AllowUsers`. Trên VM họ RHEL: cố ý gây lỗi SELinux (đổi thư mục gốc của web server), đọc AVC, rồi sửa bằng `semanage fcontext` và `restorecon`.
* **Case study sự cố:**
  1. *Case 1:* Khóa SSH đúng nhưng vẫn bị hỏi mật khẩu, do quyền hoặc chủ sở hữu của `~/.ssh` hay thư mục home quá rộng (`StrictModes`).
  2. *Case 2:* Nginx/httpd trả về 403 trên máy họ RHEL dù quyền file đúng, do ngữ cảnh SELinux của thư mục web sai.

---

### MODULE 9: SYSTEMD, KHỞI ĐỘNG & LOGGING
*Ước lượng: ~4.500 từ*
*🎯 Học xong làm được: biến một chương trình thành dịch vụ chạy ổn định, đọc log đúng cách và khôi phục máy không boot được.*

* **9.1. systemd và `systemctl`**
  * Các loại unit: service, socket, timer, mount, target, path. `start`/`stop`/`restart`/`reload`/`enable`/`disable`/`status`/`mask`; `enable` khác `start`; `daemon-reload`; `list-dependencies`; `systemctl cat`; `systemctl edit` (drop-in override) thay vì sửa file trong `/usr/lib`.
* **9.2. Viết unit file chuẩn**
  * `[Unit]`: `Description`, `After`/`Before`, `Requires`/`Wants` (`After=` chỉ quy định thứ tự, không tạo phụ thuộc); `network.target` so với `network-online.target`.
  * `[Service]`: `Type` (`simple`, `exec`, `forking`, `oneshot`, `notify`), `ExecStart`, `ExecReload`, `User`, `WorkingDirectory`, `EnvironmentFile`, `Restart=on-failure`, `RestartSec`, `TimeoutStopSec`, `LimitNOFILE`. Giới hạn khởi động lại `StartLimitIntervalSec`/`StartLimitBurst` (đặt trong `[Unit]`).
  * `[Install]`: `WantedBy=multi-user.target`. Củng cố bảo mật: `NoNewPrivileges`, `ProtectSystem`, `ProtectHome`, `PrivateTmp`, `ReadWritePaths`, `DynamicUser`, đo bằng `systemd-analyze security`.
* **9.3. systemd timers so với cron**
  * `OnCalendar`, `OnBootSec`, `Persistent=true`, kiểm tra biểu thức bằng `systemd-analyze calendar`. So sánh với cron (xem Mục 13.1).
* **9.4. Quy trình khởi động và khôi phục**
  * UEFI → GRUB → kernel và initramfs → systemd → `default.target`; `systemd-analyze blame` và `critical-chain`; các target `multi-user`, `rescue`, `emergency`; vào chế độ rescue bằng tham số kernel (`systemd.unit=rescue.target`), `/proc/cmdline`.
  * `fstab` sai dẫn đến emergency mode. Công cụ tạo initramfs có thể khác nhau tùy distro và phiên bản (`initramfs-tools`, `dracut`) [CẦN XÁC MINH theo phiên bản].
* **9.5. Logging**
  * journald: `journalctl -u <dịch vụ> -f`, `-b`, `-p err`, `--since`, `-o json`; lưu log bền vững (`/var/log/journal` hoặc `Storage=persistent`); giới hạn dung lượng (`SystemMaxUse`, `journalctl --vacuum-size`).
  * rsyslog và `/var/log` (`auth.log` so với `secure`, `syslog` so với `messages`), `logrotate` (`/etc/logrotate.d`, ưu và nhược của `copytruncate`), mức độ nghiêm trọng syslog (0–7), gửi log về hệ thống tập trung.
* **Lab thực hành:** Viết service systemd cho một HTTP server nhỏ (ví dụ `python3 -m http.server`) chạy bằng user riêng, `Restart=on-failure`, có tùy chọn củng cố; `kill -9` để xem tự khởi động lại. Viết timer chạy mỗi 5 phút, phân tích boot bằng `systemd-analyze blame`, cấu hình `logrotate` cho một file log tự tạo.
* **Case study sự cố:**
  1. *Case 1:* Dịch vụ lặp lại vòng khởi động rồi bị systemd dừng với thông báo `start request repeated too quickly` (chạm giới hạn start limit); cách đọc nguyên nhân gốc và `systemctl reset-failed`.
  2. *Case 2:* Dịch vụ khởi động lúc boot trước khi mạng sẵn sàng nên lỗi, vì chỉ khai báo `After=network.target` mà không dùng `network-online.target`.

---

### MODULE 10: QUẢN LÝ GÓI & PHẦN MỀM
*Ước lượng: ~3.000 từ*
*🎯 Học xong làm được: cài, giữ phiên bản, gỡ và truy vết gói trên cả họ Debian và họ RHEL, và có chiến lược vá an toàn.*

* **10.1. Khái niệm nền tảng**
  * Gói, phụ thuộc, kho (repository), siêu dữ liệu, chữ ký GPG. Thư viện dùng chung, `ldd`, `ldconfig`.
* **10.2. Debian/Ubuntu**
  * `dpkg` (`-l`, `-L`, `-S`), `apt update`/`upgrade`/`install`/`remove`/`purge`/`autoremove`, `apt-cache policy`, `apt-mark hold`.
  * Kho trong `/etc/apt/sources.list.d/` (định dạng deb822 `.sources` trên bản mới), khóa ký đặt trong `/etc/apt/keyrings` và dùng `signed-by` (`apt-key` đã bị deprecate), PPA, pin phiên bản; `unattended-upgrades`. Trong script nên dùng `apt-get` thay `apt`.
* **10.3. Họ RHEL**
  * `rpm -qa`/`-ql`/`-qf`, `dnf install`/`update`/`remove`/`history`, `dnf history undo`, `versionlock`, kho trong `/etc/yum.repos.d/`, EPEL, giới thiệu AppStream modules.
* **10.4. Alpine và container**
  * `apk add --no-cache`, musl; trong Dockerfile dùng `apt-get install --no-install-recommends` và xóa `/var/lib/apt/lists/*`; ghim phiên bản gói khi cần tái lập.
* **10.5. Biên dịch từ source và công cụ ngoài gói**
  * `./configure && make && make install` vào `/usr/local` hoặc `/opt`; snap/flatpak ở mức khái niệm; tải binary thì xác minh checksum/chữ ký, tránh `curl | sudo bash` một cách mù quáng; công cụ quản lý phiên bản runtime (asdf, mise, nvm, pyenv) ở mức khái niệm.
* **10.6. Cập nhật, kernel và vá bảo mật**
  * Chiến lược vá (staging trước production), khi nào cần reboot, `needrestart` (Debian/Ubuntu), `needs-restarting` (họ RHEL), livepatch, theo dõi CVE (USN, RHSA), rollback, và hướng tiếp cận immutable (thay image mới thay vì sửa tại chỗ).
* **Lab thực hành:** Thêm một kho APT bên thứ ba đúng cách (keyring + `signed-by`), ghim/giữ phiên bản một gói; trên VM họ RHEL dùng `dnf history` và `undo`; tìm file thuộc gói nào bằng `dpkg -S`/`rpm -qf`; biên dịch một công cụ nhỏ từ source vào `/usr/local`.
* **Case study sự cố:**
  1. *Case 1:* `apt upgrade` vô tình nâng phiên bản cơ sở dữ liệu/nginx gây downtime, do không giữ phiên bản và không có cửa sổ bảo trì.
  2. *Case 2:* Đã cập nhật thư viện (như OpenSSL/glibc) nhưng dịch vụ vẫn chạy bản cũ trong bộ nhớ, nên lỗ hổng chưa thực sự được vá; phát hiện bằng `needrestart`/`needs-restarting`.

---

### MODULE 11: NAMESPACES, CGROUPS & NỀN TẢNG CỦA CONTAINER
*Ước lượng: ~5.000 từ*
*🎯 Học xong làm được: giải thích container thực chất là gì, tự dựng một container tối giản bằng lệnh Linux và đọc giới hạn tài nguyên từ phía host.*

* **11.1. Container thực chất là gì**
  * Một tiến trình Linux bình thường được bao bởi namespaces (cô lập "nhìn thấy gì"), cgroups (giới hạn "dùng bao nhiêu"), root filesystem riêng, capabilities và seccomp. Container dùng chung kernel với host, khác với máy ảo. Chuỗi công cụ: Docker → containerd → runc.
* **11.2. Namespaces**
  * Tám loại: mnt, pid, net, uts, ipc, user, cgroup, time. `lsns`, `/proc/<pid>/ns/`, `unshare`, `nsenter`.
  * User namespace và ánh xạ UID (rootless). PID namespace và PID 1 trong container (xem Mục 5.4). Network namespace xem giáo trình Mạng máy tính, Mục 8.1.
* **11.3. cgroups v2**
  * Cây phân cấp thống nhất tại `/sys/fs/cgroup`; các controller: `cpu` (`cpu.weight`, `cpu.max`), `memory` (`memory.max`, `memory.high`, `memory.current`, `memory.events`), `io` (`io.max`, `io.weight`), `pids` (`pids.max`). Công cụ `systemd-cgls`, `systemd-cgtop`, `systemd-run -p`.
  * Phân biệt cgroup v1 và v2; kiểm tra nhanh bằng `stat -fc %T /sys/fs/cgroup` (kết quả `cgroup2fs` nghĩa là v2). Hầu hết distro hiện đại mặc định dùng v2; Kubernetes 1.35 mặc định không cho kubelet khởi động trên node dùng cgroup v1 (`failCgroupV1`).
  * Ánh xạ khái quát của Kubernetes: `requests.cpu` → trọng số CPU, `limits.cpu` → `cpu.max`, `limits.memory` → `memory.max`; các lớp QoS (Guaranteed/Burstable/BestEffort) ảnh hưởng `oom_score_adj` [CẦN XÁC MINH chi tiết theo phiên bản kubelet và runtime].
* **11.4. chroot, pivot_root và mount namespace**
  * Root filesystem của container, mount `/proc`, bind mount, volume.
* **11.5. OverlayFS và image layer**
  * lower/upper/work/merged, copy-up; `mount | grep overlay`; vì sao ghi nhiều vào lớp ghi của container thì chậm và nên dùng volume; dọn dẹp bằng `docker system df` và `docker system prune`.
* **11.6. Capabilities, seccomp và bảo mật runtime**
  * Capabilities mặc định của Docker, `--cap-drop ALL`, nguy hiểm của `--privileged`, hồ sơ seccomp mặc định, AppArmor/SELinux (xem Mục 8.6), rootless container, rootfs chỉ đọc.
* **11.7. Quan sát container từ phía host**
  * `docker top`, `docker stats`, tìm PID trên host (`docker inspect -f '{{.State.Pid}}'`), `nsenter -t <PID> -n`, đọc cgroup của container (`memory.events`, `cpu.stat`), `crictl` trên node Kubernetes.
* **Lab thực hành:** Tự dựng "container" bằng `unshare` kết hợp `chroot` (rootfs lấy từ `docker export` của image Alpine) và cgroup v2 thủ công: tạo cgroup, đặt `memory.max` và `pids.max`, đưa PID vào `cgroup.procs`; thử fork bomb bị `pids.max` chặn và vượt giới hạn bộ nhớ bị OOM kill.
* **Case study sự cố:**
  1. *Case 1:* Pod Kubernetes có độ trễ p99 cao dù mức dùng CPU thấp, do CPU throttling từ `cpu.max`; đọc `nr_throttled` trong `cpu.stat` để xác nhận (xem Mục 7.5).
  2. *Case 2:* Container bị `OOMKilled` (mã thoát 137) dù ứng dụng báo bộ nhớ ổn; đọc `memory.events` và `memory.stat`, lưu ý giới hạn tính cả page cache và bộ nhớ kernel liên quan, và heap của JVM đặt lớn hơn giới hạn.

---

### MODULE 12: TINH CHỈNH KERNEL & QUAN SÁT NÂNG CAO
*Ước lượng: ~3.500 từ*
*🎯 Học xong làm được: tinh chỉnh tham số kernel có kiểm chứng và bền vững, tìm nguyên nhân tiến trình crash bằng core dump và truy vết bằng eBPF ở mức cơ bản.*

* **12.1. `/proc` và `/sys`**
  * Các file hữu ích: `/proc/meminfo`, `/proc/cpuinfo`, `/proc/loadavg`, `/proc/<pid>/...`, `/proc/sys`, `/sys/class`, `/sys/block/<đĩa>/queue/scheduler`.
* **12.2. `sysctl` và lưu cấu hình bền vững**
  * `sysctl -a`, `sysctl -w` (chỉ tạm thời), `/etc/sysctl.d/99-*.conf` kèm `sysctl --system`.
  * Các nhóm tham số: `vm.*` (`swappiness`, `dirty_ratio`, `dirty_background_ratio`, `overcommit_memory`, `max_map_count`), `fs.*` (`file-max`, `inotify.max_user_watches`), `kernel.*` (`pid_max`, `core_pattern`); nhóm `net.*` xem giáo trình Mạng máy tính, Mục 8.5.
  * Quy tắc: đo trước và sau, mỗi lần đổi một tham số, ghi lại lý do.
* **12.3. `ulimit`, `limits.conf` và giới hạn trong systemd**
  * `ulimit -a`, giới hạn do PAM so với `LimitNOFILE=` của systemd (xem Mục 5.6 và 9.2).
* **12.4. Core dump và log kernel**
  * `dmesg -T`, `journalctl -k`, kernel oops/panic, `ulimit -c`, `kernel.core_pattern`, `systemd-coredump` và `coredumpctl`, giới thiệu `kdump`.
* **12.5. Công cụ truy vết**
  * `strace`, `ltrace`, `perf`, `ftrace` (giới thiệu). eBPF: `bpftrace` một dòng lệnh, bộ công cụ BCC (`execsnoop`, `opensnoop`, `biolatency`; trên Debian/Ubuntu tên lệnh thường có hậu tố `-bpfcc`). Yêu cầu quyền và kernel headers; overhead thấp nhưng không bằng 0.
* **12.6. Giám sát liên tục**
  * `sysstat`/`sar` để xem lịch sử, node_exporter kết hợp Prometheus, cảnh báo dựa trên triệu chứng và bão hòa thay vì chỉ ngưỡng đơn lẻ. Hệ sinh thái quan sát mạng xem giáo trình Mạng máy tính, Mục 13.5.
* **Lab thực hành:** Tạo `/etc/sysctl.d/99-lab.conf` đổi `vm.swappiness`, nạp và kiểm chứng, reboot để xác nhận giữ nguyên; bật core dump rồi gây crash một chương trình C nhỏ (SIGSEGV) và đọc bằng `coredumpctl info`; dùng `bpftrace` hoặc `execsnoop` để thấy các tiến trình được tạo ra.
* **Case study sự cố:**
  1. *Case 1:* Elasticsearch/OpenSearch không khởi động với lỗi `max virtual memory areas vm.max_map_count [65530] is too low`; khắc phục bằng `sysctl` và lưu bền vững.
  2. *Case 2:* Tiến trình crash ngẫu nhiên mà không để lại log; bật core dump và dùng `coredumpctl` để xác định lỗi segfault hoặc OOM.

---

### MODULE 13: TỰ ĐỘNG HÓA VẬN HÀNH
*Ước lượng: ~3.000 từ*
*🎯 Học xong làm được: lập lịch công việc đúng cách, khởi tạo máy mới bằng cloud-init và viết một playbook Ansible có tính idempotent.*

* **13.1. cron và `at`**
  * Cú pháp 5 trường, `crontab -e`/`-l`, `/etc/cron.d` (có thêm trường user), `/etc/cron.daily`, môi trường tối giản (PATH, SHELL), xem log (`journalctl` hoặc log cron), `MAILTO`, múi giờ, `@reboot`; dùng `flock` để tránh chạy chồng. So sánh với systemd timers (xem Mục 9.3).
* **13.2. Viết script vận hành bền vững**
  * Idempotent, `--dry-run`, logging, mã thoát có nghĩa, khóa chống chạy chồng, timeout, retry, không in secret. Script nhỏ dùng Bash; logic phức tạp hoặc gọi API thì dùng Python (xem giáo trình Python Scripting).
* **13.3. cloud-init**
  * User-data và `#cloud-config` (`users`, `packages`, `write_files`, `runcmd`), các giai đoạn, log `/var/log/cloud-init.log` và `/var/log/cloud-init-output.log`, `cloud-init status --long`, kiểm tra cú pháp bằng `cloud-init schema`; phần lớn chỉ chạy một lần trên mỗi instance.
* **13.4. Quản lý cấu hình với Ansible (nhập môn)**
  * Inventory, lệnh ad-hoc, playbook, module có tính idempotent, handler, `--check --diff`, role; so sánh với shell script; cơ chế không cần agent qua SSH (liên hệ Mục 8.3).
* **13.5. Hạ tầng bất biến và image**
  * Golden image so với cấu hình lúc boot, giới thiệu Packer, "cattle không phải pets", rollback bằng image, kết hợp với container.
* **Lab thực hành:** Viết script sao lưu chạy bằng cron có `flock`, logging và mã thoát đúng, rồi chuyển sang systemd timer. Viết một `cloud-config` và kiểm tra bằng `cloud-init schema`. Viết một playbook Ansible cài nginx và chạy hai lần (lần hai phải báo `changed=0`).
* **Case study sự cố:**
  1. *Case 1:* Job cron chạy chồng chéo vì lần chạy trước chưa xong, làm đĩa và cơ sở dữ liệu quá tải; khắc phục bằng `flock`.
  2. *Case 2:* User-data chạy lỗi giữa chừng chỉ trên một số máy mới (phụ thuộc mạng hoặc kho gói chưa sẵn sàng) mà không ai phát hiện, vì không kiểm tra `cloud-init status`.

---

### MODULE 14: PHỤ LỤC MỞ RỘNG (ẢO HÓA, KERNEL NÂNG CAO & HỆ ĐIỀU HÀNH KHÁC)
*Ước lượng: ~2.500 từ*

* **14.1. [Mở rộng] Ảo hóa**
  * Hypervisor loại 1 và loại 2, KVM/QEMU, virtio, vCPU và steal time, instance dạng burstable (CPU credit), NUMA trong cloud, khái niệm live migration; so sánh container, máy ảo và microVM (như Firecracker).
* **14.2. [Mở rộng] Một số chủ đề kernel nâng cao**
  * io_uring (I/O bất đồng bộ), eBPF CO-RE, vá nóng kernel (livepatch/kpatch) ở mức khái niệm.
* **14.3. [Mở rộng] Windows và macOS dưới góc nhìn DevOps**
  * Windows: dịch vụ, Task Scheduler, PowerShell, WSL2 (máy ảo nhẹ chạy kernel Linux thật). macOS: userland dựa trên BSD và `launchd`; các khác biệt công cụ hay gây lỗi khi viết script chạy cả hai nơi (ví dụ `sed -i` yêu cầu đối số khác nhau giữa GNU và BSD).

---

## 📊 TỔNG KẾT QUY MÔ GIÁO TRÌNH (ĐẾM THỰC TẾ)

* **Tổng số module:** 15 module (Module 0 → Module 14).
* **Tổng số bài Lab thực hành:** 14 bài lab (Module 0 → Module 13; Module 14 là phụ lục mở rộng không có lab).
* **Tổng số Case Study sự cố production:** 28 kịch bản (Module 0 → Module 13, mỗi module 2 case; Module 14 không có case).
* **Tổng số từ dự kiến toàn giáo trình:** ~57.500 từ (bằng tổng ước lượng của 15 module).
* **Tài liệu bàn giao sau khi hoàn thành toàn bộ module:**
  1. Bảng thuật ngữ chuyên ngành Anh – Việt.
  2. Cheat Sheet lệnh tổng hợp dành cho SRE on-call.
  3. Bộ 20 câu hỏi phỏng vấn DevOps/SRE mức Junior–Mid có lời giải chi tiết.
  4. Lộ trình ôn tập 4 tuần có phân bổ thời gian cụ thể.

---

## 📚 TÀI LIỆU THAM KHẢO CHÍNH THỨC

* Linux man pages: https://man7.org/linux/man-pages/
* Tài liệu kernel: https://docs.kernel.org/
* Tài liệu systemd: https://www.freedesktop.org/software/systemd/man/
* Tài liệu Ubuntu Server và ghi chú phát hành: https://documentation.ubuntu.com/ và https://discourse.ubuntu.com/
* Tài liệu Kubernetes (cgroup, QoS, quản lý tài nguyên): https://kubernetes.io/docs/
* Phương pháp USE và checklist 60 giây của Brendan Gregg: https://www.brendangregg.com/
