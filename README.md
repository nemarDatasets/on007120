[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on007120-blue)](https://doi.org/10.82901/nemar.on007120)

This dataset contains intracranial EEG data recorded during non-REM sleep and used in Hatano et al. (in press).

Authors: 
Keisuke Hatano, Naoto Kuroda, Hiroshi Uda, Kazuki Sakakura, Michael J. Cools, Aimee F. Luat, Shin-Ichiro Osawa, Hitoshi Nemoto, Kazushi Ukishiro, Hidenori Endo, Nobukazu Nakasato, Yutaro Takayama, Keiya Iijima, Masaki Iwasaki, Eishi Asano

Funding: 
National Institutes of Health (NIH; NS064033 to E.A.); 
Uehara Memorial Foundation Postdoctoral Fellowship (202441017 to K.H.; 20210301 to H.U.);
Japan Society for the Promotion of Science (JP22J23281, JP22KJ0323, and 202560576 to N.K.; 202560628 to H.U.; JP19K09494 and 22K09296 to M.I.)

## Channel names follow the data headers (18 Oct 2026)

In 70 recordings the channel list of channels.tsv did not equal the data-file header (names, order or count), so `mne_bids.read_raw_bids` stopped with 'Channel mismatch' (or 'Duplicate channel names'); EEGDash renamed the data channels by position to the channels.tsv names, which gives wrong labels wherever the two lists are not aligned. Since 18 Oct 2026 every channels.tsv lists exactly the header channels, in header order, with the header names (MNE names: duplicated header labels numbered -0, -1).

Rows were matched to header channels BY NAME, never by position (exact; then case/whitespace; then the recorder prefix 'EEG '/'POL ', '_' and zero padding; then a trailing '-<reference>' token). Matched rows keep all their columns (type, units, status, ...); 8274 rows took the header name (the header labels carry '-AV' suffix).

12 channels.tsv rows had no channel in the data file (1 files) and were removed; they are kept verbatim under `sourcedata/channels-removed-2026-10-18/` (same relative path). Examples: `sub-072_ses-01_task-sleep_acq-A_run-01_ieeg.edf`: A41, A42, A43, A44, A45.

EEGDash's positional renaming had given wrong labels to 64 channels in 1 files (rows missing, extra or out of order before that position).

electrodes.tsv is unchanged: it names the contacts (e.g. `A1`), while channel names follow the recorder (e.g. `A1-AV`); to attach positions in MNE, map channel names to contact names first, e.g. `raw.rename_channels(lambda n: re.sub(r'-[A-Za-z0-9]+$', '', n))`.
