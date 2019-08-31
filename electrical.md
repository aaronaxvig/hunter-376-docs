![Alt text](https://g.gravizo.com/source/main?https%3A%2F%2Fraw.githubusercontent.com%2Faaronaxvig%2Fhunter-376-docs%2Fmaster%2Felectrical.md)

<details> 
<summary></summary>

graph Main {
    rankdir=LR;
    "Shunt" -- "Negative Bus Bar";
    "Shunt" -- "Charger/Inverter";
    "Shunt" -- "Negative Battery Bus Bar"
    "Shunt" -- "Positive Battery Bus Bar"[label="Voltage-sense",color=red];
    "Shunt" -- "Engine Start Battery"[label="Voltage-sense",color=red];
    "Negative Battery Bus Bar" -- "Battery 1";
    "Negative Battery Bus Bar" -- "Battery 2";
    "Negative Battery Bus Bar" -- "Battery 3";
    "Negative Battery Bus Bar" -- "Battery 4";
    "Battery 1" -- "Battery Breaker 1"[color=red];
    "Battery 2" -- "Battery Breaker 2"[color=red];
    "Battery 3" -- "Battery Breaker 3"[color=red];
    "Battery 4" -- "Battery Breaker 4"[color=red];
    "Battery Breaker 1" -- "Positive Battery Bus Bar"[color=red];
    "Battery Breaker 2" -- "Positive Battery Bus Bar"[color=red];
    "Battery Breaker 3" -- "Positive Battery Bus Bar"[color=red];
    "Battery Breaker 4" -- "Positive Battery Bus Bar"[color=red];
    "Positive Battery Bus Bar" -- "400A Fuse"[color=red];
    "400A Fuse" -- "House Battery Switch"[color=red];
    "400A Fuse" -- "Charger/Inverter"[color=red];
    "Charger/Inverter" -- "Engine Start Battery"[label="Trickle-charge",color=red];
    // House Battery Switch
    subgraph cluster_house_battery_switch {
        label="House Battery Switch"
        "House Battery Switch" -- "House Battery Switch Battery Fuse"[color=orange];
        "House Battery Switch" -- "House Battery Switch Bilge Fuse"[color=red];
    }
    "House Battery Switch Battery Fuse" -- "DCBP Main Breaker"[color=orange];
    "House Battery Switch Bilge Fuse" -- "Bilge Pump Auto/Man Switch"[color=red];
    "House Battery Switch Bilge Fuse" -- "BPAMS DC +"[color=red];
    "House Battery Switch" -- "House Battery Switch Bus Bar"[color=red];
    // Windlass
    "House Battery Switch Bus Bar" -- "Windlass Breaker"[color=red];
    "Negative Bus Bar" -- "Windlass Negative Bus Bar";
    "Windlass Motor" -- "Windlass Negative Bus Bar";
    subgraph cluster_windlass {
        label="Windlass"
        "Windlass Breaker" -- "Windlass Contactor"[color=red];
        "Windlass Contactor" -- "Windlass Negative Bus Bar";
        "Windlass Up Switch" -- "Windlass Negative Bus Bar";
        "Windlass Up Switch" -- "Windlass Contactor";
        "Windlass Down Switch" -- "Windlass Negative Bus Bar";
        "Windlass Down Switch" -- "Windlass Contactor";
        "Windlass Motor" -- "Windlass Contactor"[color=red];
    }
    // Watermaker
    "House Battery Switch Bus Bar" -- "Watermaker HP Pump Breaker"[color=red];
    "Watermaker HP Pump" -- "Negative Bus Bar";
    subgraph cluster_watermaker {
        label="Watermaker"
        "Watermaker HP Pump Breaker" -- "Watermaker HP Pump"[color=red];
    }
    // Solar Charging
    "Solar Charge Controller" -- "House Battery Switch Bus Bar"[color=red];
    "Solar Charge Controller" -- "Negative Bus Bar";
    subgraph cluster_solar {
        label="Solar charging"
        "Solar Charge Controller" -- "Solar Panel Aft Port";
        "Solar Panel Aft Port" -- "Solar Panel Aft Starboard";
        "Solar Panel Aft Starboard" -- "Solar Panel Fore";
        "Solar Panel Fore" -- "Solar Charge Controller";
    }
    "Engine Start Battery" -- "Negative Bus Bar";
    "Engine Start Battery" -- "Winch Contactor"
    "Engine Start Battery" -- "Engine Battery Switch"[color=red];
    "Engine Battery Switch" -- "Battery Isolator"[color=red];
    "House Battery Switch Bus Bar" -- "Battery Isolator"[color=red];
    "Battery Isolator" -- "Battery Combiner Relay"[color=red];
    "Battery Isolator" -- "Battery Combiner Relay"[color=red];
    "Engine Start Battery" -- "Winch Breaker"[color=red];
    subgraph cluster_electric_winch {
        label="Electric winch"
        "Winch Breaker" -- "Winch Contactor"[color=red];
        "Winch Motor" -- "Winch Contactor";
        "Winch Motor" -- "Winch Contactor"[color=red];
        "Winch Button" -- "Winch Contactor";
        "Winch Button" -- "Winch Contactor"[color=red];
    }
    "Engine Start Solar Charge Controller" -- "Engine Start Solar Panel";
    "Engine Start Solar Charge Controller" -- "Engine Start Solar Panel"[color=red];
    "Engine Start Solar Charge Controller" -- "Negative Bus Bar";
    "Engine Start Solar Charge Controller" -- "Engine Start Battery"[color=red];
    "Negative Bus Bar" -- "Engine Ground Lug";
    "SR 12V In" -- "Engine Battery Switch"[label="Supply",color=red]
    subgraph cluster_engine {
        label="Engine ignition";
        subgraph cluster_starter_relay {
            label="Starter Relay"
            "SR 12V In"
            "SR Coil Activate"
            "SR Output"
            "SR Ground (Frame)"
        }
        subgraph cluster_key_relay {
            label="Key Relay"
            "KR Coil +"
            "KR Coil -"
            "KR Load +"
            "KR Load -"
        }
        "Aux Start Switch" -- "SR 12V In"[color=red];
        "Aux Start Switch" -- "SR Coil Activate"[color=red];
        "SR Ground (Frame)" -- "Engine Ground Lug";
        "SR Output" -- "Starter"
        "Key" -- "KR Coil +";
        "Key" -- "Alternator"[color=red];
        "KR Coil -" -- "Engine Ground Lug"
        "KR Load +" -- "SR 12V In"
        "KR Load -" -- "SR Coil Activate"[color=yellow];
        "Alternator" -- "Engine Ground Lug";
        "Alternator" -- "SR 12V In"[color=red];
        "Starter" -- "Engine Ground Lug"[label=Frame];
    }
    subgraph cluster_dc_breaker_panel {
        label="DC Breaker Panel";
        "DCBP Main Breaker";
        "DCBP Negative Bus Bar"
        subgraph cluster_current_meter {
            label="Current Meter";
            "DCBP CM DC In";
            "DCBP CM DC Out";
        }
        "DCBP Main Breaker" -- "DCBP CM DC In";
        subgraph cluster_voltage_meter {
            label="Voltage Meter";
            "DCBP VM DC +";
            "DCBP VM DC -";
        }
        subgraph cluster_dcbp_bus_a {
            label="DCBP Bus A"
            "DCBP Bus Bar A" -- {
                "DCBP Breaker Panel Lights",
                "DCBP Breaker Cabin Lights 1",
                "DCBP Breaker Cabin Lights 2",
                "DCBP Breaker Water Pressure",
                "DCBP Breaker Bilge Counter/Alarm",
                "DCBP Breaker Head Vent and Inverter Fans",
                "DCBP Breaker Refrigerator"
            }
        }
        subgraph cluster_dcbp_bus_b {
            label="DCBP Bus B"
            "DCBP Bus Bar B" -- {
                "DCBP Breaker Stereo",
                "DCBP Breaker LP Gas",
                "DCBP Breaker Watermaker Supply",
                "DCBP Breaker Fans",
                "DCBP Breaker Shower Pump",
                "DCBP Power Gauges",
                "DCBP Breaker"
            }
        }
        subgraph cluster_dcbp_bus_c {
            label="DCBP Bus C"
            "DCBP Bus Bar C" -- {
                "DCBP Breaker Anchor Lights",
                "DCBP Breaker Steaming Lights",
                "DCBP Breaker Deck Lights",
                "DCBP Breaker Running Lights",
                "DCBP Breaker Instruments",
                "DCBP Breaker VHF/AIS",
                "DCBP Breaker Autopilot"
            }
        }
        "DCBP CM DC Out" -- "DCBP Bus Bar C"
        "DCBP Bus Bar C" -- "DCBP Bus Bar B"
        "DCBP Bus Bar B" -- "DCBP Bus Bar A"
        "DCBP Bus Bar B" -- "DCBP VM DC +"
        "DCBP Negative Bus Bar" -- "DCBP VM DC -"
    }
    subgraph cluster_bilge_systems {
        label="Bilge Systems"
        subgraph cluster_bilge_automan {
            label="Bilge Pump Auto/Manual Switch"
            "BPAMS DC +"
            "BPAMS Auto"
            "BPAMS Manual"
        }
        subgraph cluster_pump_cycle_counter {
            label="Pump Cycle Counter";
            "PCC Signal Input";
            "PCC DC +";
            "PCC DC -";
        }
        subgraph cluster_high_water_float_switch {
            label="High Water Float Switch";
            "HWFS A";
            "HWFS B";
        }
        subgraph cluster_high_water_alarm {
            label="High Water Alarm";
            "HWA DC +";
            "HWA DC -";
        }
        subgraph cluster_bilge_pump_float_switch {
            label="Bilge Pump Float Switch";
            "BPFS A"
            "BPFS B"
        }
        subgraph cluster_bilge_pump {
            label="Bilge Pump";
            "BP DC +";
            "BP DC -";
        }
        "Bilge Splice"
    }
    "DCBP Negative Bus Bar" -- "Negative Bus Bar"
    "DCBP Breaker Bilge Counter/Alarm" -- "PCC DC +"[color=red];
    "DCBP Breaker Bilge Counter/Alarm" -- "HWFS A"[color=red];
    "DCBP Negative Bus Bar" -- "PCC DC -";
    "HWFS B" -- "HWA DC +"[color=red];
    "HWA DC -" -- "DCBP Negative Bus Bar";
    "PCC Signal Input" -- "Bilge Splice";
    "BPFS B" -- "Bilge Splice";
    "BPAMS Manual" -- "Bilge Splice";
    "Bilge Splice" -- "BP DC +";
    "BP DC -" -- "Negative Bus Bar";
    "BPFS A" -- "BPAMS Auto"
}
</details>
