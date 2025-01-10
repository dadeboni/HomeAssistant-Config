

# Advanced Mobile Device Notifier Blueprint

## Overview

This blueprint allows you to send customized notifications to mobile devices based on their location state. You can filter notifications by location (**Home**, **Away**, **All Locations**, or **Custom Zone**). The blueprint is compatible with both iOS and Android devices and supports both critical and non-critical notifications.

---

## Features

- **Location-based Notification Filtering**: Send notifications based on the current location state of the devices (**Home**, **Away**, **All Locations**, or **Custom Zone**).
- **Critical and Non-Critical Alerts**: Option to send critical alerts (iOS) or high-priority notifications (Android) that override silent modes.
- **Customizable Sounds**: Choose from default or custom notification sounds.
- **Mobile Device Compatibility**: Works with devices integrated via the `mobile_app` integration in Home Assistant.

---

## Requirements

- **Home Assistant** setup with the `mobile_app` integration for mobile device tracking.
- Mobile devices registered under the `device_tracker` entity.
- A working zone configuration if using the **Custom Zone** filter.

---

## Inputs

- **Location Filter**: Select the filter for location state (**Home**, **Away**, **All Locations**, or **Custom Zone**).
- **Custom Zone Name**: If **Custom Zone** is selected, specify the exact name of the zone.
- **Notification Title**: The title of the notification.
- **Notification Message**: The content of the notification.
- **Critical Alert**: If enabled, the notification will be sent as a critical alert (iOS) or high-priority (Android).
- **Notification Sound**: Choose a sound for the notification (default sound or specify a custom sound name).

---

## How It Works

1. **Location Filtering**:
   - Based on the **Location Filter** selected, the blueprint identifies which mobile devices meet the criteria.
2. **Notification Sending**:
   - Notifications are sent to devices matching the filter conditions. If **Critical Alert** is enabled, notifications will override silent modes (iOS) or be marked high-priority (Android).
3. **Logging**:
   - The blueprint logs information about which devices received the notification and the parameters of the notification.

---

## Example Use Cases

- **Alert when family arrives home**: Use the **Home** filter to notify when someone arrives.
- **Notify when a device leaves a specific area**: Use the **Away** filter to send notifications when someone leaves a location.
- **Send an urgent alert to all family members**: Enable **Critical Alert** to override silent mode for critical situations.

---

## Logs

- **Logbook**: Records the notifications sent, including details like the notification title and message.
- **System Log**: Logs the devices that received the notification and details such as sound and priority.

---

## Troubleshooting

If notifications are not working as expected, check the following:

- **Device Integration**: Ensure devices are correctly integrated and tracked via the `device_tracker` entity.
- **Filter Criteria**: Confirm the correct **Location Filter** is selected and that devices meet the criteria.
- **System Logs**: Check logs for issues in notification delivery or blueprint execution.

---

## Example YAML

Below is an example YAML configuration for the blueprint:

```yaml
blueprint:
  name: Advanced Mobile Device Notifier
  author: debonisd
  description: >
    Send customized notifications to mobile devices based on their location state.
    Supports filtering by home, away, all locations, or a specific zone.
    Compatible with both iOS and Android devices, with options for critical and non-critical alerts.
  domain: script
  input:
    filter_state:
      name: Location Filter
      description: >
        Choose which devices to notify based on their current location state.
      selector:
        select:
          options:
            - label: Home
              value: home
            - label: Away
              value: away
            - label: All Locations
              value: all
            - label: Custom Zone
              value: custom_zone
      default: all

    custom_zone_name:
      name: Custom Zone Name
      description: >
        If 'Custom Zone' is selected above, enter the exact name of the zone here (case-sensitive).
        Leave empty if not using a custom zone.
      default: ""
      selector:
        text:

    notification_title:
      name: Notification Title
      description: The title of the notification.
      default: ""
      selector:
        text:

    notification_message:
      name: Notification Message
      description: The main content of the notification.
      default: ""
      selector:
        text:

    critical_alert:
      name: Critical Alert
      description: >
        If enabled, the notification will be sent as a critical alert (iOS) or high priority (Android).
        Use this for important notifications that should override silent modes.
      default: false
      selector:
        boolean:

    notification_sound:
      name: Notification Sound
      description: >
        Choose a sound for the notification. Use 'default' for the default sound,
        or specify a valid sound name for the device.
      default: "default"
      selector:
        text:
```

---

### Final Touch

> **Note**: If you encounter any issues or have suggestions, feel free to open an issue or submit a pull request in this repository.

---
