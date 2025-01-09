Advanced Mobile Device Notifier Blueprint
Overview

This blueprint allows you to send customized notifications to mobile devices based on their location state. You can filter notifications by location (Home, Away, All Locations, or Custom Zone). The blueprint is compatible with both iOS and Android devices, and supports both critical and non-critical notifications.
Features

    Location-based Notification Filtering: Send notifications based on the current location state of the devices (Home, Away, All Locations, or Custom Zone).
    Critical and Non-Critical Alerts: Option to send critical alerts (iOS) or high-priority notifications (Android) that override silent modes.
    Customizable Sounds: Choose from default or custom notification sounds.
    Mobile Device Compatibility: Works with devices integrated via mobile_app in Home Assistant.

Requirements

    Home Assistant setup with mobile_app integration for mobile device tracking.
    Mobile devices registered under the device_tracker entity for each mobile device.
    A working zone configuration if using the Custom Zone filter.

Inputs

    Location Filter: Select the filter for location state (Home, Away, All Locations, or Custom Zone).
    Custom Zone Name: If Custom Zone is selected, specify the exact name of the zone.
    Notification Title: The title of the notification.
    Notification Message: The content of the notification.
    Critical Alert: If enabled, the notification will be sent as a critical alert (iOS) or high-priority (Android).
    Notification Sound: Choose a sound for the notification (default sound or specify custom sound name).

How It Works

    Location Filtering: Based on the Location Filter selected, the blueprint will identify which mobile devices meet the criteria.
    Notification Sending: Notifications are sent to the devices that match the filter conditions. If Critical Alert is enabled, notifications will be sent as critical (iOS) or high-priority (Android).
    Logbook and System Logs: The blueprint logs information about which devices received the notification, as well as the parameters of the sent notification.

Example Use Cases

    Alert when family arrives home: Use the Home filter and set a notification message that lets you know when someone arrives.
    Notify when a device leaves a specific area: Use the Away filter to notify when someone is away.
    Send an urgent alert to all family members: Enable Critical Alert to override silent mode for critical situations.

Logs

    Logbook: The logbook records the notifications sent with details such as notification title and message.
    System Log: Logs the devices that received the notification and details of the notification (sound, priority, etc.).

Example YAML

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

Troubleshooting

If you are not seeing notifications, check the following:

    Ensure that the devices are correctly integrated and tracked via the device_tracker entity.
    Confirm that the correct location filter is selected and that the devices meet the filtering criteria.
    Check the system logs for any issues with the notification process.


