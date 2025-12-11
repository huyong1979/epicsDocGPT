# EPICS `mbbo` Record Examples

Below are two complete examples of `mbbo` records:

---

## 1. `mbbo` Record Using **Soft Channel**

This version uses `DTYP = "Soft Channel"` and therefore its numerical values (`ZRVL`, `ONVL`, etc.) **must be ≤ 15**, because Soft Channel does not support raw value bit-patterns.

```epics
record(mbbo, "example:mbboSoft") {
    field(DESC, "Soft Channel mbbo example")
    field(DTYP, "Soft Channel")
    field(VAL, 0)

    # Enumerated states (MAX 0–15)
    field(ZRST, "State 0")
    field(ONST, "State 1")
    field(TWST, "State 2")
    field(THST, "State 3")

    # Corresponding numeric values (0–15)
    field(ZRVL, 0)
    field(ONVL, 1)
    field(TWVL, 2)
    field(THVL, 3)
}
````
**Note**: ChatGPT can make mistakes. The values of `ZRVL`, `ONVL`, etc. can be > 15. However, the field of VAL (the value of `example:mbboSoft`) must be <= 15.

---

## 2. `mbbo` Record Using **Raw Soft Channel**

Use `DTYP = "Raw Soft Channel"` when you need:

* Large values (e.g., `RVAL = 255`)
* Direct bit-pattern mapping via `RVAL`

```epics
record(mbbo, "example:mbboRaw") {
    field(DESC, "Raw Soft Channel mbbo example")
    field(DTYP, "Raw Soft Channel")

    # Enumerated strings
    field(ZRST, "Low Power")
    field(ONST, "Medium Power")
    field(TWST, "High Power")
    field(THST, "Turbo Mode")

    # Raw numeric bit-patterns (can be > 15)
    field(ZRVL, 0)     # 0b0000
    field(ONVL, 85)    # 0b01010101
    field(TWVL, 170)   # 0b10101010
    field(THVL, 255)   # 0b11111111

    # Initial raw value
    field(RVAL, 0)
}
```

---

```
```
