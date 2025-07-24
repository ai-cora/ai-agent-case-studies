# Appendix: Token Usage Calculation for Voice Mode Configuration Work

## Time Zone Conversion

**Work Period**: 30 minutes from 2:08 AM to 2:38 AM Melbourne time (July 24, 2025)

**Melbourne to UTC Conversion**:
- Melbourne is UTC+10 (AEST - Australian Eastern Standard Time)
- 2:08 AM Melbourne, July 24 = 16:08 UTC, July 23
- 2:38 AM Melbourne, July 24 = 16:38 UTC, July 23

## ccusage Billing Block Analysis

The work falls within this billing block:
- **Block Start**: 2025-07-23T14:00:00.000Z (July 24, 12:00 AM Melbourne)
- **Block End**: 2025-07-23T19:00:00.000Z (July 24, 5:00 AM Melbourne)
- **Actual End**: 2025-07-23T16:39:40.068Z (July 24, 2:39:40 AM Melbourne)

## Token Usage for the Block

```json
{
  "startTime": "2025-07-23T14:00:00.000Z",
  "endTime": "2025-07-23T19:00:00.000Z",
  "actualEndTime": "2025-07-23T16:39:40.068Z",
  "entries": 211,
  "totalTokens": 14049860,
  "costUSD": 31.803399749999993
}
```

## Calculation Method

Since ccusage tracks usage in 5-hour blocks, we cannot extract exact usage for just the 30-minute work period. However, we can make estimates:

1. **Total Block Duration**: 2 hours 39 minutes 40 seconds (12:00 AM - 2:39:40 AM)
2. **Work Period**: 30 minutes (2:08 AM - 2:38 AM)
3. **Work Period as % of Block**: 30 min / 159.67 min = 18.8%

### Estimated Token Usage for 30-minute Work

**Conservative Estimate** (assuming even distribution):
- Total tokens in block: 14,049,860
- Estimated work tokens: 14,049,860 × 0.188 = 2,641,374 tokens
- Estimated cost: $31.80 × 0.188 = $5.98

**Refined Estimate** (considering session patterns):
- The block had 211 API entries
- Assuming ~40-50 entries during the 30-minute intensive work period
- Estimated proportion: 45/211 = 21.3%
- Estimated tokens: 14,049,860 × 0.213 = 2,992,620 tokens
- Estimated cost: $31.80 × 0.213 = $6.77

## Token Breakdown

The block contained:
- Input tokens: 462
- Output tokens: 35,519
- Cache creation tokens: 470,245
- Cache read tokens: 13,543,634

Most tokens (96.4%) were cache reads, which are much cheaper than regular tokens.

## Conclusion

**Best Estimate for 30-minute Configuration Work**:
- **Tokens**: ~2.6-3.0 million tokens
- **Cost**: ~$6-7 USD
- **Note**: This is higher than my initial $0.50-$1.00 estimate but more accurate given the actual ccusage data

The higher cost reflects:
1. Significant cache reading for context
2. Multiple file operations and edits
3. Test creation and documentation
4. Git operations and status checks

## Data Source

```bash
# Command used to extract billing block data:
npx ccusage blocks --since 20250723 --until 20250724 --json

# Filtered for the relevant time period using jq
```