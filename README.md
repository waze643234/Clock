```csharp
using System;

public class Clock : IEquatable<Clock>
{
    private const int MinutesPerHour = 60;
    private const int MinutesPerDay = 24 * MinutesPerHour;
    private readonly int _totalMinutes;

    public Clock(int hours, int minutes)
    {
        int rawMinutes = hours * MinutesPerHour + minutes;
        _totalMinutes = ((rawMinutes % MinutesPerDay) + MinutesPerDay) % MinutesPerDay;
    }

    public Clock Add(int minutesToAdd) => new Clock(0, _totalMinutes + minutesToAdd);

    public Clock Subtract(int minutesToSubtract) => new Clock(0, _totalMinutes - minutesToSubtract);

    public override string ToString()
    {
        int hours = _totalMinutes / MinutesPerHour;
        int minutes = _totalMinutes % MinutesPerHour;
        return $"{hours:D2}:{minutes:D2}";
    }

    public bool Equals(Clock? other) => other is not null && _totalMinutes == other._totalMinutes;

    public override bool Equals(object? obj) => Equals(obj as Clock);

    public override int GetHashCode() => _totalMinutes.GetHashCode();
}
```
