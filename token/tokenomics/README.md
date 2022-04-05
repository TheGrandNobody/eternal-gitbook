---
description: The economics and crypto-economics of the Eternal token
---

# 🪙 ETRNL

### <mark style="color:blue;">Definition</mark>

<mark style="color:purple;">ETRNL (spelled out "Eternal") is fundamentally, one of the main three forces in the entire long-termist synergetic system contributing to the overall success of Eternal. Functionally, it is Eternal's governance and utility token, as well as the primary currency of usage on the platform.</mark>

## Economic Value

The intrinsic value of ETRNL is generated and guaranteed by seven factors:

### 1/2. Gaging Fees & Buybacks

For all gages, regardless of centralized or decentralized applications, a small fee is taken on any deposited assets which are not ETRNL. This fee occurs upon withdrawal of the asset from the given gage and is instantly transferred to the Eternal Treasury. This ensures that **ETRNL is backed by a diversified basket of goods, which accrues in both variety and quantity over time.** Furthermore, half of the fee is also sold back for ETRNL placing upward pressure on the token's price.

### 3. Automatic Liquidity Provision

On every transaction with ETRNL, a small fee is computed. **ETRNL provides its own liquidity to decentralized exchanges** using a fraction of this fee. As the **LP-tokens received from this are only accessible by the** [**Eternal Fund**](../../governance/eternal-fund.md)**, this increases the token’s price resilience to changes, rendering it more stable.**&#x20;

### 4/5. Reward Redistribution & Funding (Indefinite Deflation)

One other fraction of the aforementioned ETRNL fee is sent to the Eternal Treasury and another is redistributed to all holders of ETRNL. As the Eternal Treasury accumulates ETRNL, it slowly begins compounding its ETRNL reserves over time. **The total ETRNL supply temporarily deflates as part of it remains unused in the** Eternal Treasury’s reserves **for an indefinite period of time. This percentage of the supply can be re-injected into the economy in the event that ETRNL's rate of deflation becomes detrimentally high.**

### **6.** Allocation of Reserves

All of the Eternal Treasury's reserves are to be allocated by the [Eternal Fund](../../governance/eternal-fund.md) to diverse financial strategies, in an effort of maximizing the economic value of said reserves. The strategies which the reserves undergo result in an increase of their value. The quantitative increase in value is also allocated by the [Eternal Fund](../../governance/eternal-fund.md). Hence, the **Eternal Treasury's reserves compound over time, leading to an exponential increase in intrinsic value of ETRNL in the long-term.**

### 7/8. Supply burn and Limited Supply (Definite Deflation)

At present, most major currencies in our world's economy are inflationary. This is also true to cryptocurrencies. With such contexts in mind, deflation leads to the increase of purchasing power of a given token. This is further reinforced by the idea that the other currencies against which ETRNL is compared to are inflationary, hence their purchasing power decreases. **ETRNL is deflationary by standard due to having a limited supply**, where no new ETRNL will be printed. Additionally, **ETRNL also burns its supply, which introduces a rate of deflation. This rate is modifiable and can therefore be deactivated in any event of economical distress.**

## Circular Flow of ETRNL

The fee mechanisms implemented in ETRNL are key players in ensuring the sustainability of the system. The Eternal Treasury distributes ETRNL to individuals who gage on the platform. This ETRNL will inevitably find its way back to the Eternal Treasury through the token fee and gaging fee mechanisms.

![Diagram of the circular flow of the Eternal token](<../../.gitbook/assets/Eternal flow.png>)

Given $$T_e$$, the period of time during which liquid gages can be offered before the Eternal Treasury's usable reserves run out, $$\alpha$$, the daily count of transacted ETRNL subject to fees, $$F_r$$, the ETRNL treasury funding rate, $$R_r$$, the ETRNL reward-redistribution rate, $$S_t$$, the present total supply of ETRNL, and $$\psi$$, the minimum ETRNL reserves to ever remain in the treasury, the total amount of ETRNL flowing in, $$A_{in}$$ is given by:

$$
A_{in} = T_e\alpha(F_r + \frac{\psi{R_r}}{S_t})
$$

Conversely, assume that not a single liquid gage closes in favor of the Eternal treasury. Taking the treasury's total ETRNL reserves, $$R_t$$ the liquid gage's treasury risk, $$r$$ and the impermanent loss incurred by any given liquid gage, $$\beta$$, the amount flowing out of the treasury, $$A_{out}$$ can be defined by:

$$
A_{out} = \frac{(R_t - \psi)(\beta + r + \beta{r})}{1 + 2r}
$$

Thus, at any given moment, the treasury regulates ETRNL outflow such that:

$$
A_{in} \geq A_{out}
$$

## ETRNL Flywheel: The Virtuous-Cycle model

![Diagram of the Eternal Flywheel](<../../.gitbook/assets/The Eternal Flywheel.png>)

Taking the factors affecting the economic value of ETRNL and the modus operandi of the Eternal Treasury, one particular observation quickly becomes clear: gaging fees and gages which close in favour of the treasury create an upward pressure on the price of ETRNL. Therefore, gaging activity creates upward pressure on the price of ETRNL. Simultaneously, gaging activity also leads to ETRNL flowing out. Some ETRNL flowing out finds its way back into the treasury which consequently distributes more gages and further contributes to ETRNL's upward price pressure. As this occurs, part of the ETRNL supply deflates, further contributing to the value of ETRNL. A greater price value of ETRNL also means the treasury is now able to offer more gages to users as its reserves are now worth more and thus can accumulate more fees. These events keep repeating themselves unless $$\alpha$$ is 0. Thus, this leads to the virtuous cycle depicted above: the ETRNL Flywheel.

