---
uid: Meadow.Foundation.Grove.Sensors.Light.LightSensor
remarks: *content
---

| LightSensor | |
|--------|--------|
| Status | <img src="https://img.shields.io/badge/Working-brightgreen" style="width: auto; height: -webkit-fill-available;" alt="Status badge: working" /> |
| Source code | [GitHub](https://github.com/WildernessLabs/Meadow.Foundation.Grove/tree/main/Source/LightSensor) |
| NuGet package | <a href="https://www.nuget.org/packages/Meadow.Foundation.Grove.Sensors.Light.LightSensor/" target="_blank"><img src="https://img.shields.io/nuget/v/Meadow.Foundation.Grove.Sensors.Light.LightSensor.svg?label=Meadow.Foundation.Grove.Sensors.Light.LightSensor" alt="NuGet Gallery for Meadow.Foundation.Grove.Sensors.Light.LightSensor" /></a> |

### Code Example

```csharp
LightSensor sensor;

public override Task Initialize()
{
    Console.WriteLine("Initialize...");

    sensor = new LightSensor(Device, Device.Pins.A01);

    var consumer = LightSensor.CreateObserver(
        handler: result => Console.WriteLine($"Observer filter satisfied: {result.New.Millivolts:N2}mV, old: {result.Old?.Millivolts:N2}mV"),
        filter: result =>
        {
            if (result.Old is { } old)
            { //c# 8 pattern match syntax. checks for !null and assigns var.
                return (result.New - old).Abs().Millivolts > 500;
            }
            return false;
        });

    sensor.Subscribe(consumer);

    sensor.Updated += (sender, result) => 
    {
        Console.WriteLine($"Voltage Changed, new: {result.New.Millivolts:N2}mV, old: {result.Old?.Millivolts:N2}mV");
    };

    return Task.CompletedTask;
}

public override async Task Run()
{
    var result = await sensor.Read();
    Console.WriteLine($"Initial read: {result.Millivolts:N2}mV");

    sensor.StartUpdating(TimeSpan.FromMilliseconds(1000));
}

```

[Sample project(s) available on GitHub](https://github.com/WildernessLabs/Meadow.Foundation.Grove/tree/main/Source/LightSensor/Sample/LightSensor_Sample)

### Wiring Example

| LightSensor | Meadow Pin |
|--------|------------|
| GND    | GND        |
| VCC    | 3.3V       |
| RX     | D01        |
| TX     | D00        |
