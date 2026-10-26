# YouTube Tech Channel Analysis

An exploratory analysis of 130 YouTube tech and coding channels and their recent videos. The goal is to inform an animated YouTube series that teaches computer science to kids ages 12-18, with episodes of 10-15 minutes.

## Key findings

- **Video length:** The raw gap in views for 10-25 minute videos disappears once each video is compared with its own channel's typical video. 10-15 minute videos performed about average (1.03).
- **Topic:** Seven of eight topic groups landed between 0.96 and 1.07 relative performance. Cybersecurity looked lower (0.87) but is based on only 20 videos.
- **Channel growth:** Upload frequency is only weakly related to growth (rank correlation 0.19). The fastest-growing channels followed two paths: fewer, high-view videos, or very high volume.
- **Takeaway:** The data shows no evidence that a 10-15 minute format or a particular topic gives an edge. Quality and audience fit likely matter more, and this data can't measure either.

## Data

Both files are in `assignment_5/`:

| File | Rows | Description |
|---|---|---|
| `youtube_tech_channels_20251120_133753.xlsx` | 130 | One row per channel: subscribers, total views, total videos, creation date, country |
| `youtube_tech_videos_20251120_133004.xlsx` | 1,300 | 10 recent videos per channel: title, publish date, views, likes, comments, duration |

Both were collected on 2025-11-20, so all counts are as of that date.

## Data cleaning

- Converted text dates to real dates and calculated channel age.
- Ignored the `duration_readable` column, which was wrong for videos under an hour. Built `duration_min` from the raw `duration` column instead.
- Recovered 11 blank video IDs from the video URLs (all began with a hyphen, which Excel likely blanked out).
- Removed 6 videos with zero length and zero views (scheduled streams that had not aired). The cleaned table has 1,294 videos.
- Repaired garbled characters in video titles.

## Methods

- **Views per day:** views divided by video age, with a 1-day minimum.
- **Relative performance:** a video's views per day divided by its own channel's median, so 1.0 means typical for that channel. This removes the effect of channel size.
- **Topics:** assigned by keywords in video titles, so groups are approximate.
- **Channel growth:** subscribers divided by channel age, compared with upload frequency using rank correlation.

## Limitations

- Each channel contributes only its 10 most recent videos, not its best ones.
- Several topic groups have 20-60 videos, so small differences are noise.
- The channels are not aimed specifically at teens, and the data says nothing about a 12-18 year old audience.
- Results show association only, not cause.

## How to run it

Requires Python 3.9 or later.

```bash
git clone https://github.com/FichardReynman/carlos-data-analysis
cd carlos-data-analysis 

python3 -m venv env
source env/bin/activate
pip install -r requirements.txt

cd assignment_5
jupyter notebook
```

Then open `data_analysis.ipynb` and run the cells in order (Kernel > Restart & Run All).

## Tools

Python, pandas, matplotlib, Jupyter, and openpyxl (for reading Excel files).
