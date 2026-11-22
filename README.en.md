# Minolog (ミノログ)

[日本語](README.md) | English

Minolog is a Windows tool that turns a recording (mp4) of a Puyo Puyo Tetris 2 versus match into a move-by-move Tetris record: which piece was placed, where, in which rotation, whether HOLD was used, which lines were cleared, and what garbage arrived.

**This is an alpha release.** It is free to use. It is an unofficial tool made by an individual, and is not affiliated with SEGA, The Tetris Company, or Tetris Holding.

The program's screens, file names, and reports are in Japanese. This page explains what to click.

## Download

Get the newest `minolog_v….zip` from [Releases](../../releases).

## What it does

1. Splits the recording into frames and reads the moves from the screen.
2. For moves it could not read, solves them again from the surrounding frames and fills them in.
3. Fixes missed HOLD swaps.
4. Writes the record (JSON) and an HTML report where you can step through the board one move at a time. The report also marks "mistake" candidates by comparing each move with the choice of a strong Tetris AI (Cold Clear). Treat these as a reference only.

On 9 recordings (49,973 moves in total), 99.5% of the moves (49,738) ended up in the record. Moves that could not be read are left empty rather than guessed. Of the moves that were filled in at step 2, roughly 1 in 100 may be wrong.

## Recordings that work

- The PC version of Puyo Puyo Tetris 2, recorded in 1920x1080 fullscreen.
- A versus match. At the start you choose which board to read: left (1P), right (2P), or both. The board you read must be a Tetris board.
- Very fast play (close to 2 pieces per second) or very slow piece movement may not be read.

## How to use

1. Extract the zip (right-click → "Extract All").
2. Once, the first time: double-click `セットアップ.bat` (setup). If .NET 9 or Python is missing, it asks whether to install them. Answer `y` to install.
3. Drag and drop your recording onto `ミノログ.bat`.
4. Choose the board by number: `1` = 1P, `2` = 2P, `3` = both. Pressing Enter alone means 1P.
5. When it finishes, `入口.html` (the entry page) opens in your browser.

Time, for one side: about 10 minutes for a 5-minute recording, and 2–3 hours for a 25-minute recording. A single long game takes longer; a 37-minute recording that contained long games took about 10 hours. Choosing both boards takes less than twice as long, because recovery for 1P and the main analysis for 2P run at the same time. While it runs it needs free disk space of about 4.5 times the size of the recording. When it finishes, the result is a few tens of MB.

Results are written to `結果\<recording name>\1P\` (or `2P\`). The record itself is in `回収\棋譜_回収込み\区間\` as `kifu.json` and `kifu.chunkN.json`.

## Requirements

- Windows 10 / 11 (64-bit)
- .NET 9 Desktop Runtime and Python 3.10 or later (setup checks for both)

It has not been tested much on PCs other than the author's. If setup stops, please tell us in Issues.

## Reporting a problem

Open an [Issue](../../issues), describe what you did and what happened, and attach `版.txt` (the version file inside the zip) and `記録_ミノログ.txt` (the log in the result folder). English is fine.

From 0.1.12, the zip contains `診断を作る.bat`. Double-clicking it makes a diagnostic file (`minolog_diag_….zip`) that is easier for us to work with: it holds the version, facts about the PC, and the logs, with your user name, folder locations, and the recording's name replaced by placeholders. It does not contain the recording or the record. Attach that instead if you have it.

## Terms and licenses

Please read `利用条件.txt` (terms of use, in Japanese) inside the zip. In short: free to use, including for streams and videos; no warranty; unofficial; please share Minolog by linking to this page rather than re-hosting or modifying the zip.

Licenses of third-party components (OpenCV, OpenCvSharp, FFmpeg, Cold Clear) are in the `ライセンス` folder inside the zip.

"Puyo Puyo" is a trademark of SEGA. "Tetris" is a trademark of Tetris Holding.
