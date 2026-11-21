# Angel Audio

Turn Android phones into speakers for your computer. Use **one phone** as a plain speaker, or up to **7 phones** as a surround-sound system. Volume goes up to 200%.

> Status: early version. Not yet tested on real devices, so please report problems under Issues.

## 1. Put it on GitHub and get the app

1. Create a free account at github.com and press **New repository** (name it `angel-audio`).
2. Upload everything from this folder. Easiest way: on the new repo page press **uploading an existing file**, drag the *contents* of the unzipped folder in (including the hidden `.github` folder), then press **Commit changes**.
   Or with git:
   ```
   git init
   git add .
   git commit -m "Angel Audio"
   git branch -M main
   git remote add origin https://github.com/YOUR-NAME/angel-audio.git
   git push -u origin main
   ```
3. Open the **Actions** tab. A run called *Build Android app* starts by itself (about 5 minutes). If it does not, choose it and press **Run workflow**.
4. When it shows a green tick, open the run and download **AngelAudio-apk** at the bottom. Unzip it to get `AngelAudio.apk`.
5. Optional: to publish a download page, create a tag such as `v1.0` (Releases → Draft a new release). The APK is attached automatically.

If the build fails, open the red run, copy the error text and open an Issue (or paste it to Claude).

## 2. Install on your phone

1. Copy `AngelAudio.apk` to the phone and open it.
2. Allow "Install unknown apps" when asked.
3. Open **Angel Audio** and allow notifications (this keeps it playing with the screen off).

## 3. Use it with ONE phone (simplest)

1. Open the app and switch on **This phone is plugged into my computer**.
2. Leave the position on **Solo (everything)**, then tap **Start**.
3. Plug the phone into the computer with a USB cable. Turn on **USB tethering** (the app has a button that opens that setting).
4. On the computer open a web browser and type the address the app shows, for example `http://192.168.42.129:8080`.
5. Press **Download Windows installer** and open it. If Windows warns you, choose *More info → Run anyway*. It installs everything and puts an **Angel Audio** shortcut on your desktop. If it asks you to open the file a second time, do so.
6. Play anything on the computer. The phone is now its speaker. Next time, just plug in, start the app, and double-click the **Angel Audio** desktop shortcut.

Tip: mute the computer's own speakers if you only want the phone to play.

## 4. Add more phones (surround sound)

Other phones find the main phone by themselves, like file-sharing apps do.

**Easiest: scan a code**
1. On the main phone, scroll to **Add other phones**. A QR code is shown there.
2. On each other phone open the app, tap **Extra speaker**, then **Scan the main phone's code**.
3. That is all. The phone connects (Wi-Fi if you share a network, Bluetooth if not) and starts playing.

**Or let them find each other**
- *Wi-Fi:* put the phones on the same Wi-Fi as the main phone, choose **Extra speaker** and tap **Start**. The main phone's name appears on the extra phone and the extra phone appears under **Phones nearby** on the main phone.
- *Bluetooth:* on the main phone tap **Make visible to Bluetooth phones**. On the extra phone choose **Bluetooth**, tap **Search for nearby phones**, tap the main phone's name, then **Start**. No pairing needed.

**Placing the speakers**
- New phones are placed automatically (Front Left, Front Right, Center, and so on).
- On the main phone, **Phones nearby** lists every phone. Use the drop-down to move one to another position, and tap **Beep** to hear which phone is which.
- Set the main phone's own position (for example Front Left) once your other phones have joined.
- If one phone sounds early or late, use its **Sync nudge** slider.

Bluetooth notes:
- Each Bluetooth phone gets about 12 KB/s of compressed 24 kHz audio, a little less crisp than Wi-Fi.
- While a Bluetooth phone is connected, all phones add about 0.2 s of delay so they stay in sync. Fine for music; for video, use your player's audio delay setting.
- Bluetooth shares one radio between all phones. 2 to 3 is comfortable, 7 may stutter. You can mix Wi-Fi and Bluetooth phones.
- The scanner uses Google Play Services. If a phone does not have it, use the search lists instead.

## Find a lost phone

When an extra phone joins, it is asked once: *"Find this phone if it gets lost?"* If you tap **Share**, the main phone can then:

