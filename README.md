# MACRO – Machine Crop Operation Index

MACRO (Machine Crop Operation Index) is a formal, machine-usable schema that defines the semantic relationships between crops, agricultural operations, and machine capabilities. It provides a structured index for robotic and autonomous systems to reason about what operations are allowed, on which crops, at what growth stages, and using which machines or implements, while respecting environmental and spatial constraints. MACRO is designed as a shared knowledge layer to support task planning, coordination, and compatibility validation across heterogeneous agents in precision agriculture.

## Implementation

This repository contains a complete JSON-based implementation of the MACRO schema with comprehensive agricultural data.

### Structure
```
macro/
├── macro.json                        # Main manifest/index
├── PLAN.md                           # Implementation roadmap
├── progress.md                       # Implementation statistics
├── schemas/                          # JSON Schema definitions (10 files)
│   ├── operation.schema.json         # Agricultural operations
│   ├── device.schema.json            # Basic device definitions
│   ├── enhanced_device.schema.json   # Devices with attachment systems
│   ├── crop.schema.json              # Crop definitions with growth stages
│   ├── vendor.schema.json            # Equipment manufacturers
│   ├── field_context.schema.json     # Field state and environment
│   ├── workflow.schema.json          # Operation sequencing
│   ├── equipment_chain.schema.json   # Multi-machine coordination
│   ├── compatibility.rules.json      # Equipment compatibility rules
│   └── attachment_types.json         # Hitch and attachment definitions
├── data/                             # Structured data files
│   ├── operations/                   # 12 operation files (119 operations)
│   ├── devices/                      # 18 device files (102 devices)
│   ├── crops/                        # 7 crop files (41 crops)
│   ├── vendors/                      # Vendor database (30 vendors)
│   ├── workflows/                    # Workflow definitions (8 workflows)
│   ├── contexts/                     # Field context examples (3 contexts)
│   ├── equipment_chains/             # Multi-machine chains (3 chains)
│   └── validation/                   # Validation rules (5 rule sets)
├── rules/                            # Compatibility validation rules
└── examples/                         # Usage examples
```

### Quick Start

1. **Load the main index:**
```json
// Load macro.json to get the complete resource manifest
{
  "name": "MACRO",
  "version": "1.0.0",
  "resources": { ... }
}
```

2. **Access structured data:**
```bash
# Operations by category
./data/operations/tillage.json
./data/operations/planting.json
./data/operations/harvest.json
./data/operations/fertilization.json
./data/operations/protection.json
./data/operations/post_harvest.json
./data/operations/cultivation.json
./data/operations/irrigation.json
./data/operations/maintenance.json
./data/operations/forestry.json
./data/operations/livestock.json
./data/operations/specialty_operations.json

# Devices by type
./data/devices/tractors.json
./data/devices/enhanced_tractors.json
./data/devices/harvesters.json
./data/devices/specialty_harvesters.json
./data/devices/tillage_equipment.json
./data/devices/planting_equipment.json
./data/devices/implements.json
./data/devices/enhanced_implements.json
./data/devices/loaders_material_handling.json
./data/devices/front_loader_tools.json
./data/devices/advanced_application.json
./data/devices/livestock_equipment.json
./data/devices/forestry_equipment.json
./data/devices/hay_forage_equipment.json
./data/devices/irrigation_equipment.json
./data/devices/specialty_utility_vehicles.json
./data/devices/precision_ag_equipment.json
./data/devices/grain_handling_equipment.json

# Crops by category
./data/crops/cereals.json
./data/crops/legumes.json
./data/crops/vegetables.json
./data/crops/oilseeds.json
./data/crops/fruits_orchards.json
./data/crops/forages.json
./data/crops/fiber_industrial.json
```

3. **Validate compatibility:**
```json
// Use data/validation/validation_rules.json for validation logic
{
  "rule_sets": [
    "equipment_compatibility",
    "operation_sequencing",
    "field_constraints",
    "environmental_conditions",
    "data_integrity"
  ]
}
```

### Usage Examples

#### Basic Compatibility Check
```javascript
// Example: Can John Deere 8R with Case IH planter plant corn?
const tractor = loadDevice("TRACTOR-8R-001");
const planter = loadDevice("PLANTING-ROW-001");
const corn = loadCrop("CORN_GRAIN");
const operation = loadOperation("ROW_CROP_PLANTING");

const result = validateCompatibility(
  [tractor, planter],
  corn,
  operation,
  "PLANTING"  // growth stage
);
// Result: VALID with compatibility details
```

#### Workflow Execution
```javascript
// Execute a tillage workflow
const workflow = loadWorkflow("WF-CONV-TILLAGE-001");
const field = loadContext("CTX-IOWA-CORN-001");

// Validate prerequisites
if (field.state === workflow.steps[0].field_state_requirements) {
  // Execute primary tillage
  executeOperation(workflow.steps[0].operations[0]);
}
```

#### Equipment Chain Coordination
```javascript
// Coordinate grain harvest chain
const chain = loadChain("EC-GRAIN-HARVEST-001");
// Returns: combine -> grain cart -> semi-truck coordination
```

### Current Data

| Category | Files | Entries |
|----------|-------|---------|
| **Operations** | 12 | 119 |
| **Devices** | 18 | 102 |
| **Crops** | 7 | 41 |
| **Vendors** | 1 | 30 |
| **Workflows** | 2 | 8 |
| **Field Contexts** | 1 | 3 |
| **Equipment Chains** | 1 | 3 |
| **Validation Rules** | 1 | 5 rule sets |

