# Temp.csv Dataset Overview

This repository contains `temp.csv`, a pricing time series that tracks daily market data for three tickers—Samsung Electronics (`005930.KS`), Apple (`AAPL`), and NVIDIA (`NVDA`). The file stores a three-level header (category, ticker, field) and daily values for the Close, High, Low, Open, and Volume metrics.

## File Structure
- **Ticker_Date** – Trading date in `YYYY-MM-DD` format.
- **<Ticker>_<Field>** – Numerical columns for each ticker and field pair. The available fields are `Close`, `High`, `Low`, `Open`, and `Volume`.

The dataset consists of **516 trading days** spanning **16 October 2023** through **10 October 2025**.

## Summary Statistics
The table below lists the minimum, mean, and maximum values observed for each price field per ticker.

### Samsung Electronics (`005930.KS`)
| Metric | Min | Mean | Max |
| --- | ---: | ---: | ---: |
| Close | 48,968.97 | 66,471.53 | 94,400.00 |
| High | 50,784.92 | 67,202.08 | 94,500.00 |
| Low | 48,968.97 | 65,822.65 | 92,700.00 |
| Open | 49,263.38 | 66,509.00 | 94,000.00 |
| Volume | 2,957,915.00 | 19,481,204.69 | 57,691,266.00 |

### Apple (`AAPL`)
| Metric | Min | Mean | Max |
| --- | ---: | ---: | ---: |
| Close | 163.82 | 209.52 | 258.10 |
| High | 165.21 | 211.47 | 259.24 |
| Low | 162.91 | 207.33 | 256.72 |
| Open | 164.17 | 209.29 | 257.99 |
| Volume | 23,234,700.00 | 56,558,297.39 | 318,679,900.00 |

### NVIDIA (`NVDA`)
| Metric | Min | Mean | Max |
| --- | ---: | ---: | ---: |
| Close | 40.30 | 115.60 | 192.57 |
| High | 40.85 | 117.54 | 195.62 |
| Low | 39.21 | 113.41 | 191.06 |
| Open | 40.43 | 115.59 | 193.51 |
| Volume | 105,157,000.00 | 325,122,504.81 | 1,142,269,000.00 |

## Reproducing the Statistics
The following Python snippet parses the multi-level header and recomputes the descriptive statistics without relying on external dependencies:

```python
import csv
from datetime import datetime

with open("temp.csv", newline="") as f:
    reader = csv.reader(f)
    header_rows = [next(reader) for _ in range(3)]
    columns = [
        f"{t or ''}_{m or c}".strip("_") or "Ticker_Date"
        for c, t, m in zip(*header_rows)
    ]
    records = [row for row in reader if any(row)]

# Convert rows to dictionaries and compute statistics as needed
```

This approach avoids third-party libraries (e.g., `pandas`), which may be unavailable in restricted environments.
