# Bulk Onboarding with Agent Smith

When a new agent registers with Rewst, the workflow hits Azure IoT Hub’s **identity registry up to five times**  
(two queries → create → get → tag‑update).  
On a **Standard‑1 (S1) hub** that registry is capped at **100 identity operations per minute, per unit**.

```
100 ops ÷ 5 ops / agent ≈ **20 agents / min / unit**
```

> **Important — Plan your own throttle or scale‑up**  
> Rewst deliberately leaves rate‑limiting in **your** hands so you can tune roll‑outs to match your  Azure budget.  
> A large, unthrottled burst will exceed IoT Hub limits, pile up **HTTP 429** retries, and slow down _all_ of your Rewst workflows during onboarding.  
> To avoid this, either add jitter/batching in your RMM job **or** do a temporary IoT Hub scale‑up before the push.

---

## What’s an IoT Hub *Unit*?

A *unit* is simply a slice of IoT Hub capacity you can dial up or down.  
All per‑minute limits scale linearly with both **units** _and_ **SKU size**:

| SKU | Identity ops / min / unit | Agents / min / unit (with our 5‑call workflow) |
|-----|---------------------------|-----------------------------------------------|
| **S1 / S2** | 100 | ~20 |
| **S3** | 5 000 | ~1 000 |

---

## Quick Playbook

| Choose one | How to do it | Throughput | Cost Example* |
|------------|--------------|------------|---------------|
| **Scale the hub (fast)** | ```bash
az iot hub update -n <hub> --sku S3 --unit 2
```<br>Run 5 min before deploy; scale back to `S1 --unit 1` when done. | ~2 000 agents / min | S3 ≈ **$3.47 per unit‑hour** → 2 units × 4 h ≈ **$28** |
| **Throttle in RMM (no Azure cost)** | • Deploy ≤ 50 agents / min / S1‑unit.  
• Add jitter: `Start‑Sleep (Get‑Random 5 3600)` before install. | Current hub limit | Longer total time; more scripting effort |

\* US‑East pricing, rounded.

---

### Rules of Thumb

* Default **S1 × 1** → **≈ 20 agents / min**.  
* Formula: `Agents / min = (100 or 5 000) × units ÷ 5`.  
* Scaling is live—existing connections stay up; a few messages may arrive out of order (harmless).

Pick the path that matches your timeline and budget to avoid 429s during mass onboarding.
