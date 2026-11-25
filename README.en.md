# Minolog (ミノログ)

[日本語](README.md) | English

Minolog is a Windows tool that turns a recording (mp4) of a Puyo Puyo Tetris 2 versus match into a move-by-move Tetris record: which piece was placed, where, in which rotation, whether HOLD was used, which lines were cleared, and what garbage arrived.

**This is a beta release.** It is free to use. It is an unofficial tool made by an individual, and is not affiliated with SEGA, The Tetris Company, or Tetris Holding.

The program's screens, file names, and most reports are in Japanese. From 0.1.16, the start page, the statistics and the mistake summary also come in English (`入口.en.html` and so on), and `Minolog (English).bat` opens the English start page when it finishes. This page explains what to click.

## Download

Get the newest `minolog_v….zip` from [Releases](../../releases).

If you would rather not install .NET or Python, download the bundled build `minolog_v…_portable.zip` from the same page instead (about 177 MB, from 0.1.17; .NET 10 and Python are inside, no setup needed).

## What it does

1. Splits the recording into frames and reads the moves from the screen.
2. For moves it could not read, solves them again from the surrounding frames and fills them in.
3. Fixes missed HOLD swaps.
4. Writes the record (JSON) and an HTML report where you can step through the board one move at a time. The report also marks "mistake" candidates by comparing each move with the choice of a strong Tetris AI (Cold Clear). Treat these as a reference only.

On 7 recordings (9 boards, counting the left and right sides separately; 49,973 moves in total), 99.5% of the moves (49,738) ended up in the record. Moves that could not be read are left empty rather than guessed. Of the moves that were filled in at step 2, roughly 1 in 100 may be wrong. Moves read from the screen in step 1 can also be wrong (on one recording, 9 of 263 checked moves; mostly missed HOLD swaps, counted before step 3 corrects HOLD).

## What it cannot do, and what has not been tested

- It cannot read Puyo Puyo boards. Recordings that are not versus matches (40 lines and other solo modes) have not been tested.
- Low-quality recordings mix in wrong moves, which cannot be told apart inside the record. Use the original 1920x1080 recording.
- Moves in places where the recording itself skipped (this happens when the PC is busy while recording) cannot be brought back.
- "Mistakes" are a reference only. It does not look at the opponent's attack or the flow of the match.
- It has not yet been run end to end on any PC other than the author's (one Windows 11 PC). Windows 10, accounts that are not administrators, folders under OneDrive, and PCs without internet have not been tested.
- See "KNOWN LIMITS AND WHAT HAS NOT BEEN TESTED" and "QUESTIONS" in `README_en.txt` inside the zip for details.

## Recordings that work

- The PC version of Puyo Puyo Tetris 2, recorded in 1920x1080 fullscreen (the author's recordings are 60 fps, about 13 Mbps; 10 Mbps or more is recommended).
- A versus match. At the start you choose which board to read: left (1P), right (2P), or both. The board you read must be a Tetris board.
- Very fast play or very slow piece movement may not be read (the fastest recordings read so far were about 2.4 pieces per second).

## How to use

1. Extract the zip (right-click → "Extract All"). Do not open it from inside the zip: it cannot find its other files and stops, or the results may be written to a temporary place. If you downloaded the zip with a browser, right-click the zip before extracting it, choose Properties, tick "Unblock" at the bottom and press OK. This avoids most "Windows protected your PC" warnings when opening the .bat files and exes. If the warning appears, click "More info", then "Run anyway" (Minolog is not code-signed).
2. Double-click `ミノログ.exe` (the program with a window, from 0.1.15). The first time, press the button "最初の準備をする(1回だけ)" (first-time setup). If .NET or Python is missing, it asks whether to install them.
3. Drop your recording onto the window, choose the board (1P, 2P or both) and press "棋譜にする" (make the record).
4. When it finishes, `入口.html` (the entry page) opens in your browser.

Without the window: once, the first time, double-click `セットアップ.bat` (setup; answer `y` to install what is missing). Then drag and drop your recording onto `ミノログ.bat` and choose the board by number: `1` = 1P, `2` = 2P, `3` = both. Pressing Enter alone means 1P.

Time, for one side: about 10 minutes for a 5-minute recording, and 2–3 hours for a 25-minute recording. A single long game takes longer; a 37-minute recording that contained long games took about 10 hours. Choosing both boards takes less than twice as long, because recovery for 1P and the main analysis for 2P run at the same time. While it runs it needs free disk space of about 4.5 times the size of the recording. When it finishes, the result is a few tens of MB.

Results are written to `結果\<recording name>\1P\` (or `2P\`). The record itself is in `回収\棋譜_回収込み\区間\` as `kifu.json` and `kifu.chunkN.json`.

## Requirements

- Windows 10 / 11 (64-bit)
- .NET 9 or later Desktop Runtime and Python 3.11 or later (setup checks for both; from 0.2.0 it installs .NET 10 when .NET is missing)
- Setup needs the internet. On a PC without it, use the bundled build `minolog_v…_portable.zip`
- It does not need to run as administrator (whether Windows asks for permission when setup installs .NET or Python has not been tested)

It has not been tested much on PCs other than the author's. If setup stops, please tell us in Issues.

## Reporting a problem

Open an [Issue](../../issues), describe what you did and what happened, and attach `版.txt` (the version file inside the zip) and `記録_ミノログ.txt` (the log in the result folder). English is fine.

From 0.1.12, the zip contains `診断を作る.bat`. Double-clicking it makes a diagnostic file (`minolog_diag_….zip`) that is easier for us to work with: it holds the version, facts about the PC, and the logs, with your user name, folder locations, and the recording's name replaced by placeholders. It does not contain the recording or the record. Attach that instead if you have it.

## Terms and licenses

Please read `利用条件.txt` (terms of use, in Japanese) inside the zip. In short: free to use, including for streams and videos; no warranty; unofficial; please share Minolog by linking to this page rather than re-hosting or modifying the zip.

Licenses of third-party components (OpenCV, OpenCvSharp, FFmpeg, Cold Clear) are in the `ライセンス` folder inside the zip.

"Puyo Puyo" is a trademark of SEGA. "Tetris" is a trademark of Tetris Holding.
