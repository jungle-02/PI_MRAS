# PI_MRAS

PI_MRAS là repository phục vụ bài toán điều khiển động cơ DC với bộ điều khiển PI và PI-MRAS, bao gồm firmware nhúng trên STM32, giao diện giám sát/điều khiển trên Windows và các artifact từ mô hình Simulink.

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Tính năng chính](#tính-năng-chính)
- [Cấu trúc repository](#cấu-trúc-repository)
- [Yêu cầu môi trường](#yêu-cầu-môi-trường)
- [Cài đặt và sử dụng](#cài-đặt-và-sử-dụng)
- [Kết nối phần cứng](#kết-nối-phần-cứng)

## Giới thiệu

Dự án tập trung vào:

- Điều khiển tốc độ động cơ bằng firmware STM32.
- Truyền thông UART giữa vi điều khiển và ứng dụng GUI.
- Theo dõi tín hiệu đáp ứng và tín hiệu điều khiển theo thời gian thực.

## Tính năng chính

- Hỗ trợ lựa chọn bộ điều khiển PI hoặc PI-MRAS.
- Hỗ trợ nhiều dạng tín hiệu vào (Setpoint, Sine, Pulse).
- Giao diện GUI hiển thị đồ thị tín hiệu vận hành theo thời gian thực.
- Có sẵn mô hình/nguồn sinh tự động từ Simulink cho firmware.

## Cấu trúc repository

```text
PI_MRAS/
├── Keil_C_motorcontrol/     # Firmware STM32 + project Keil/MDK-ARM + model liên quan
├── Motor_control_GUI_3/     # Ứng dụng GUI Windows Forms (C#)
├── slprj/                   # Thư mục sinh tự động từ Simulink
└── REPORT EXTEND MODULE - PIMRAS.pdf
```

## Yêu cầu môi trường

- **Firmware**:
  - Keil MDK-ARM (hoặc IDE tương thích dự án STM32)
  - Bộ thư viện STM32 HAL/CMSIS (đã đi kèm trong project)
- **GUI**:
  - Windows
  - Visual Studio (hỗ trợ .NET Framework cho Windows Forms)
  - Cổng COM để giao tiếp UART
- **Mô hình** (nếu chỉnh sửa/sinh lại code):
  - MATLAB/Simulink

## Cài đặt và sử dụng

### 1) Firmware STM32

1. Mở project trong `/home/runner/work/PI_MRAS/PI_MRAS/Keil_C_motorcontrol/New_control/MDK-ARM/`.
2. Build và nạp firmware vào board STM32.
3. Đảm bảo thông số UART trên thiết bị khớp với GUI trước khi chạy.

### 2) Ứng dụng GUI

1. Mở solution `/home/runner/work/PI_MRAS/PI_MRAS/Motor_control_GUI_3/Motor_control.sln`.
2. Build và chạy project `Motor_control`.
3. Chọn đúng cổng COM và kết nối với thiết bị.
4. Thiết lập tham số điều khiển, gửi cấu hình và theo dõi đồ thị.

### 3) Mô hình Simulink (tùy chọn)

- Mô hình `.slx` nằm trong thư mục firmware và có thể dùng để tham chiếu/chỉnh sửa thuật toán trước khi sinh mã lại.

## Kết nối phần cứng

- PA0 → EN (PWM output)
- PA10 → Xung A encoder
- PA1 → IN1
- PB7 → TX USB UART
- PB6 → RX USB UART
- GND nối chung
