# Code Example: Live Hand Position Transitions

The full implementation is not published in this portfolio repository. This condensed example shows the style of deterministic Core logic used for live positions without reproducing unpublished internal metadata. It is illustrative rather than a standalone compilable file; helper methods and overloads are omitted for brevity.

```csharp
public static LiveHandPosition Next(
    LiveHandPosition current,
    IReadOnlyCollection<int> activeSeats)
{
    ArgumentNullException.ThrowIfNull(current);
    Validate(current.TableNumber, current.TableSize, activeSeats);

    if (activeSeats.Count == 2)
    {
        int button = activeSeats.Contains(current.BigBlindSeat)
            ? current.BigBlindSeat
            : FindNextOccupied(
                current.TableSize,
                current.BigBlindSeat,
                activeSeats);

        return CreateHeadsUp(
            current.TableNumber,
            current.TableSize,
            checked(current.HandNumber + 1),
            button,
            activeSeats);
    }

    int nextBigBlind = FindNextOccupied(
        current.TableSize,
        current.BigBlindSeat,
        activeSeats);

    return CreateRingFromBlinds(
        current.TableNumber,
        current.TableSize,
        checked(current.HandNumber + 1),
        current.SmallBlindSeat,
        current.BigBlindSeat,
        nextBigBlind,
        activeSeats);
}
```

A heads-up transition explicitly enforces the tournament roles:

```csharp
return new LiveHandPosition
{
    ButtonSeat = buttonSeat,
    SmallBlindSeat = buttonSeat,
    BigBlindSeat = bigBlindSeat,
    PreflopFirstSeat = buttonSeat,
    PostflopFirstSeat = bigBlindSeat,
    PostflopLastSeat = buttonSeat,
    IsHeadsUp = true
};
```

Representative regression coverage included:

```csharp
[Fact]
public void OrdinaryUnusedSeatsAreSkipped()
{
    int[] participating = [2, 4, 6];

    LiveHandPosition current = Initialize(
        tableSize: 8,
        buttonSeat: 2,
        activeSeats: participating);

    LiveHandPosition next = Next(current, participating);

    Assert.Equal(4, next.ButtonSeat);
    Assert.Equal(6, next.SmallBlindSeat);
    Assert.Equal(2, next.BigBlindSeat);
}
```

The important architectural property is that the position calculation is deterministic and independent of WPF or SQLite. The UI projects the result, while persistence stores the canonical state and one prior undo state.