#### Operations Coverage (119 total)
- Tillage (13): Primary/secondary tillage, plowing, cultivating, harrowing
- Planting (11): Precision planting, drilling, broadcasting, transplanting
- Harvest (15): Grain, forage, silage, root crop harvesting
- Fertilization (8): Broadcasting, banding, injection, variable rate
- Crop Protection (12): Herbicide, insecticide, fungicide, biological control
- Post-Harvest (9): Baling, raking, tedding, windrowing, chopping
- Cultivation (6): Inter-row, mechanical weeding, flame weeding
- Irrigation (7): Sprinkler, drip, pivot, linear move, flood
- Maintenance (8): Pruning, mowing, scouting, soil sampling
- Forestry (5): Timber harvest, delimbing, bucking, chipping
- Livestock (5): Feed mixing, distribution, milk transport, manure
- Specialty (20): Cotton, potato, grape, sugarcane, specialty crops

#### Devices Coverage (102 total)
- Tractors (6): Utility, row crop, high HP with attachment systems
- Harvesters (10): Combines, forage harvesters, specialty harvesters
- Tillage Equipment (4): Plows, cultivators, harrows, disks
- Planting Equipment (4): Planters, drills, seeders
- Implements (8): General and enhanced with attachment requirements
- Loaders & Material Handling (5): Front loaders, skid steers, telehandlers
- Front Loader Tools (4): Buckets, forks, bale grabs
- Application Equipment (5): Sprayers, spreaders
- Livestock Equipment (4): Feed mixers, milk tankers
- Forestry Equipment (4): Harvesters, forwarders, chippers
- Hay & Forage Equipment (12): Mowers, balers, tedders, rakes, wrappers
- Irrigation Equipment (10): Pivots, linear move, drip, pumps, sensors
- Specialty Utility Vehicles (13): ATVs, UTVs, farm trucks, sprayers
- Precision Ag Equipment (7): GPS, auto-steer, yield monitors, drones
- Grain Handling Equipment (6): Grain carts, augers, dryers, vacuums

#### Crops Coverage (41 total)
- Cereals (8): Winter/Spring wheat, grain/silage corn, barley, oats, rice
- Legumes (6): Soybean, field pea, dry bean, lentil, chickpea, alfalfa
- Vegetables (6): Potato, sugar beet, carrot, onion, tomato, cabbage
- Oilseeds (5): Canola (winter/spring), sunflower, flax, safflower
- Fruits & Orchards (6): Apple, wine grape, strawberry, blueberry, cherry, orange
- Forages (6): Timothy, orchardgrass, ryegrass, red/white clover, sorghum-sudan
- Fiber & Industrial (4): Cotton, hemp, sugarcane, tobacco

### Key Features

- **Farming Simulator-style attachment systems** - Realistic equipment connections
- **Power requirements validation** - Tractor/implement compatibility checking
- **Operation sequencing** - Field state transitions and workflow management
- **Multi-machine coordination** - Equipment chain definitions for complex operations
- **Growth stage restrictions** - Crop-specific operation timing
- **Environmental validation** - Weather and soil condition constraints
- **Comprehensive vendor database** - 30 major equipment manufacturers

### Extensibility

The JSON-based structure allows easy extension:

- **Add Operations:** Follow `schemas/operation.schema.json` structure
- **Add Devices:** Follow `schemas/device.schema.json` or `schemas/enhanced_device.schema.json`
- **Add Crops:** Follow `schemas/crop.schema.json` structure
- **Add Workflows:** Follow `schemas/workflow.schema.json` structure
- **Regional Variants:** Create localized data files
- **Custom Rules:** Extend validation logic in `data/validation/`

### Compatibility Rules

Five core validation rule sets ensure safe and effective operations:

1. **Equipment Compatibility** - Power, attachment, and weight validation
2. **Operation Sequencing** - Field state requirements and transitions
3. **Field Constraints** - Size, slope, and soil type validation
4. **Environmental Conditions** - Weather and moisture constraints
5. **Data Integrity** - Schema compliance and reference validation

### Integration

Load and validate data in any programming language:

```python
import json

# Load main index
with open('macro.json') as f:
    macro = json.load(f)

# Load specific data
with open('data/operations/planting.json') as f:
    planting_ops = json.load(f)

with open('data/devices/tractors.json') as f:
    tractors = json.load(f)

# Load validation rules
with open('data/validation/validation_rules.json') as f:
    rules = json.load(f)

# Implement compatibility validation
def check_power_compatibility(tractor, implement):
    tractor_hp = tractor['power_specifications']['power_output']['rated_power_hp']
    required_hp = implement['attachment_requirements']['required_power']['optimal_minimum_hp']
    return tractor_hp >= required_hp
```

### Workflows

MACRO includes pre-defined workflows for common agricultural systems:

**Crop Workflows:**
- Winter wheat production cycle
- Grain corn production cycle
- Soybean production cycle
- Hay production cycle

**Tillage Workflows:**
- Conventional tillage system
- Reduced tillage system
- No-till system
- Strip-till system

---

For detailed examples, see `examples/`

For schema definitions, see the `schemas/` directory

*Schema Version: 1.0.0 | Last Updated: January 2026*
