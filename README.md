# DisplayDashApp for iOS
DisplayDash Navigator App for iOS

## DisplayDash 3.0 iOS Application BLE Documentation

DisplayDashApp for iOS provides navigation functionality by calculating routes and communicating key navigation information to the DisplayDash 3.0 device using Bluetooth Low Energy (BLE). This section outlines the BLE services and characteristics used in the application, along with the expected data format for communication.

### BLE Service and Characteristics

#### Service UUID

- **Service Name**: DisplayDash Navigation Service
- **UUID**: `4fafc201-1fb5-459e-8fcc-c5c9c331914b`

#### Characteristics

The following characteristics are defined for communication with the DisplayDash 3.0:

| Characteristic Name         | UUID                                      | Description                                   |
|-----------------------------|------------------------------------------|-----------------------------------------------|
| Next Street Name            | `beb5483e-36e1-4688-b7f5-ea07361b26a8` | Name of the next street to navigate to.      |
| Estimated Time of Arrival   | `ca83fac2-2438-4d14-a8ae-a01831c0cf0d` | Estimated time of arrival at the destination.|
| Direction Distance          | `0343ff39-994e-481b-9136-036dabc02a0b` | Distance to the next directional change.      |
| ETA in Minutes              | `563c187d-ff17-4a6a-8061-ca9b7b70b2b0` | ETA expressed in minutes.                     |
| Distance to Arrival         | `8bf31540-eb0d-476c-b233-f514678d2afb` | Total distance to the destination.            |
| Direction Arrow             | `a602346d-c2bb-4782-8ea7-196a11f85113` | Directional arrow indicating next turn.      |

### BLE Communication Flow

#### Initial Connection

1. **Device Initialization**: The DisplayDash 3.0 initializes the BLE server with the specified service UUID.
2. **Advertising**: The device advertises its presence, including the service UUID to allow iOS devices to discover it.

#### Data Transmission

The iOS app can write data to the defined characteristics to send navigation information. Each characteristic will update the corresponding data on the DisplayDash device.

##### Example Usage

- To set the next street name:
  ```swift
  let nextStreetUUID = CBUUID(string: "beb5483e-36e1-4688-b7f5-ea07361b26a8")
  let nextStreetData = "Main Street"
  peripheral.writeValue(nextStreetData.data(using: .utf8)!, for: nextStreetCharacteristic, type: .withResponse)
