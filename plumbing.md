graph Main {
    "Water Tank" -- "Water Fill";
    "Water Tank" -- "Strainer";
    "Water Tank" -- "Vent";
    "Water Tank" -- "Watermaker product output";
    "Strainer" -- "Pressure Pump";
    "Pressure Pump" -- "Carbon Filter";
    "Carbon Filter" -- "Tee 1";
    "Tee 1" -- "Watermaker Flush Valve";
    "Tee 1" -- "Tee 2";
    "Tee 2" -- "V-Berth Sink";
    "Tee 2" -- "Tee 3";
    "Tee 3" -- "Aft Supply"[color=blue];
    "Tee 3" -- "Tee 4";
    "Tee 4" -- "Tempering Valve"[color=blue];
    "Tee 4" -- "One-way Valve";
    "One-way Valve" -- "Water Heater";
    "Water Heater" -- "Tempering Valve"[color=red];
    "Tempering Valve" -- "Aft Supply"[color=red];
    "Aft Supply" -- "Kitchen Faucet"[color=red];
    "Aft Supply" -- "Bathroom Faucet"[color=red];
    "Aft Supply" -- "Bathroom Shower"[color=red];
    "Aft Supply" -- "Cockpit Shower"[color=red];
    "Aft Supply" -- "Kitchen Faucet"[color=blue];
    "Aft Supply" -- "Bathroom Faucet"[color=blue];
    "Aft Supply" -- "Bathroom Shower"[color=blue];
    "Aft Supply" -- "Cockpit Shower"[color=blue];
    "Raw Water Seacock" -- "Raw Water Strainer";
    "Raw Water Strainer" -- "Raw Water Tee"
    "Raw Water Tee" -- "WM Raw Water Pump"
    "Raw Water Tee" -- "AC Raw Water Pump"
    "Watermaker Flush Valve" -- "WM Flush Timer"
    subgraph cluster_watermaker {
        label="Watermaker";
        "WM Raw Water Pump" -- "WM Raw One-way Valve";
        "WM Raw One-way Valve" -- "WM Input Water Tee";
        "WM Flush Timer" -- "WM Fresh One-way Valve";
        "WM Fresh One-way Valve" -- "WM Input Water Tee";
        "WM Input Water Tee" -- "WM Filter 1";
        "WM Filter 1" -- "WM Filter 2";
        "WM Filter 2" -- "WM Input Pressure Gauge";
        "WM Input Pressure Gauge" -- "WM High Pressure Pump";
        "WM High Pressure Pump" -- "WM Membrane";
        "WM Membrane" -- "WM TDS Meter"[label="Product"];
        "WM Membrane" -- "WM High Pressure Gauge"[label="Waste"];
        "WM High Pressure Gauge" -- "WM Needle Valve";
        "WM Needle Valve" -- "Overboard 2";
        "WM TDS Meter" -- "WM Flow Meter";
        "WM Flow Meter" -- "WM Product Tee";
        "WM Product Tee" -- "WM Product Discard Valve";
        "WM Product Tee" -- "WM Product To Tank Valve";
        "WM Product To Tank Valve" -- "Watermaker product output";
    }
    "AC Raw Water Pump" -- "AC Compressor";
    "AC Compressor" -- "Overboard 1"
}