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
    "House Battery Switch Battery Fuse" -- "DC breaker panel"[color=orange];
    "House Battery Switch Bilge Fuse" -- "Bilge Pump Auto/Man Switch"[color=red];
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
}