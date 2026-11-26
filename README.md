# AIKillsWhat — AI Exposure Dataset (open data)

Machine-readable export of the [AIKillsWhat.com](https://aikillswhat.com) evidence pipeline:
**AI Exposure Scores** per occupation (task-level, graded from published evidence), plus the **AI model registry**.

> The AI Exposure Score measures the share of an occupation's core tasks that current AI systems can
> demonstrably do today, evidenced from published sources (model releases, capability research, adoption and
> hiring signals). It is **not a prediction of job losses**. Task statements © O*NET OnLine, U.S. Department
> of Labor (CC BY 4.0). Scores © AIKillsWhat.com — [methodology](https://aikillswhat.com/research/how-we-score).

## Files

| File | Contents |
| --- | --- |
| [data/aikillswhat-occupations.csv](data/aikillswhat-occupations.csv) | occupations with composite AI Exposure Score, task coverage, evidence count, employment/median wage (BLS context), SOC code, industry |
| [data/aikillswhat-models.csv](data/aikillswhat-models.csv) | AI model registry: provider, release date, modality, provenance |

## Columns (occupations)

`slug, title, soc_code, category, industry, ai_exposure_score, score_delta, evidence_count, core_task_count, task_coverage, employment_bls, median_wage_usd_bls, score_calculated_at_utc, detail_url`

## Columns (models)

`slug, name, provider, provider_slug, release_date, modality, provenance, detected_at_utc, detail_url`

## File format

UTF-8 CSV with a header of `#` comment lines (source, license, generation time) followed by the column row. Row counts change as the pipeline refreshes. Skip the comment lines when loading.

## Quick start

```bash
git clone https://github.com/Aboodseada1/ai-exposure-dataset.git
cd ai-exposure-dataset
pip install pandas   # Python 3.9+
```

```python
import pandas as pd

jobs = pd.read_csv("data/aikillswhat-occupations.csv", comment="#")
models = pd.read_csv("data/aikillswhat-models.csv", comment="#")

# Ten occupations with the highest exposure score
print(jobs.sort_values("ai_exposure_score", ascending=False)
          [["title", "soc_code", "ai_exposure_score"]].head(10))

# Models released per provider
print(models.groupby("provider").size().sort_values(ascending=False).head(10))
```

No API key or environment variables are needed. The data is plain files.

## Tests

There is no test suite. The hourly GitHub Action (`.github/workflows/refresh.yml`) only refreshes the CSV files.

## Refresh

The [live site](https://aikillswhat.com/data) re-exports these files continuously; an hourly GitHub Action in
this repo commits whenever the source changes. You can also pull the data by API:
[api-docs](https://aikillswhat.com/api-docs) (endpoints /api/jobs, /api/models — rate-limited, no signup).

## Interact with the data

- Per-job dossiers: https://aikillswhat.com/jobs
- Embeddable exposure widget for any occupation (copy from a job page)
- Research briefs: [most exposed](https://aikillswhat.com/research/top-25-ai-exposure-jobs) ·
  [safest](https://aikillswhat.com/research/safest-jobs) · [monthly digest](https://aikillswhat.com/research/ai-labor-monthly)

## License & attribution

- Task statements © O*NET OnLine, U.S. Department of Labor (CC BY 4.0)
- AI Exposure Scores and derived fields © AIKillsWhat.com — attribution: "AIKillsWhat.com, aikillswhat.com/methodology"