- see the phone's **last known position** and battery level, and open it in your maps app (**Show on map**),
- make it **ring loudly** (**Ring it**), even when it is on silent. If it is out of reach, **Ring when found** rings it as soon as it reconnects,
- keep the last position even after the phone disconnects, so you know where to start looking.

How it stays fair and visible:
- It is off until the phone's owner agrees, and the owner can switch it off any time under **Find my phone** on that phone.
- While sharing, the phone shows a permanent notification saying so, and a ringing phone shows a **Stop ringing** button.
- It shares only location, battery level and phone name, only with the main phone it joined, and stops when you tap **Stop**.
- Allow location when Android asks. Choose "While using the app"; the running notification keeps it working with the screen off.

Limits: it only works while the phone is on and in range (same Wi-Fi or Bluetooth). It is not a replacement for Google Find Hub (Android) or Find My (iPhone), which can find a phone anywhere. Keep those switched on too.

## Volume above 100%

The slider goes to 200%. It is a software boost with a soft limiter. Small phone speakers will sound harsher and can be damaged at the top end, so keep the phones away from your ears.

## Without a USB cable (same Wi-Fi only)

You can skip the cable: put the computer and phones on the same Wi-Fi, leave the hub switch off on every phone, tap Start, and run on the computer:
```
pip install soundcard "numpy<2"
python pc_sender/angel_audio_sender.py
```
Allow Python through the Windows firewall when asked.

## Troubleshooting

If something goes wrong, scroll to the bottom of the app and tap **Copy diagnostics**, then paste the text into your message. If the app ever closes by itself, a card at the top offers **Copy details** the next time you open it.

If sound stops when the screen turns off, tap **Allow** on the "Keep it playing with the screen off" card.

| Problem | Fix |
|---|---|
| Computer page does not open | Check USB tethering is on and the app shows *Waiting for your computer*. Try each address the app lists. |
| "Cannot reach the phone" in the PC window | Start the app on the phone first, then run the shortcut. |
| No sound | Tap *Play test sound*. Check the phone volume and that the computer is actually playing something. |
| A phone is out of sync | Move its timing slider a little. Use Wi-Fi 5 GHz and keep phones near the router. |
| Status says *Waiting for your computer* while the computer is silent | Normal. Windows sends no audio during silence. It resumes when sound plays. |
| Orange warning under Status | A part had a problem and restarts itself. If it keeps counting up, tap Stop then Start. |
| Bluetooth phone will not connect | Make sure the main phone has tapped Start first, both phones have Bluetooth on, and the Bluetooth permission was allowed. |
| Scanning does nothing | Needs Google Play Services. Use Wi-Fi or Bluetooth search instead. |
| Phone does not show up under Phones nearby | Tap Start on both phones. On Wi-Fi they must share a network; some public or guest Wi-Fi blocks phones from seeing each other, so use the QR code or Bluetooth. |
| Ring or location does not work | The lost phone needs Angel Audio running (Start tapped) and location allowed. Check the Find my phone switch on that phone. |
| Choppy sound | Too many phones on a weak Wi-Fi. Move closer or use a hotspot from the hub phone. |
| Mac | Needs a loopback driver such as BlackHole, then run `python3 pc_sender/angel_audio_sender.py <phone-ip>`. |
| TV | A TV cannot run the helper. Connect a computer to the TV and use that computer. |

## What keeps it steady

- Every part of the app restarts itself if it hits a problem, waiting a little longer each time.
- The phone keeps its CPU and Wi-Fi awake while playing, so the screen can be off.
- The computer program finds the phone again if its address changes, and restarts audio capture if Windows resets it.
- The app never restarts itself after a crash, so it cannot get stuck in a loop.

## How it works

The computer captures its audio output and sends 10 ms packets. The main phone keeps the clock, plays its own channel and relays the others to the other phones over Wi-Fi or Bluetooth. Every phone plays about 150 ms after capture, so they line up.

## Developing

Tests for the computer program and the audio codec live in `tests/` and run automatically on GitHub before each build. Run them yourself with `pip install "numpy<2"` then `python tests/test_sender.py` and `python tests/test_adpcm.py`.


Open the folder in Android Studio and run. Needs JDK 17. Android 8.0 or newer.
The PC helper is `pc_sender/angel_audio_sender.py` (a copy lives in `app/src/main/assets` and is served by the phone).

## License

MIT
