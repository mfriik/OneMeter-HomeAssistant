# OneMeter-HomeAssistant Integration Setup helper
Instructions for setting up integration in Home AssistantOS to GET readings from OneMeter Cloud

<h3>Rest Integration with OneMeter Cloud</h3>

1. Add the below snippet to your configuration.yaml file: 
``
rest: !include rest-integrations.yaml 
`` 
2. Download [rest-integrations.yaml](https://github.com/mfriik/OneMeter-Hass/blob/main/rest-integrations.yaml) place it in the same location as configuration.yaml and change ``<your device ID>`` & ``<API key>`` inside the file to values from [cloud.onemeter.com](https://cloud.onemeter.com/#/api) & .
2.1(Optional) Feel free to modify the file to your needs. Add/remove sensors modify settings etc. Currently, this integration has defined 7 sensors (all are extracted from OneMeter Cloud): \
   ``sensor.onemeterfirmware`` - it will display firmware version of the OneMeter in ``v.0.23.0`` format \
   ``sensor.onemeterlastrefresh`` - this shows a DateTime of when HA sent \
    last request to Cloud (this is calculated locally not based on cloud data) \
   ``sensor.onemeterlastread`` - this shows the DateTime of last successful read from OneMeterDevice \
   ``sensor.onemeterbattery`` - this shows battery voltage (kinda useless, \
    there does not seem to be any data on battery percentage in the JSON response from cloud.onemeter.com ) \
   ``sensor.onemeterenergy`` - this is what you need, this is a reading of your energy meter \
   ``sensor.onemetercurrentmonth`` - this shows usage in the current month rounded to 2 decimal places \
   ``sensor.onemeterpreviousmonth`` - this shows usage in the previous month rounded to 2 decimal places 
4. Upload [rest-integrations.yaml](https://github.com/mfriik/OneMeter-Hass/blob/main/rest-integrations.yaml) to the same folder as your configuration.yaml file in HA. 
5. RESTART your Home Assistant instance (reload is not enough)
6. New sensors should be available in your HASS environment. Add them to your Dashboards if you'd like

<h3>Utility Meter in Energy Dashboard</h3>

After you have successfully setup the REST Integration we can move forward and add our Sensor to Energy Dashboard. 

1. In Home Assistant: Go to Settings>Devices & services>Helpers
2. +Create Helper ``Utility meter`` (for more info on specific settings for this helper refer to [Utility Meter Documentation](https://www.home-assistant.io/integrations/utility_meter/) \
   Setup its name, and cycle and use ``sensor.onemeterenergy`` as input. Save your Helper
4. Go to Setting>Dashboards>Energy and in ``Grid consumption`` add your newly added ``Utility Meter`` Helper
5.(Optional). You can set pricing per kWh If you want to track that
6. Wait, as advised per HomeAssistant OS suggestion  - After setting up a new device, it can take up to 2 hours for new data to arrive in your energy dashboard.

You should start to see the vertical bars in your Energy Dashboard ;)
