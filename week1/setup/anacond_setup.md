# Panduan Instalasi & Penggunaan Anaconda

Dokumen ini memandu kamu dari nol hingga memiliki environment Python yang siap digunakan untuk proyek TL Vision Amarine.

---

## 1. Instalasi Anaconda

### Windows

1. Download installer di [https://www.anaconda.com/download](https://www.anaconda.com/download)
2. Pilih versi **Python 3.10** atau lebih baru (64-bit)
3. Jalankan file `.exe` yang sudah diunduh
4. Ikuti wizard instalasi:
   -  Centang **"Add Anaconda to my PATH environment variable"** *(opsional, tapi memudahkan)*
   - Centang **"Register Anaconda as my default Python"**
5. Klik **Install** dan tunggu hingga selesai

### macOS

```bash
# Gunakan Homebrew (direkomendasikan)
brew install --cask anaconda

# Tambahkan ke PATH (tambahkan ke ~/.zshrc atau ~/.bash_profile)
export PATH="/usr/local/anaconda3/bin:$PATH"

# Reload shell
source ~/.zshrc
```

### Linux (Ubuntu/Debian)

```bash
# Download installer
wget https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh

# Jalankan installer
bash Anaconda3-2024.02-1-Linux-x86_64.sh

# Ikuti instruksi, ketik 'yes' saat diminta
# Setelah selesai, reload shell
source ~/.bashrc
```

---

## 2. Verifikasi Instalasi

Buka **Terminal** (macOS/Linux) atau **Anaconda Prompt** (Windows), lalu jalankan:

```bash
conda --version
# Output yang diharapkan: conda 24.x.x atau lebih baru

python --version
# Output yang diharapkan: Python 3.10.x atau lebih baru
```

---

##  3. Membuat Environment Baru

Environment adalah "ruang kerja" terisolasi yang memiliki versi Python dan library sendiri. Ini mencegah konflik antar proyek.

```bash
# Buat environment bernama 'amarine' dengan Python 3.10 {environment bisa diganti dengan yang diinginkan}
conda create -n amarine python=3.10

# Tunggu proses selesai, lalu ketik 'y' saat diminta konfirmasi
```

---

##  4. Mengaktifkan & Menonaktifkan Environment

```bash
# Mengaktifkan environment
conda activate amarine

# Kamu akan melihat (amarine) di awal baris terminal:
# (amarine) username@computer:~$

# Menonaktifkan environment (kembali ke base)
conda deactivate
```

---

## 5. Menginstal Library yang Dibutuhkan

Pastikan environment `amarine` sudah aktif sebelum menginstal:

```bash
# Pastikan environment aktif
conda activate amarine

# Install NumPy
conda install numpy

# Install OpenCV (via pip karena tidak tersedia di channel default conda)
pip install opencv-python

# Install library tambahan yang berguna
conda install matplotlib pillow

# Install sekaligus (cara lebih efisien)
conda install numpy matplotlib pillow
pip install opencv-python
```

---

## 6. Perintah Conda yang Sering Digunakan

```bash
# Melihat daftar semua environment yang ada
conda env list

# Melihat semua library yang terinstal di environment aktif
conda list

# Mencari library tertentu
conda search numpy

# Update library tertentu
conda update numpy

# Update semua library
conda update --all

# Menghapus library
conda remove numpy

# Menghapus environment (hati-hati!)
conda env remove -n nama_environment
```

---

##  7. Export & Import Environment

Fitur ini berguna untuk berbagi environment dengan tim atau ketika pindah komputer.

```bash
# Export environment aktif ke file YAML
conda env export > environment.yml

# Membuat environment dari file YAML (digunakan orang lain)
conda env create -f environment.yml

# Aktifkan environment yang baru dibuat
conda activate amarine
```

Contoh isi file `environment.yml`:

```yaml
name: amarine
channels:
  - defaults
  - conda-forge
dependencies:
  - python=3.10
  - numpy=1.24.3
  - matplotlib=3.7.1
  - pillow=9.4.0
  - pip:
    - opencv-python==4.8.0.76
```

---

## 8. Troubleshooting Umum

### Conda tidak dikenali setelah instalasi (Windows)
```bash
# Buka Anaconda Prompt, bukan Command Prompt biasa
# Atau tambahkan Conda ke PATH secara manual
```

### Error saat install OpenCV
```bash
# Coba uninstall dulu lalu install ulang
pip uninstall opencv-python
pip install opencv-python --upgrade
```

### Environment tidak muncul di Jupyter
```bash
# Install ipykernel di environment amarine
conda activate amarine
pip install ipykernel
python -m ipykernel install --user --name=amarine --display-name="Python (amarine)"
```

### Conda sangat lambat saat resolve dependencies
```bash
# Install dan gunakan mamba sebagai alternatif yang lebih cepat
conda install -n base conda-libmamba-solver
conda config --set solver libmamba
```

---
