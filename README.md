# COMI – Crop Operation Machine Index

COMI (Crop Operation Machine Index) is a formal, machine-usable schema that defines the semantic relationships between crops, agricultural operations, and machine capabilities. It provides a structured index for robotic and autonomous systems to reason about what operations are allowed, on which crops, at what growth stages, and using which machines or implements, while respecting environmental and spatial constraints. COMI is designed as a shared knowledge layer to support task planning, coordination, and compatibility validation across heterogeneous agents in precision agriculture.

## Implementation

This repository contains a complete JSON-based implementation of the COMI schema with:

### 📁 Structure
```
comi/
├── schemas/                      # JSON Schema definitions
│   ├── operation.schema.json     # Agricultural operations
│   ├── device.schema.json        # Machines and implements  
│   ├── crop.schema.json          # Crop definitions
│   └── vendor.schema.json        # Equipment manufacturers
├── data/                         # Structured data files
│   ├── operations/               # Operation definitions by category
│   ├── devices/                  # Device definitions by type
│   ├── crops/                    # Crop definitions by category
│   └── vendors/                  # Vendor information
├── rules/                        # Compatibility validation rules
├── examples/                     # Usage examples
└── comi.json                     # Main manifest/index
```

### 🚀 Quick Start

1. **Load the main index:**
```json
// Load comi.json to get the complete resource manifest
{
  "name": "COMI",
  "version": "1.0.0",
  "resources": { ... }
}
```

2. **Access structured data:**
```bash
# Operations by category
./data/operations/tillage.json
./data/operations/planting.json
./data/operations/protection.json
./data/operations/harvest.json

# Devices by type  
./data/devices/tractors.json
./data/devices/implements.json
./data/devices/harvesters.json

# Crops by category
./data/crops/cereals.json
./data/crops/legumes.json
./data/crops/vegetables.json
```

3. **Validate compatibility:**
```json
// Use rules/compatibility-rules.json for validation logic
{
  "rules": {
    "width_compatibility": { ... },
    "power_compatibility": { ... },
    "environmental_compatibility": { ... }
  }
}
```

### 🔧 Usage Examples

#### Basic Compatibility Check
```javascript
// Example: Can John Deere 6140R with Amazone D9-30 plant wheat?
const tractor = loadDevice("TRACTOR_JD_6140R_001");
const seeder = loadDevice("SEEDER_AMZ_D930_001"); 
const wheat = loadCrop("WHEAT_WINTER");
const operation = loadOperation("PLANT_SEED");

const result = validateCompatibility(
  [tractor, seeder], 
  wheat, 
  operation, 
  "PLANT"  // growth stage
);
// Result: VALID with 95% compatibility score
```

#### API Implementation
Suggested REST endpoints for consuming applications:

- `GET /operations` - List all operations
- `GET /devices/{category}` - Get devices by category  
- `GET /crops/{category}` - Get crops by category
- `POST /compatibility/check` - Validate combinations
- `POST /planning/suggest` - Suggest compatible devices

### 📊 Current Data

- **52 Operations** across 7 categories (tillage, planting, protection, harvest, fertilization, post-harvest, cultivation)
- **19 Devices** from 8 major vendors (tractors, implements, harvesters, tillage equipment, planting equipment)
- **12 Crops** across 4 categories (cereals, legumes, vegetables, oilseeds)  
- **6 Compatibility Rules** with validation logic
- **8 Equipment Vendors** with authentication keys

**Progress toward full list.md implementation:**
- ✅ 52/89 Operations (58% complete)
- ✅ 19/156 Device types (12% complete) 
- ✅ 12/250+ Crop varieties (5% complete)

### 🔄 Extensibility

The JSON-based structure allows easy extension:

- **Add Operations:** Follow `operation.schema.json` structure
- **Add Devices:** Follow `device.schema.json` structure  
- **Add Crops:** Follow `crop.schema.json` structure
- **Regional Variants:** Create localized data files
- **Custom Rules:** Extend compatibility validation logic

### 📋 File Formats

**Advantages of JSON:**
- ✅ Universal language support
- ✅ Human-readable with formatting
- ✅ Schema validation with JSON Schema
- ✅ Web browser native support
- ✅ Easy to version control
- ✅ Simple to extend and modify

**Schema Validation:**
All data files include JSON Schema references for structure validation and IDE support.

### 🎯 Use Cases

1. **Autonomous Systems:** Task planning and device selection
2. **Fleet Management:** Compatibility validation before field operations
3. **Precision Agriculture:** Operation optimization based on crop growth stages
4. **Equipment Dealers:** Compatibility checking for equipment combinations
5. **Research:** Agricultural system modeling and simulation

### 📈 Compatibility Rules

Six core validation rules ensure safe and effective operations:

1. **Width Compatibility** - Device width vs crop access requirements
2. **Growth Stage** - Operation timing restrictions  
3. **Device Capability** - Machine operation capabilities
4. **Power Compatibility** - Power supply and demand matching
5. **Attachment Compatibility** - Mechanical connection validation
6. **Environmental** - Weather and soil condition constraints

### 🔗 Integration

Load and validate data in any programming language:

```python
import json

# Load main index
with open('comi.json') as f:
    comi = json.load(f)

# Load specific data
with open('data/operations/planting.json') as f:
    planting_ops = json.load(f)

# Implement compatibility validation
def check_compatibility(devices, crop, operation):
    # Apply rules from rules/compatibility-rules.json
    pass
```

---

For detailed examples, see `examples/wheat-planting-example.json`

For schema definitions, see the `schemas/` directory

For questions or contributions, see [Issues](https://github.com/your-org/comi/issues)
