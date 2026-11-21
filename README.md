# 📡 SGT Telemetry 2018

**Bezdrôtová telemetria pre elektrickú formulu: číta správy z CAN zbernice a posiela ich po rádiu do boxov.**

![Rok](https://img.shields.io/badge/rok-2018-blue) ![MCU](https://img.shields.io/badge/STM32-F105RB-03234b) ![Zbernica](https://img.shields.io/badge/CAN-bus-red) ![Tím](https://img.shields.io/badge/STUBA-Green%20Team-green)

> **Rok realizácie:** 2018 · **Tagy:** `stm32` `can-bus` `telemetry` `formula-student` `electric-vehicle` `embedded` `rf` `uart` `stuba` `green-team`

## O projekte

Firmvér telemetrickej jednotky pre elektrický monopost tímu **STUBA Green Team** (Formula Student, sezóna 2018). Jednotka sa pripojí na CAN zbernicu vozidla, zachytáva správy od ostatných elektronických modulov a odosiela ich cez UART do rádiového modulu, aby sa dali sledovať mimo vozidla.

## Ako to funguje

```
Moduly vozidla ──CAN──► STM32F105 (filter + príjem) ──USART1──► RF modul ──► prijímač v boxoch
```

- **CAN1** s ID filtrom (16-bitové masky) a príjmom cez prerušenie (`HAL_CAN_Receive_IT`).
- **USART1** odosiela prijaté dáta v krátkych rámcoch do rádiového modulu.
- Súbor `CAN2018.h` / `CAN2018.c` definuje **aplikačný protokol CAN** celého vozidla, teda štruktúry správ a ich funkcie na odosielanie.

### Správy v protokole CAN2018

| ID | Správa |
|---|---|
| `0x10` | BBOX_power |
| `0x15` | wheel_RPM: otáčky kolies |
| `0x20` | BBOX_status |
| `0x25`, `0x70` | FU_Values_1 / FU_Values_2 |
| `0x50` | BMS_State (batériový manažment) |
| `0x60` | ECU_State (riadiaca jednotka) |
| `0x80` | Interconnect |

## Technológie

STM32F105RB · STM32 HAL · STM32CubeMX (`telemetry.ioc`) · CAN 2.0 · USART · Atollic TrueSTUDIO

## Zostavenie

Projekt importujte do TrueSTUDIO (alebo iného Eclipse IDE s ARM GCC), v `main.c` odkomentujte potrebné štruktúry z `CAN2018.h` a nahrajte cez ST-LINK.

## Autor

**Vratislav Režo** ([@VRDragon](https://github.com/VRDragon))
