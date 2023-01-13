# Enriched Device Type Library

## About this Library

This library is enriched copy of Netbox device type library [NetBox](https://github.com/netbox-community/devicetype-library).
It contains a set of device type definitions expressed in YAML and arranged by manufacturer. Each file represents a
discrete physical device type (e.g. make and model).

Some fiels are added, yaml files in stage of enrichment by additional data.
Definitions below - from original library + additional fields.
New items marked by *

## Device Type Definitions

Each definition must include at minimum the following fields:

- `manufacturer`: The name of the manufacturer which produces this device type.
- `model`: The model number of the device type. This must be unique per manufacturer.
- `slug`: A URL-friendly representation of the model number. Like the model number, this must be unique per
  manufacturer.

The following fields may optionally be declared:

- `part_number`: An alternative representation of the model number (e.g. a SKU).
- `u_height`: The height of the device type in rack units. Increments of 0.5U are supported. (Default: 1)
- `is_full_depth`: A boolean which indicates whether the device type consumes both the front and rear rack faces.
  (Default: true)
- `subdevice_role`: Indicates that this is a `parent` or `child` device. (Default: None)
- 'weight'*: device weight in kg
- 'MTBF'*: Mean Time Between Failures – MTBF (hours)
- 'typical_draw'*: The device typical power draw, with uplink card and load, but without SFPs, in watts.
- 'switch_capacity'*: ASIC bandwidth, Gbps
- 'fwd_rate'*: Packet processing rate, mpps
- 'depth'*: Device maximum possible (w/power supply) depth, cm

For further detail on these attributes and those listed below, please reference the
[schema definitions](schema/).

### Component Definitions

Valid component types are listed below. Each type of component must declare a list of the individual component templates
to be added.

- `console-ports`
- `console-server-ports`
- `power-ports`
- `power-outlets`
- `interfaces`
- `rear-ports`
- `front-ports`
- `module-bays`
- `device-bays`
- `inventory-items`

The available fields for each type of component are listed below.

#### Console Ports

- `name`: Name
- `label`: Label
- `type`: Port type slug (API value)

#### Console Server Ports

- `name`: Name
- `label`: Label
- `type`: Port type slug (API value)

#### Power Ports

- `name`: Name
- `label`: Label
- `type`: Port type slug (API value)
- `maximum_draw`: The port's maximum power draw, in watts (optional)
- `allocated_draw`: The port's allocated power draw, in watts (optional)

#### Power Outlets

- `name`: Name
- `label`: Label
- `type`: Port type slug (API value)
- `power_port`: The name of the power port on the device which powers this outlet (optional)
- `feed_leg`: The phase (leg) of power to which this outlet is mapped; A, B, or C (optional)

#### Interfaces

- `name`: Name
- `label`: Label
- `type`: Interface type slug (API value)
- 'poe_type'*: Typr of PoE standart: {type1-ieee802.3af, type2-ieee802.3at, type3-ieee802.3bt}
- `mgmt_only`: A boolean which indicates whether this interface is used for management purposes only (default: false)

#### Front Ports

- `name`: Name
- `label`: Label
- `type`: Port type slug (API value)
- `rear_port`: The name of the rear port on this device to which the front port maps
- `rear_port_position`: The corresponding position on the mapped rear port (default: 1)

#### Rear Ports

- `name`: Name
- `label`: Label
- `type`: Port type slug (API value)
- `positions`: The number of front ports that can map to this rear port (default: 1)

#### Module Bays

- `name`: Name
- `label`: Label
- `position`: The module bay's position within the parent device

#### Device Bays

- `name`: Name
- `label`: Label

#### Inventory Items

- `name`: Name
- `label`: Label
- `manufacturer`: The name of the manufacturer which produces this item
- `part_id`: The part ID assigned by the manufacturer
