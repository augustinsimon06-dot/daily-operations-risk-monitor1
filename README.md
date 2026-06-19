# Daily Operations Risk Monitor

Hands-on n8n and SQL project for automated weather risk monitoring.

## What it does

The workflow runs on a schedule, retrieves the next weather forecast for Paris, classifies operational risk, stores the result in PostgreSQL/Supabase, generates an AI summary with Gemini, and sends the summary by email.

## Workflow

```text
Schedule Trigger
→ Weather API
→ Split hourly forecasts
→ Keep future forecasts
→ Select next forecast
→ Prepare fields
→ Classify risk (HIGH / MEDIUM / NORMAL)
→ Store observation in PostgreSQL
→ Generate AI summary
→ Store AI summary
→ Send email
→ Mark email as submitted
```

## Tools

- n8n
- PostgreSQL / Supabase
- SQL and PL/pgSQL trigger
- MET Norway weather API
- Google Gemini
- SMTP / Gmail

## Risk rules

Demo thresholds used for learning purposes:

- **HIGH**: temperature ≥ 35 °C or wind speed ≥ 15 m/s
- **MEDIUM**: temperature ≥ 30 °C or wind speed ≥ 10 m/s
- **NORMAL**: otherwise

These thresholds are illustrative and are not official operational standards.

## Database fields

Main fields stored in `weather_observations`:

- `city`
- `forecast_time`
- `temperature`
- `wind_speed`
- `sql_risk_level`
- `sql_risk_reason`
- `n8n_risk_level`
- `n8n_risk_reason`
- `ai_summary`
- `email_sent_at`

A unique constraint on `(city, forecast_time)` prevents duplicate observations.

## Import and setup

1. Import `daily-operations-risk-monitor.json` into n8n.
2. Create your own PostgreSQL, Gemini, and SMTP credentials.
3. Replace the placeholder email addresses.
4. Create the `weather_observations` table and the SQL risk trigger.
5. Set the workflow timezone to `Europe/Paris`.
6. Test manually before activating the schedule.

## Security

The public workflow template contains no API keys, passwords, credential IDs, personal email addresses, or n8n instance identifiers.

## Learning goal

This project was built to practise API integration, JSON transformation, workflow automation, SQL storage, business-rule classification, AI summarisation, retries, and operational traceability.
