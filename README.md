# Torrent To Google Drive Downloader

Download torrents directly to your Google Drive using Google Colab and libtorrent.

---

## 🚀 Features

- Download via `.torrent` file or magnet link
- Save files directly to Google Drive
- Real-time progress bars with interactive widgets
- Maximize disk space by switching to GPU runtime

---

## 🛠️ Setup

1. **Open in Google Colab**
2. **Change Runtime:**  
   Go to `Runtime → Change runtime type → Hardware accelerator: GPU`  
   (Gives ~384GB disk space)
3. **Install dependencies:**
   ```
   !python -m pip install --upgrade pip setuptools wheel
   !python -m pip install lbry-libtorrent
   !python -m pip install --upgrade libtorrent
   ```
4. **Mount Google Drive:**
   ```python
   from google.colab import drive
   drive.mount("/content/drive")
   ```

---

## 📥 Download Torrents

### Add From Torrent File

Upload a `.torrent` file and start downloading:

```python
from google.colab import files
source = files.upload()
params = {
    "save_path": "/content/drive/My Drive/Torrent",
    "ti": lt.torrent_info(list(source.keys())[0]),
}
downloads.append(ses.add_torrent(params))
```

### Add From Magnet Link

Interactively add magnet links:

```python
params = {"save_path": "/content/drive/My Drive/Torrent"}
while True:
    magnet_link = input("Enter Magnet Link Or Type Exit: ")
    if magnet_link.lower() == "exit":
        break
    downloads.append(
        lt.add_magnet_uri(ses, magnet_link, params)
    )
```

---

## 📊 Monitor Progress

Real-time download status with progress bars using `ipywidgets`.

---

## 💡 Tips & Troubleshooting

- For more disk space, always use GPU runtime.
- If widgets do not close properly, see [Colab issue #726](https://github.com/googlecolab/colabtools/issues/726#issue-486731758).
- References:
  - [StackOverflow: Downloading torrents in Python](https://stackoverflow.com/a/5494823/7957705)
  - [GitHub Issue #3](https://github.com/FKLC/Torrent-To-Google-Drive-Downloader/issues/3)

---

## 📄 License

MIT License

---

## 🙏 Credits

- Based on solutions from StackOverflow and GitHub community.

---

## Example Screenshot

_(Add a screenshot of the notebook running in Colab with progress bars, if desired)_
