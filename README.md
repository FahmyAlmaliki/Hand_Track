# Hand Tracking with Arduino Control


Proyek ini mengimplementasikan sistem hand tracking real-time menggunakan MediaPipe dan OpenCV yang dapat mengontrol servo motor melalui Arduino untuk membuat robotic hand yang meniru gerakan tangan manusia.

## Features

- **Real-time Hand Detection**: Menggunakan MediaPipe untuk mendeteksi dan melacak tangan secara real-time
- **Finger Recognition**: Mendeteksi status jari (terbuka/tertutup) untuk setiap jari
- **Hand Type Detection**: Membedakan tangan kiri dan kanan
- **Arduino Serial Communication**: Mengirim data ke Arduino untuk mengontrol servo motor
- **Interactive Controls**: Kontrol keyboard untuk berbagai fitur
- **Visual Feedback**: Tampilan real-time dengan informasi tracking

## Hardware Requirements

- **Computer**: Dengan webcam untuk capture video
- **Arduino**: Arduino Uno/Nano atau compatible board
- **Servo Motors**: 5 servo motor (untuk 5 jari) + 1 optional (untuk pergelangan tangan)
- **Power Supply**: External power untuk servo motor (5V, minimal 2A)
- **Kabel**: Kabel USB untuk koneksi Arduino dan kabel jumper

## Software Requirements

### Python Dependencies
```bash
pip install opencv-python
pip install mediapipe
pip install numpy
pip install pyserial
```

### Arduino Libraries
- Servo library (biasanya sudah include di Arduino IDE)

## Project Structure

```
Hand_Track/
├── hand_track_with_arduino_serial.py  # Main program dengan Arduino control
├── hand_track.py                      # Hand tracking tanpa Arduino
├── arduino_serial_hand_track.ino      # Arduino code untuk servo control
├── arduino_hand_track.ino             # Alternative Arduino code
├── README.md                          # Dokumentasi proyek
└── LICENSE                            # License file
```

## Setup Instructions

### 1. Hardware Setup

#### Arduino Wiring:
- Servo 1 (Thumb): Pin 3
- Servo 2 (Index): Pin 5  
- Servo 3 (Middle): Pin 6
- Servo 4 (Ring): Pin 9
- Servo 5 (Pinky): Pin 10

**Catatan**: Gunakan external power supply untuk servo motor. Jangan power servo dari pin 5V Arduino untuk menghindari kerusakan.

### 2. Software Setup

1. **Upload Arduino Code**:
   - Buka `arduino_serial_hand_track.ino` di Arduino IDE
   - Sesuaikan pin servo jika diperlukan
   - Upload ke Arduino board

2. **Install Python Dependencies**:
   ```bash
   pip install opencv-python mediapipe numpy pyserial
   ```

3. **Configure Serial Port**:
   - Buka `hand_track_with_arduino_serial.py`
   - Ubah `ARDUINO_PORT = 'COM9'` sesuai port Arduino Anda
   - Di Windows: biasanya COM3, COM4, dll.
   - Di Linux/Mac: biasanya /dev/ttyUSB0, /dev/ttyACM0, dll.

## Usage

### Running the Main Program

```bash
python hand_track_with_arduino_serial.py
```

### Controls

| Key | Function |
|-----|----------|
| `q` | Quit program |
| `c` | Toggle finger counting display |
| `d` | Toggle distance measurement between thumb and index finger |
| `p` | Pause/resume Arduino communication |

### Program Features

1. **Hand Detection**: Program akan mendeteksi tangan yang paling dekat dengan kamera
2. **Finger Status**: Menampilkan status setiap jari (OPEN/CLOSE)
3. **Hand Type**: Menampilkan jenis tangan (Left/Right)
4. **Finger Count**: Menampilkan jumlah jari yang terbuka
5. **Arduino Control**: Mengirim data ke Arduino untuk menggerakkan servo

## Data Communication Protocol

Program mengirim data ke Arduino dalam format:
```
<thumb,index,middle,ring,pinky,wrist>
```

Dimana setiap nilai adalah:
- `0`: Jari tertutup (servo ke posisi 0°)
- `1`: Jari terbuka (servo ke posisi 180°)

Contoh: `<1,1,0,0,0,180>` = thumb dan index terbuka, sisanya tertutup, tangan kanan

## Troubleshooting

### Arduino Connection Issues
- Pastikan port COM benar
- Pastikan Arduino tidak digunakan program lain
- Restart Arduino dan program Python

### Hand Detection Issues
- Pastikan pencahayaan cukup
- Posisikan tangan dalam frame kamera
- Hindari background yang kompleks
- Jaga jarak optimal dengan kamera (30-100cm)

### Servo Issues
- Pastikan power supply cukup untuk semua servo
- Periksa wiring servo ke pin Arduino
- Pastikan servo tidak macet atau rusak

## Code Structure

### HandTracker Class Methods

- `find_hands()`: Deteksi tangan dalam gambar
- `find_position()`: Mendapatkan posisi landmark tangan
- `get_hand_type()`: Menentukan jenis tangan (kiri/kanan)
- `fingers_up()`: Mendeteksi status jari (terbuka/tertutup)
- `calculate_finger_open_close_binary()`: Mengkonversi status jari ke binary
- `find_distance()`: Menghitung jarak antar landmark

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

- **FahmyAlmaliki** - *Initial work*

## Acknowledgments

- MediaPipe team untuk hand tracking solution
- OpenCV community
- Arduino community untuk servo control examples
