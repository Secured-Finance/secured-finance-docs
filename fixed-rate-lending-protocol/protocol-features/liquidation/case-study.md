---
description: Example of the liquidation process
---

# 📋 Case Study

There would be 2 main patterns that trigger the liquidation. One is your collateral value decrease against your borrowed asset. The currency exchange rate represents this. The other is the borrowed asset value increase compared to your collateral. This might occur when the borrowing rates go lower.&#x20;

#### Case study

Bob borrowed 1,000 FIL with 15,000 USDC for 1y (365 days) at 20% at FILUSDC 10.0. Hence Bob's borrowed value is 10,000 USDC (= 1,000 FIL \* 10.0 FILUSDC FX rate), and his LTV is 66.7% (10,000/15,000).&#x20;

IF the FILUSDC exchange rate spike to 12.0 from 10.0 right after he borrowed, the value of his collateral decreases against his liability. In other words, his liability increased to 12,000 USDC (=1,000 FIL \* 12.0 FILUSDC FX rate). As a result, 50% of his position will be subject to liquidation since LTV reached 80% (12,000/15,000).&#x20;

Our Smart-contract will repay half of his obligation, helped by the liquidator, which is 500 FIL. Instead, Bob will lose his collateral of 6,420 USDC (=500 FIL \* 12.0 FILUSDC FX rate \* 107% penalty).&#x20;

After the liquidation process, Bob's position will be 500 FIL cash, 500 FIL borrowed with 8,580 USDC collateral (15,000 - 6,420 USDC). His LTV recovered to 69.9% (=500 FIL \* 12.0 FILUSDC FX rate / 8,580 collateral).



{% embed url="http://www.plantuml.com/plantuml/png/RL9TRu8m57tlhxWnCT644J3JAG-BWMN9acOFulPUuSgQb9QLglFVxu8IQxOdeEVZt7lekdN2kaEjM4DFMSX6Q0UZrEn685f8xu_pchuWCzfPKRYUaMVt52w_3x8KpjWUveobyF1Cj0HIOwqvGHn4KGIlRnmccL5AEBH29H3F-_EF_2MRCdANHq8w-pph3D91ZwNlmBUV2ImMuTDuoahqPKmRUZ57j906VJu9EdV0d-9Bw0h1TbIf2ukYnHRsrjGGHs44pa0y2oDlzdSy0MN1P4du-By1UG9RAwkAyjIr0saqx8s5-MNQcuWpFXXli17dWU4t0WrgeToPrWiUPqCntexyrWpt0WjJDme9dsom5b9BNS7ksbmo10Lm0mll9oo3-V8I5GmhK_ugNFsfTuswf6lp2m00" %}

