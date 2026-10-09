# SLA Monitoring Checklist

Practical checklist for monitoring an **electronic voucher management system (EVMS)** against operational SLAs.

## 1. Scope the SLA

| Service | In SLA? | Notes |
|---------|---------|-------|
| POS / API voucher vend | Usually yes | Core revenue path |
| PIN redeem / top-up | Usually yes | Customer completion path |
| Balance / stock enquiry | Often yes | Dealers depend on it |
| Bulk report export | Sometimes | Separate target if slow by design |
| Marketing website | Usually no | Do not conflate with EVMS |

## 2. Signals to collect

- [ ] Request success rate by endpoint and channel (POS, USSD, API)
- [ ] Latency histograms (p50 / p95 / p99), not only averages
- [ ] Dependency health: DB, vault/HSM, partner IN/UCIP links
- [ ] Queue depth / backlog for async issuance
- [ ] Reconciliation job freshness (last successful run age)

## 3. Synthetic probes

- [ ] External probe vends a **test** SKU only
- [ ] Probe redeems or voids safely so stock does not leak to production reports
- [ ] Probes run from at least two networks / regions if dealers are multi-country
- [ ] Probe failure pages on-call after N consecutive fails

## 4. Alerting hygiene

- [ ] SEV-1: vend or redeem success below threshold for M minutes
- [ ] SEV-2: elevated latency or single-channel failure
- [ ] Silence windows documented for approved maintenance
- [ ] Each alert links to a runbook section

## 5. Monthly report pack

- [ ] Measured availability vs target
- [ ] Top incident list with TTX (acknowledge / mitigate / restore)
- [ ] Error budget remaining
- [ ] Partner carve-outs clearly listed
- [ ] Action items owned by name and date

## Related

See the main [README](../README.md). Product context: [electronic voucher management system](https://evdsystem.com/electronic-voucher-management-system-evd-telecom/).
