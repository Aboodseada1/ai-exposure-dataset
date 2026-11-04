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
