---
description: >-
  I would like to apologize for any shortcomings in the explanation I gave to
  the reader. 🥰
---

# Introduction 🦾

## The Goal Is Integrating Hadoop, Spark And Hive

## Hive and Spark

On this docs, am going to use **Hive 3.1.2** and **Spark 2.3.0,** am already tested on **Spark 3.1.2**, **hive** still doesn't work (😢 **may be am make mistake in a configuration**), that's make me frustrated about that 😭. And then am make decision to **downgrade a spark version to 2.3.0**. And then..., that's actually works 🤪.

By adding a some **configuration** in **hive**.

### By Source

{% embed url="https://cwiki.apache.org/confluence/display/Hive/Hive+on+Spark%3A+Getting+Started" %}

**Hive on Spark** is only tested with a **specific version of Spark**, so a given version of Hive is only guaranteed to work with a specific version of Spark. Other versions of Spark may work with a given version of Hive, but that is not guaranteed. Below is a list of Hive versions and their corresponding compatible Spark versions.

### Version Compatibility

| Hive Version | Spark Version |
| ------------ | ------------- |
| master       | 2.3.0         |
| 3.0.x        | 2.3.0         |
| 2.3.x        | 2.0.0         |
| 2.2.x        | 1.6.0         |
| 2.1.x        | 1.6.0         |
| 2.0.x        | 1.5.0         |
| 1.2.x        | 1.3.1         |
| 1.1.x        | 1.2.0         |

